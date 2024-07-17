# 분산시스템 유일 ID 생성기 설계

1단계 문제 이해 및 설계 범위 확정
- 질의 응답


2단계 개략적 설계안 제시 및 동의 구하기
- 다중마스터 복제
- UUID
- 티켓서버
- 트위터 스노플레이크 접근법

3단계 상세 설계
- 타임스탬프


4단계 마무리


Snow Flake를 공부하며 느낀점

- TimeStamp가 주요한 부분을 차지한다.
- TImeStamp는 결국 기원시간 (Epoch) 으로부터 얼만큼 지났는지에 대한 정보이다.
  - TimeStamp에는 41비트라는 제한된 공간이 주어지고
  - 이 공간에서는 최대 69년까지 표현할 수 있기 때문에
  - 현재의 2024년을 표현하기 위해서는 기원시간 개념이 필요하다.

발표자료

[트위터 Snow Flake](https://docs.google.com/presentation/d/1KLvUoA2LoQoZIfJoPXNDQT9UwLgpsijDcXLadbgHbHE/edit?usp=sharing)