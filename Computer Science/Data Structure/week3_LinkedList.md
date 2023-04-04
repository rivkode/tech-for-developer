# 자료구조

본 내용은

- 유용재 교수님의 [자료구조 3주차](https://www.youtube.com/watch?v=-kjd6PPeihw&t=5841s)

을 정리한 내용입니다.

![image](https://user-images.githubusercontent.com/109144975/225552568-b89e3a9f-093a-497f-aaca-f6de81843b03.png)

# Linked List와 연결형 자료구조

목차
- 정적 배열과 동적 배열
- Linked List와 그 특징
- 양방향 Linked List
- 클래스와 객체 지향
- Linked List의 실제적 구현

## 정적 배열과 동적 배열

> 자료구조란 ?
> 
> 자료를 제어하는 원리
> 어떤 자료를 어떻게 제어할 것인가 ?

## 정적 배열을 이용한 데이터의 저장

정적 배열
- 자료구조의 한 형태인 배열에 속하며, 그 중에서도 크기가 고정되어 있는 것
- 특징
  - 인덱스를 활용한 접근
  - 원소간 순서 구분을 공유
- 정적배열의 한계
  - 배열의 크기를 초과할 때 추가로 데이터를 넣을 수 없음
  - 배열의 크기가 처음부터 정해져있으므로

동적 배열
- 자료구조의 한 형태인 배열에 속하며, 그 중에서도 정적 배열과는 달리 크기가 가변적인 것
- 배열의 공간이 부족해질 경우, 크기를 두 배로 늘린 후 기존의 데이터를 복사하여 넣는 방식
- 인덱스를 활용해 데이터에 접근이 가능하며, 원소간 순서는 구분됨

동적배열의 데이터 접근
- 배열은 인덱스를 이용하므로, 인덱스 값을 알면 곧장 데이터 값을 얻을 수 있음
  - 앞에 몇개의 데이터가 있는지 상관하지 않고 해당 인덱스의 주소값과 일치하는 것을 바로 찾으므로
- 즉, 데이터 접근 시간은 데이터 크기 N과 무관하므로 시간복잡도는 O(1)

동적배열의 데이터 말단 삽입

![image](https://user-images.githubusercontent.com/109144975/225554570-82f32fef-1df8-4b3b-be75-63b693c187ac.png)

말단 삽입의 경우 O(1)이다. 하지만 모든칸이 다 찾을 경우 ?

> A : O(N) 왜냐하면 N개의 데이터를 새로운 장소에 복사한 뒤 공간을 늘려야 하므로

동적 배열의 데이터 임의 위치 삽입
- 말단이 아닌 위치에 데이터를 삽입하려는 경우, 뒤쪽 데이터들을 모두 한 칸씩 밀어야만 삽입이 가능하므로 최악의 경우 n 개의 기존 데이터를 모두 밀어야 함
- 따라서, 최악의 경우 시간복잡도는 O(N)


동적배열의 데이터 삭제
- (말단 삭제) 삽입에서와 유사하게, 다른 데이터에 영향을 주지 않으므로 시간복잡도는 O(1)
- (임의 위치 삭제) 삭제 대상 우측의 데이터가 모두 좌측으로 밀리므로 최악의 경우 시간복잡도는 O(N)

정리
- [] 인덱스로 접근 가능
- append(), insert(index, value)로 특정 위치 혹은 마지막에 데이터 추가 가능
- del(lst[index])로 특정 위치에 데이터 삭제 가능


## Linked List와 그 특징

![image](https://user-images.githubusercontent.com/109144975/225557727-abd91c35-58d9-4fd7-b118-89f9b5ac4981.png)

기존의 동적배열에서의 삽입시 시간복잡도 O(N)의 문제를 Linked List에서는 어떻게 해결하였는가 ?

Linked List에서의 데이터 삽입
- 어떤 위치에 데이터를 삽입하려 하든, 아래 두 과정만 거치면 삽입이 완료될 수 밖에 없음
  - 신규 Node의 data와 next를 지정
  - 직전 Node의 next 대상을 신규 Node로 변경
- 이 과정은 데이터 전체 크기와 상관없으므로, 시간복잡도는 O(1)


Linked List에서의 데이터 삭제
- 어떤 위치에 존재하는 데이터를 삭제하려 하든, 아래의 두 과정만을 거치면 삭제가 완료됨
  - 삭제 대상 직전 Node의 next를 조정
  - 삭제 대상 Node를 실제로 제거
    - 양방향일 경우 양쪽에 대해서 위 과정 진행
- 삭제 대상 직전 Node를 이미 안다는 가정 하에, 시간 복잡도는 O(1)


Linked List의 단점
- Linked List에서의 데이터 접근
  - N개의 Node가 존재하는 Linked List에서 특정 위치의 데이터에 접근하기 위해서는 모든 Node를 돌아야 함
    - 최악의 상황의 시간복잡도는 O(N)

## 양방향 Linked List

![image](https://user-images.githubusercontent.com/109144975/225559268-e2347c54-0219-4cc7-91c1-b934b4cbbdb6.png)

양방향에서의 데이터 삭제
- 다음의 세 과정을 거치면 임의 위치의 데이터를 O(1) 시간복잡도로 삭제 가능
  - 삭제 대상 D 데이터 직전 Node의 next를 삭제 대상 D 다음 Node로 가리키게 함
  - 삭제 대상 D 데이터 직후 Node의 prev를 삭제 대상 D 이전 Node로 가리키게 함
  - 삭제 대상 Node를 실제로 제거


## 클래스와 객체지향

![image](https://user-images.githubusercontent.com/109144975/225560681-698d685d-a5e1-4bbf-bb18-0ad78514431c.png)


클래스학습의 주요 개념

인스턴스
- 클래스로부터 생성되는 각각의 개체
- 후보1, 후보2, 후보3, 등등 개개인이 클래스의 인스턴스가 됨

속성
- 각각의 인스턴스가 가질 수 있는 데이터 값
- 후보자 나이, 성별, 지지율 등

메소드
- 클래스 내에서 정의되고 사용되는 함수, self 키워드 사용


```python
class Candidate :
    region = "서울"

    def __init__(self, name, age, number):
        self.name = name
        self.age = age
        self.number = number
```

region 은 `클래스 속성` = 모든 인스턴스가 공유하는 속성


위 클래스에서 `self.name = name` 의미는 `인스턴스 속성`

`self.name` 에서 해당 객체에 name 공간을 만든다는 것

즉 저 키워드로 인해 속성이 생성되었으므로 name이라는 속성을 사용할 수 있음 

`__init__(self, ...)` 는 생성자
- self를 항상 포함해야함

## Linked List 의 실제적 구현

```python
class Node :

    def __init__(self, data, prev, next):
        self.data = data
        self.prev = prev
        self.next = next

def node_insert(value, position) :
    new_node = Node(value, position, position.next)
    new_node.prev.next = new_node
    new_node.next.prev = new_node

    return new_node

def node_delete(input_node) :
    input_node.prev.next = input_node.next
    input_node.next.prev = input_node.prev

def visit_all(input_node) :
    now_node = input_node
    while(True):
        print(now_node.data)
        now_node = now_node.next

        if (now_node.data) == None:
            break

head = Node(None, None, None)
tail = Node(None, None, None)


head.next = tail
tail.prev = head

### 시험
N1 = node_insert("노드", head)

## tail 뒤에는 못넣음
N2 = node_insert("윤", N1)

N3 = node_insert("수민", head)

node_delete(N2)

visit_all(head)
```

> 결과
> 
> None
> 수민
> 노드
> 
> 마지막에 None이 없는 이유는 node.next 에서 다음 node가 tail이면 data가 None 이므로 break가 print() 이전에 발생하므로