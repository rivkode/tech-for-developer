# 자료구조

본 내용은

- 유용재 교수님의 [자료구조 6주차](https://www.youtube.com/playlist?list=PLL3t9Nt4HrfsD64K-x1A51Tpjvq74-QDh)

을 정리한 내용입니다.

# 우선순위 Queue와 이진 Tree 의 기초

![image](https://user-images.githubusercontent.com/109144975/230373808-9e8ffa5d-73c3-468d-8404-d8c42b4adfa9.png)

목차
- Graph 와 Tree
- Tree에 대한 구조적 이해
- Heap 과 주요 연산
- Heap의 실제적 구현
- 우선순위 Queue의 이해

## Graph 와 Tree

선형 형태의 자료구조를 통해 다양한 형태의 것들을 효율적으로 나타낼 수 있었지만, 
모든것을 나타낼 수는 없다.

- 이전에 배웠던 Linked List, Stack, Queue 등 선형적 자료구조를 이용하여 모든 상황을 표현하기는 힘듦
- 비 선형적 자료구조에는 어떤 것들이 있나 ?

![image](https://user-images.githubusercontent.com/109144975/230375825-81623731-9a87-4575-8795-1fc8329ca817.png)

![image](https://user-images.githubusercontent.com/109144975/230376058-7a74f0ae-5614-4d7e-8a17-ef10707341d8.png)

- walk 1 : A-C-B-D-C : Open walk
- walk 2 : C-B-D-C : Close walk
- A, C : 서로 인접한 꼭짓점
- A, D : 서로 비 인접한 꼭짓점
- 비연결 그래프란 ? : 연결되지 않는 점이 하나라도 있는 경우

![image](https://user-images.githubusercontent.com/109144975/230376463-07942e4b-746f-4584-8feb-e1cb3f9f79d7.png)

- 위 Graph에 존재하는 cycle의 수는 : 3개
- B-C-D-B
- C-D-E-C
- B-C-E-D-B

![image](https://user-images.githubusercontent.com/109144975/230376463-07942e4b-746f-4584-8feb-e1cb3f9f79d7.png)

- 모든 트리는 그래프이다.

## 우선순위 Queue와 이진 Tree의 기초

![image](https://user-images.githubusercontent.com/109144975/230377006-29c645d6-2b46-4644-bc63-08153115d239.png)

- Root Node : 93
- Leaf Node : 36, 72, 83, 19
- `Leaf Node를 제외`한 모든 Node들을 내부 Node라고 함
- 이진 Tree : 모든 Node가 `최대 2개의 자식 Node`를 가짐

위 Tree에서 Leaf Node의 개수는 : 4개


![image](https://user-images.githubusercontent.com/109144975/230377907-49aa6f63-6ffd-4676-9b66-391504f85fa4.png)

높이 : 가장 깊은 곳의 크기

|높이|1|2|3|...|n|
|-----|-----|-----|---|---|---|
|이진트리 Node 개수|3|7|15|...|2^(n+1) - 1|

Node 깊이 : 거쳐가는 Edge의 개수

node 개수가 777인 포화 이진트리 ? : 존재하지 않음, 777 은 2^(n-1) - 1 이 아니므로

![image](https://user-images.githubusercontent.com/109144975/230379072-23362631-344c-424d-84a7-b8d0be530e11.png)

- 왼쪽 Node를 남김
- `최하단의 모든 node들이 좌측에 몰려 있는 경우` 완전 이진 Tree
- 만약 위 상황에서 node를 추가한다면 75 자리에 무조건 추가해야 한다

> 모든 Perfect 이진 트리는 완전 이진 트리인가 ? : True

![image](https://user-images.githubusercontent.com/109144975/230382639-4cf715f0-30da-4665-83fc-c5494b493345.png)


![image](https://user-images.githubusercontent.com/109144975/230382863-88da98b6-7380-4b22-881a-fb340c2536a5.png)

- ㄱ. N은 무조건 홀수, root node + 2의 배수이므로
- ㄴ. 위 사진에서 설명
- ㄷ. 규칙이 존재
  - 완전 이진트리의 경우 규칙을 지키게 되면 리프토드가 하나 줄어들고 그 다음은 내부 노드가 줄어들게 되면서 특정 법칙이 생긴다
  - 이러한 이유로 인해 리프노드는 내부 노드의 수와 항상 같거나 하나가 더 많다
  - 예를 들어 깊이가 3인 포화 이진트리에서 리프노드를 하나 씩 제외하게 되면 아래와 같이 진행된다

|      | | | |
|------|---|---|---|
| 내부노드 |3|3|2|
| 리프노드 |4|3|3|


![image](https://user-images.githubusercontent.com/109144975/230384463-83448c92-1d13-42c1-8a9f-2a4aebe8cffb.png)

- ㄹ
  - 높이가 3일 경우 최대 가질 수 있는 모서리의 수는 14개(2^(3+1) -2) 이다


## 우선순위 Queue와 이진 Tree 의 기초

![image](https://user-images.githubusercontent.com/109144975/230385024-ab04930d-d6d1-4de9-b5c5-c718c7ce9b47.png)

- 부모님과 나의 관계처럼 "관계" 는 직속 자식만 본다.
- 노드가 추가될 때는 부모 노드와 비교 heap 원리를 깨지 않고 움직임

![image](https://user-images.githubusercontent.com/109144975/230385290-982012e4-7bf3-4a35-a2e6-50fc97da0c87.png)

> - heap 에서의 삽입은 heap 원리(완전 이진 트리) 를 깨지 않아야 하므로 항상 반드시 가장 우측 leaf에 추가된다.
> - 이후에는 부모 node와 비교하여 자식 node가 더 크다면 서로 swap 한다

![image](https://user-images.githubusercontent.com/109144975/230385662-6e811a2c-a6a1-4947-bf94-dfc64605954e.png)

> - heap 에서의 삭제는 항상 반드시 Root node 를 제거하는 것이다
> - Root node를 제거 후 root 자리를 `항상 최하단의 최우측 node로 대체`한다
> - 이후 자식 node들과 비교하며 부모와 자식 관계를 유지시키는 방향으로 swap 한다

![image](https://user-images.githubusercontent.com/109144975/230386243-1ea7164a-d169-44d1-9786-f6aaeead78d4.png)

9

## 우선순의 Queue와 이진 Tree의 기초

![image](https://user-images.githubusercontent.com/109144975/230386879-ea48ca5c-5bdd-436a-be9c-c0dfc59edaab.png)

> Heap은 완전 이진트리 이므로 각 node들에 대해 index를 매길 수 있음
> 
> 즉 배치 순서가 명확하므로 Heap을 동적 리스트로 구현이 가능함

```python
class maxHeap():

    def __init__(self): # 생성자
        self.data = list()

    def push(self, value): # 새로운 원소를 삽입하는 push
        self.data.append(value)
        now_index = len(self.data) - 1
        while(True): # 부모노드와 비교하며 자식노드가 부모 노드보다 크면 바꿔줌
            parent_index = (now_index - 1) // 2 # 부모 인덱스
            if (parent_index < 0):
                break
            if (self.data[now_index] <= self.data[parent_index]):
                break
            else: # 자식 node 가 부모 node보다 클 경우에만 swap
                self.data[now_index], self.data[parent_index] = self.data[parent_index], self.data[now_index]

    def pop(self): # Root Node를 제거하는 Pop
        now_index = len(self.data) - 1
        self.data[0] = self.data[now_index] # 최하단, 최우측의 node를 Root로 변경
        del self.data[now_index] # 기존 Root node 제거
        now_index = 0 # index 0으로 초기화

        while(True): # 자식 node 들과 비교하며 부모노드가 더 작을 경우 더 큰 자식노드와 바꿔줌
            left_child_index = now_index * 2 + 1
            right_child_index = now_index * 2 + 2
            if left_child_index >= len(self.data):
                break
            if (self.data[now_index] >= self.data[left_child_index]) and (self.data[now_index] >= self.data[right_child_index]):
                break
            else:
                if (self.data[left_child_index] > self.data[right_child_index]):
                    self.data[now_index], self.data[left_child_index] = self.data[left_child_index], self.data[now_index]
                    now_index = left_child_index
                else:
                    self.data[now_index], self.data[right_child_index] = self.data[right_child_index], self.data[now_index]
                    now_index = right_child_index
                    

```

## 우선순위 Queue와 이진 Tree 의 기초

![image](https://user-images.githubusercontent.com/109144975/230398300-e0705e0e-b9de-481f-8956-f106800f4446.png)

![image](https://user-images.githubusercontent.com/109144975/230398756-62b6e04b-64d2-49d9-9c39-dca3f4782f4a.png)

- Heap 자료구조를 통해 삽입, 삭제를 하면 됨

![image](https://user-images.githubusercontent.com/109144975/230399288-fec6cac5-df2a-48db-b0f1-26b0fd90bb08.png)

> "일반 큐에서 삽입(push)은 O(1)의 시간복잡도가 걸리지만 삭제에서 모든 인덱스를 -1씩 해줘야 하므로 O(n)의 시간복잡도가 걸린다." 라고 알고있었다.
> 
> 여기서 Heap 자료구조를 사용하게 되면 삽입과 삭제가 모두 log(n)의 시간복잡도가 소요되어 1억번, 1조번을 계산한다고 가정하였을때 그 차이가 매우 크기 때문이다.
>
> Heap에서 "swap시 아무리 많아도 높이(깊이) 만큼만 swap 함" -> 이 이유때문에 삽입, 삭제시 log(n) 의 시간복잡도가 소요되는 것으로 알고있으며 이 "높이(깊이)" 를 swap하여 계산하는 시간보다 일반 큐에서 삭제 시 모든 인덱스를 돌며 -1을 해주는 시간이 더 "많기" 때문에 Heap 자료구조가 더 좋은 삽입 삭제시 더 효율적인 자료구조다.
>
> 라고 생각하였지만 무조건적으로 이렇게 생각할 수는 없다.
> 
> 일단, Queue와 우선순위 Queue는 별개의 자료구조임에 유의해야 한다.
> 
> Queue는 '먼저 들어온' 원소가 먼저 나가지만, 우선순위 Queue는 '순위가 높은' 원소가 먼저 나가기 때문이다.
> 
> 나는 'Queue에서의 삭제보다 Heap에서의 삭제가 빠르므로 Heap이 더 우월한 자료구조다'는 단편적인 사고방식에 빠져있었다.
> 
> 하지만 앞서 말한 대로 Queue와 우선순위 Queue는 아예 존재 목적부터가 상이한 자료구조이다.
> 
> 또한, Queue에서의 삭제는 '최장 대기 원소'가 지워지는 것이지만 우선순위 Queue에서의 삭제는 '최고 순위 원소'가 지워지는 것이다.
> 
> 즉, 두 자료구조에서 '삭제'가 의미하는 바 자체가 아예 다르므로 Queue와 Heap을 동일 선상에 두고 무엇이 더 좋은 자료구조인지 논하기는 어렵다.
> 
> 다만, 우선순위 Queue 구현이라는 동일한 목표에서 동적 배열보다 Heap이 더 낫다는 의미로 교수님께서 말해주신 것이었다.
> 
> 우선순위 Queue를 기왕 구현할 것이라면, O(n)이 소요될 우려가 있는 동적 배열보다는 항상 O(logn)으로 안정적인 Heap이 더 우월하다고 할 수 있을 것이기 때문이다.
