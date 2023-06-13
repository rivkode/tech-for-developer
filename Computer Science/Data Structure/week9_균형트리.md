# 자료구조

본 내용은

- 유용재 교수님의 [자료구조 9주차](https://www.youtube.com/playlist?list=PLL3t9Nt4HrfsD64K-x1A51Tpjvq74-QDh)

을 정리한 내용입니다.

# 균형을 고려한 여러가지 Tree

목차

- 이진 탐색 Tree와 균형
- AVL Tree의 균형 유지 전략
- AVL Tree에서의 연산
- Red-Black Tree의 이해
- Red-Black Tree 에서의 삽입

## 이진 탐색 Tree와 균형

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/d939f7e2-7fc2-4f03-9587-a80d067a0965)

이진탐색 Tree는 이름에서도 알 수 있듯이 탐색을 위한 자료구조 입니다

여기서 삽입과 삭제를 수행하려면 어떻게 해야할까요 ?

삽입
- 항상 Root Node에서 출발하여 삽입하려는 값과 현재 Node를 반복해서 비교해야 합니다

삭제
- 삭제하려는 값까지 탐색하며 도달하였을때 좌측 SubTree의 최댓값 혹은 우측 SubTree의 최솟값과 바꿉니다
- 왜냐하면 부모 Node는 좌측, 우측의 SubTree를 나누는 기준이 되어야 하므로 좌측값 보다는 항상 커야하고, 우측값 보다는 항상 작아야 하기 때문입니다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/a3747e3c-335a-4079-9400-99f0f64883cb)

하지만 이진 탐색 트리에서 위와 같을 경우 삽입, 삭제, 탐색에 드는 시간 복잡도가 O(N)이 되게 됩니다

그 이유는 균형잡힌 이진 트리가 아니기 때문입니다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/7b234308-f47c-4e14-bdd8-c85a432444b0)


위 사례를 통해 이진 탐색 트리에서의 **"균형"** 은 매우 중요하다는 사실을 알 수 있습니다

이 균형은 AVL, RED-BLACK 알고리즘으로 해결할 수 있습니다

## AVL Tree의 균형 유지 전략

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/95469610-6e1f-4d08-be78-dbcbe1f81fd3)

Balance Factor
- 임의의 Node에 대하여, 다음을 Balance Factor로 정의합니다
  - (좌측 Subtree의 높이 - 우측 Subtree의 높이)

54가 가리키는 Node의 Balance Factor 값은
- -1 이 됩니다 (0-1)

각 Node의 Balance Factor 값은 이진 탐색 트리 균형의 중요한 기준이 됩니다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/d4b4e43f-a5a1-4452-bb75-611d99cba4ed)

AVL Tree란
- 이진 탐색 Tree의 성질을 충족함과 동시에 모든 Node의 Balance Factor 절댓값(이하 Balance Factor 값)이 1 이하인 경우를 의미합니다

그렇다면 Balance Factor 의 값이 1이 초과된다면?
- 해당 Node로 인해 트리의 균형이 무너졌다고 판단하여 Tree 구조를 모든 Node에 대해 Balance Factor 값이 1이 되도록 변경합니다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/245f928b-3f30-4c58-9453-7a4962bda907)

위와 같이 92를 삽입할 경우
- 45 Node의 Balance Factor 값이 2가 되어 균형이 무너짐

21을 삭제할 경우
- 28 Node의 Balance Factor 값이 2가 되어 균형이 무너짐

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/045d2828-ae1f-40c3-b16d-b1ff5112e909)

기존의 AVL 트리 형태가 유지 되던 중 균형을 무너지게 하는 원인은 위 4가지 형태가 될 수 있습니다

위 4가지의 형태가 Balance Factor의 값이 2가 되게 하는 원인이기 때문입니다


![image](https://github.com/rivkode/tech-for-developer/assets/109144975/a1ec51f6-12e1-4404-9a6d-a00ad9383287)

이에 대한 해결 방안은 위와 같습니다

여기서의 핵심은
- 각 형태에 대해서 규칙이 존재하며 부모 Node가 되는 Node를 빨리 찾아서 트리형태를 만들어 주는 것입니다

## AVL Tree에서의 연산

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/d83049f0-08c2-4362-b9a6-c37f98550007)

AVL Tree 에서의 Node 삽입도 마찬가지로 매 Node가 추가 될 때마다 Balance Factor의 값이 1을 넘는 Node가 존재하는지 추적해나가며

만약 균형이 무너지는 부분이 발생할 경우 **해당하는 지점을 찾아** 균형화를 진행합니다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/99beaf7a-bbf4-47b8-b91d-26ce268dda80)

AVL Tree 에서의 Node 삭제도 삽입과 마찬가지로 Balance Factor값을 추적해나가며 균형화를 진행합니다

## Red-Black Tree의 이해

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/ebf287d3-9005-46ca-af8d-9491811aeb1d)

일반적인 이진 Tree 의 형태를 가지며 모든 Node는 리프 Node를 가지며 이를 NIL이라 부릅니다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/4cc25d4d-4b85-4f73-b02e-44b2ca333086)

이진 탐색 Tree 이며 모든 Node는 Red 이거나 Black 색상을 가지며 아래 성질을 반드시 만족해야 합니다

- Root Node 와 NIL은 모두 Black 이여야 합니다
- Root Node에서 임의의 NIL 까지 경로에서 RED Node는 연속해서 존재할 수 없습니다
- Root Node에서 임의의 NIL 까지 경로에서 Black Node의 수는 동일해야 합니다 (NIL 도 포함)


## Red-Black Tree에서의 삽입, 삭제

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/1deacf8f-9691-45d9-b494-f4689af51311)

Recoloring 은
- 삽입을 시도한 Node 의 부모 Node 와 삼촌 Node가 **모두 Red 인 경우** Node의 색상을 재배색 함으로써 Red-Black Tree의 성질을 유지하는 것을 의미합니다

Recoloring 방법은
- 부모 Node와 삼촌 Node를 **Black 색상**으로 변경하며 조부모 Node의 색상을 **Red 색상**으로 변경함으로써 Black 의 수를 동일하게 가져가는 것을 목표로 합니다

예외인 경우
- 조부모가 Root Node인 경우 Black 을 유지
- 재배색으로 인하여 Red가 연속으로 발생할 경우 재배치(Restructuring) 및 재배색(Recoloring)


![image](https://github.com/rivkode/tech-for-developer/assets/109144975/e0efef12-0706-462d-9d9b-9dc945516cfd)

Restructuring 은
- 삽입을 시도한 Node의 부모 Node는 Red 색상이나 삼촌 Node가 Black인 경우
  - 위 사진에서는 7 Node의 오른쪽 자식이 NIL으로 Black 색상이므로 3 Node의 삼촌 Node가 Black이라 할 수 있다

Restructuring 방법은
- 해당 묶음을 균형화 한 후 자식 Node는 Red로 배색, 부모 Node는 Black으로 배색하여 재배치 한다

![image](https://github.com/rivkode/tech-for-developer/assets/109144975/d05d477a-f28d-48bf-9f06-b2e4d5897f8a)

2, 1, 8, 9, 7, 3, 6을 순서대로 삽입하여 Red-Black Tree를 구성할 경우 위와 같이 나타낼 수 있다
