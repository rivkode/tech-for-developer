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

여기서의 핵심은 모든 Node에 대해서 