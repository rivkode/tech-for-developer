# NoSQL

Lsm tree
Log structured storage engine 기반으로 동작
Log파일이란 append only , 끝에 추가만 됨

Sstable
Compaction
Key value
Write

Write 가 빠른 이유는 log파일 끝에 추가만 하는것이므로 디스크가 빠르게 처리할 수 있다
Get은 느리다 왜냐하면 full scan을 해야하기 때문이다
어떻게 개선할 수 있을까?
Index 사용
In memory hashmap를 index로 사용할 수 있음 key로 데이터의 key를 저장하고 value로 데이터의 주소값인 byte offset 을 저장

하지만 여기에 문제가 생김
Update를 하게될 경우 기존 file을 찾서 업데이트 하는게 아니라 append only이므로 중복 데이터가 발생하게 된다
그렇개되면 불필요한 데이터가 많아지므로 이걸 해결해야함
여기서 segment file, compaction이 나오게된다
기존에 모든 데이터를 하나의 log file에 저장했다면 이를 일정크기로 쪼개서 Segment file에 저장한다는 개념이다
이렇게되면 하나의 segment file이 저장되었을때 해당file은 mutable하다.
하나의 segment file이 저장되었을때는 해당 file은 변경되지 않으므로 update로 인한 중복된 값들을 제거할 수 있는 환경이 된다. 그러므로 중복값들을 제거해주며 이를 compaction이라고 한다.
그리고 hash index는 segmemt file별로 존재한다


허지만 이렇게만 만들면 단점이 존재할 수 있다
1. 모든 hash key들을 memory에서 들고있어야 한다.
   Hashmap으로 index를 구현했으므로
2. Range query하기가 어렵다
   Segment file 내에서는 중복이 없지만 segment file 끼리는 중복이 발생하므로, 그리고 segment file의 index는 정렬이 되어있지 않으므로

그래서 Sorted string table 을 사용함 기존에는 사용자의 입력순서대로 저장이 되었지먼
Sst 는 segment file을 key 로 정렬한 것

새로운 데이터를 추가할때에는 sst에 자로 추가하는것리 아니라 memory에 있는 binary tree 이진트리에 저장함 이때 self balancing 으로 균형은 항상 보장이 된다
이 트리를 보통 memtable 고 칭함

이후 memtable이 일정 size를 넘어가게되면 그때 sst 를 만듦

Sst로 만들때 memtable에는 binary tree 형태로 되어있으니 정렬된 순서대로 읽기가 쉽고 그러므로 정렬된 순서대로 append only 형태로 읽은 순서대로 쭉 sst 를 만들 수 있는것이다

그러므로 disk 입장에서는 들어온 순서대로 쓰여지기때문에 밀어넣는다? 는것이 가능해진다 write이 굉장이 빠르게 진행될 수 있다

만약 저장하는 중에 db에서 crash가 발생하면?
사실 log file에 저장된 내역들이 존재함 다만 정렬이 되지 않은채로 저장됨
이 log file을 바탕으로 다시 memtable을 만들 수 있음
그래서 sst 가 만들어지누이후에는 해당하는 log file은 모두 지워지게 됩니다.

여기서 read를 하기 위해 memtable에 저장되었던 주소값을 기반으로 데이터를 찾게 될텐데 이 read 퍼포먼스를 더 높이기 위해서는 memory를 사용하은 방법이 있습니다.

정렬된 Key와 주소값을 memory에 저장하여 메모리에서 스캔할 수 있도록 합니다. 그리고 모든 key 주소 값들이 memory에 있을 필요는 없습니다. 애초에 정렬이 되어 들어가기때문에 특정 값을 찾고싶을 경우 주변에 있는 key값을 통해 특정 범위만 탐색하면 되는 것을 알 수 있으므로 범위에 속하는 key들만 찾으면 굳이 명확한 주소값이 없더라도 값을 찾을 수 있습니다.

이것이 lsm tree가 wrtie 와 read를 빠르게 할 수 있는 원리입니다.

Write이 빠른 이유는 append only로 빠르게 되고 read는 memtable, index를 통해 빠르게 할 수 있게 됩니다.

그리고 Index가 부족하더라도 괜찮은 이유는 특정 인덱스의 범위만 알 수 있더라도 범위를 통해 찾을 수 있으므로 sstable에 key겂으로 정렬이 되어있으니

Cap이론

분산환경에서 availability 가용성, consistence 일관성, partition tolerance 분할 내성
이 세가지를 비즈니스적 관점에서 어떻게 트레이드오프를 하여 최상의 가치를 만들어갈 것 인가에 대한 내용

세가지중 항상 무조건 2가지를 가져가는 것이 아니라 3가지를 어떤방법, 조건으로 고르게 가져갈 것인가에 대한 내용

Atm 사용자, 인출, 입금, 조회 3가지 기능에 대해 설명

Sharding

샤딩은 row를 기준으로 서로 다른 데이터베이스 서버에 저장하는 것이 특징이다
이렇게 서로 다른 서버에 저장함으로써 얻을 수 있는 점은 트래픽 부하를 분산할 수 있다
그리고 partition key는 shard key로 불리며 각 shard로 나누어서 테이블을 부른다

Nosql은 스키마가 없다. 즉 아무형태의 데이터를 다 넣을 수 있다 다만 json형식이어야 함
이렇게 자유로우니 이를 flexible schema라고 한다
찾고싶은 데이터는 sql과 비슷하고 원하는 key값을 기준르로 찾을 수 있다 db.student.find({name:"lee"})

이렇게 되다보니 application 레벨에서 스티마를 관리해야하더라

그리고 nosql은 중복 다 드루와 다 허용함
이는 append only 와 관련

그리고 nosql은 scale out에 최적화됨
왜?
분산환경을 지원하니
