# 자료구조

본 내용은

- 유용재 교수님의 [자료구조 7주차](https://www.youtube.com/playlist?list=PLL3t9Nt4HrfsD64K-x1A51Tpjvq74-QDh)

을 정리한 내용입니다.

# 이진 Tree의 구현과 데이터 순회

![image](https://user-images.githubusercontent.com/109144975/231692027-31b8e906-3b54-478e-b398-03a11eb0782c.png)

목차
- 이진 Tree의 구현 원리
- 레벨 순회와 너비 우선 탐색
- 이진 Tree의 재귀적 순회
- 이진 탐색 Tree의 뜻
- 이진 탐색 Tree에서의 연산

## 이진 Tree의 구현 원리

![image](https://user-images.githubusercontent.com/109144975/231692459-510e7edc-6bce-4dea-a8c2-30a1eff91beb.png)

자식 노드에 기초한 이진 Tree의 구현

```python
class BinaryTreeNode :
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
```

![image](https://user-images.githubusercontent.com/109144975/231692846-c0eb0529-9113-4025-a5dc-552da3a09f53.png)

- O(N) 시간 복잡도가 소요
- 자식관계를 직접 정의해준다. "선의 개수"만큼
- 부모노드에서 자식 노드를 물어봐야 하기 때문

## 레벨 순회와 너비 우선 탐색

level-order Traversal

![image](https://user-images.githubusercontent.com/109144975/231693506-3a97c642-2bd2-4ac5-b3d7-d54923bfe2e5.png)

레벨 순회 : 깊이를 기준으로 노드들을 차례로 방문

![image](https://user-images.githubusercontent.com/109144975/231693868-2ae1c08c-592f-4ecf-9f9b-871cba204076.png)

> 큐(queue) 자료구조를 사용하여 구현

- 93 출력 / 15, 19 입력 / 93 제거
- 15, 19 출력 / 36, 44 입력 / 15, 19 제거
- 36, 44 출력 / 72, 83 입력 / 36, 44 제거
- 72, 83 출력 / 없음 / 없음

```python
def level_order(root_node) :
    queue = list()
    queue.append(root_node)
    while(True) :
        if len(queue) == 0:
            break
        print(queue[0])
        if (queue[0].left != None) :
            queue.append(queue[0].left)
        if (queue[0].right != None) :
            queue.append(queue[0].right)
        del queue[0]
```

![image](https://user-images.githubusercontent.com/109144975/231696330-022b464d-ae13-4211-aa34-bfb4b85e5e7a.png)

너비 우선 탐색(BFS)
- 노드의 깊이 순서대로 모든 동일한 레벨의 노드들을 다 돌고 난 후 다음 깊이의 노드로 방문한다
- Queue를 이용하여 구현
- 들어간 순서대로 호출되므로


깊이 우선 탐색(DFS)
- 노드의 가장 깊은 곳들을 먼저 순회
- 해당 노드의 자식들이 없을때 까지
- 이후 순차적으로 재귀를 빠져나옴
- 재귀를 빠져나오는 방식이 스택구조를 띔
- 재귀를 이용하여 구현
- 가장 깊은곳의 의미
  - 루트 노드가 생성될때 연관된 가장 깊은 깊이를 찾는 것
  - 가장 깊은 노드를 찾기 위해서 재귀(스택)를 사용하여 찾음
  - 재귀는 결국 자기 자신을 호출하는 것이므로 상위로 호출된 함수를 탈출하기 위해서는 해당 하위 함수들에서 모두 탈출을 해야 가능


## 이진 Tree의 구현과 데이터 순회

![image](https://user-images.githubusercontent.com/109144975/231696756-ac826dc0-66f9-454a-a872-b003255e1ee5.png)


SubTree란 자식 node 아래의 형태가 트리 구조를 가질 경우 각각 왼쪽, 오른쪽 subTree라고 정의

아래 3가지는 결국 루트를 어디 두느냐가 포인트


> - 전위 순회(Pre_order) : Root Node > 왼쪽 SubTree > 오른쪽 SubTree
> - 중위 순회(In_order) : 왼쪽 SubTree > Root Node > 오른쪽 SubTree
> - 후위 순회(Post_order) : 왼쪽 SubTree > 오른쪽 SubTree > Root Node

전위 순회의 경우

> Root Node > 왼쪽 SubTree > 오른쪽 SubTree

- Root Node를 먼저 출력
- 왼쪽 자식을 탐색 (가장 깊은곳 까지, 탐색하면서 해당되는 Root node들 출력)
- 자식이 없으면 그때 재귀함수 순차적으로 탈출
  - 이때 오른쪽 자식들을 탐색
- 최초 Root Node 왼쪽 subTree가 끝나면 오른쪽 SubTree 동일하게 탐색 시작

중위 순회의 경우

> 왼쪽 SubTree > Root Node > 오른쪽 SubTree

- 왼쪽 SubTree 최하단까지 먼저 탐색
- 왼쪽 최하단 Node를 출력
- 재귀 탈출시 해당되는 RootNode 출력
- 모든 재귀 탈출시 최초 Root Node를 만났을 경우 그제서야 Root Node 출력
- 이후 오른쪽 SubTree 동일하게 탐색 시작


후위 순회의 경우

> 왼쪽 SubTree > 오른쪽 SubTree > Root Node

- 왼쪽 SubTree 최하단까지 먼저 탐색
- 왼쪽 최하단 Node를 출력
- 모든 재귀 탈출시 해당 Node 출력하지 않고 왼쪽 SubTree 부터 먼저 탐색
- 모든 하위 Node 탐색 완료 및 재귀 탈출 시 해당 Root Node 출력
- 이후 동일하게 오른쪽 SubTree 탐색 시작


전위 순회(Pre_order)

```python
def pre_order(node):
  print(node.data)
  if (node.left) != None :
    pre_order(node.left)
  if (node.right) != None :
    pre_order(node.right)
```

중위 순회(In_order)

```python
def In_order(node):
  if (node.left) != None :
    pre_order(node.left)
  print(node.data)
  if (node.right) != None :
    pre_order(node.right)
```

후위 순회(Post_order)

```python
def In_order(node):
  if (node.left) != None :
    pre_order(node.left)
  if (node.right) != None :
    pre_order(node.right)
  print(node.data)
```

## 이진 Tree의 구현과 데이터 순회

![image](https://user-images.githubusercontent.com/109144975/231707707-2b3fe5ec-27d5-4dba-afa9-21dc34c665d8.png)

이진 탐색은 원하는 값을 탐색 시 사용

![image](https://user-images.githubusercontent.com/109144975/231707778-a5d8d976-5826-4282-99db-84819e7734ef.png)

- 이진 탐색은 중복허용을 하지않음
- 왼쪽, 오른쪽 값의 대소관계가 분명함
- 완전 이진트리 형태가 아니어도 됨

| 종류 \ 트리    |이진 탐색 Tree|Heap|
|------------|------|-----|
| 값, data    | 중복 허용하지 않음 |중복 허용|
| 자식 간 대소 관계 | 대소 관계가 아주 명확|대소 관계 관련 없음|
| 트리 형태      |이진 Tree|완전 이진 Tree|


## 이진 Tree의 구현과 데이터 순회

![image](https://user-images.githubusercontent.com/109144975/231709589-1abf230a-20dc-452b-b8ee-17c4f30aabd3.png)


![image](https://user-images.githubusercontent.com/109144975/231709675-563538cb-e790-4de7-b9d1-90e566b699b2.png)

- 자식 없음 : 바로 제거
- 좌측 자식만 있음 : 해당 SubTree의 가장 최대값이 자리 대체 (남은 트리는 좌측만 존재하므로 가장 Root Node는 남은 Tree의 값보다 가장 커야 하기 때문)
- 우측 자식만 있음 : 해당 SubTree의 가장 최소값이 자리 대체 (남은 트리는 우측만 존재하므로 가장 Root Node는 남은 Tree의 값보다 가장 작아야 하기 때문)
- 모두 있음 : 좌측 자식이 있을 경우의 대체값 혹은 우측 자식이 있을 경우의 대체값 둘 중 어느 하나의 값 (둘 중 선택)

