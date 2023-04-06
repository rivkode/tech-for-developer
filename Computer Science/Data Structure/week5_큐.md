# 자료구조

본 내용은

- 유용재 교수님의 [자료구조 5주차](https://www.youtube.com/playlist?list=PLL3t9Nt4HrfsD64K-x1A51Tpjvq74-QDh)

을 정리한 내용입니다.

# Queue 와 환형 Queue의 이해

![image](https://user-images.githubusercontent.com/109144975/230365324-04d9ec10-1a7c-496a-b6ac-d47504735568.png)


목차
- Queue의 뜻과 특징
- 환형 Queue와 그 의의
- 환형 Queue의 실제적 구현
- Deque의 이해
- 선형적 자료구조의 한계

## Queue의 뜻과 특징

![image](https://user-images.githubusercontent.com/109144975/230365571-560188b5-3efd-4e6b-96e2-279b453c182d.png)

![image](https://user-images.githubusercontent.com/109144975/230365663-09b6f11d-e0d6-40b7-819e-21a2715220c1.png)

![image](https://user-images.githubusercontent.com/109144975/230365708-f12b04b0-5988-4a34-bcc5-16732b850a84.png)

- 3회


```python
queue = list() # 비어있는 리스트를 생성함으로써 빈 Queue에서 출발

queue.append(7) # append를 이용하여 리스트의 맨 끝에 원소를 삽입

del queue[0] # 최전방 원소는 최좌측에 있으므로 가장 첫 원소를 제거

queue[0] # 순서상 맨 끝 원소가 아닌, 가장 첫 원소임에 주목
```

## 환형 Queue와 그 의의

![image](https://user-images.githubusercontent.com/109144975/230366292-54707d8d-3fbf-4f16-a55c-c3535e1cead8.png)

- O(n) 시간 복잡도의 의미는 임의 위치 삽입때 최악의 경우 모든 요소들을 옮겨야 하기 때문이다. 

![image](https://user-images.githubusercontent.com/109144975/230366734-538953eb-dca2-470d-87ad-fdefc129849e.png)

어떤 요소들에 주목해야할까 ?

front
- 주어진 환형 Queue의 최전방 원소와 함께 움직임

rear
- 주어진 환형 Queue의 최후방 원소와 함께 움직임

> Q enqueue를 수행할 경우 front와 rear중 무엇이 움직이는가 ?
> 
> A rear가 움직임

![image](https://user-images.githubusercontent.com/109144975/230367075-4741e969-94fb-4f09-8e43-fe7ac4e8b0ed.png)

- O(1), 왜냐하면 rear 위치에 데이터를 삽입할 경우 해당 위치를 찾는데에는 O(1) 시간이 걸리며 rear를 한칸만 뒤로 증가시키면 되므로

![image](https://user-images.githubusercontent.com/109144975/230367661-468d119b-83d5-4e57-9114-0774ea768cd2.png)

- O(1), 제거를 할 경우에도 일반 Queue와 달리 value 제거 후 front 위치만 +1 시켜주면 되기 때문


![image](https://user-images.githubusercontent.com/109144975/230368839-855d8d8e-d113-4eac-aeaa-3feac0c0a5d2.png)
- 1번, 환형 Queue이므로 원소 F 를 마지막에 삽입 시 인덱스 5에서 인덱스 6이 아닌(애초에 없음) 그 다음 인덱스인 0 위치에 삽입된다.


![image](https://user-images.githubusercontent.com/109144975/230369780-03bb1d5b-1977-4507-88dc-5aeb39846826.png)

```python
class CQueue:
    def __init__(self, size):
        self.size = size
        self.front = 0
        self.rear = 0
        self.data_list = list()
        for i in range(0, size):
            self.data_list.append(None)

    def enqueue(self, data):
        if (self.rear + 1 - self.front) % self.size == 0:
            print("QUEUE FULL") # 꽉 찬 Queue에는 데이터를 삽입할 수 없음
        else:
            self.data_list[self.rear] = data
            self.rear = (self.rear + 1) % self.size

    def dequeue(self):
        if (self.front == self.rear):
            print("QUEUE EMPTY") # 비어있는 Queue에서 데이터를 제거할 수는 없음
        else:
            self.data_list[self.front] = None
            self.front = (self.front + 1) % self.size
```

## Queue와 환형 Queue의 이해

![image](https://user-images.githubusercontent.com/109144975/230372487-90df68b0-3a43-4c83-8c77-4edff55ba4d1.png)

![image](https://user-images.githubusercontent.com/109144975/230372553-6c39e25c-7b3a-4267-b0ac-9eed26f51ce3.png)

Python에서 가장 빠르게 Deque를 활용할 수 있는 방법은 ?

```python
from collections import deque

a = deque()
b = deque()

a.append(9)
a.append(8)
a.pop()

b.append(5)
b.appendleft(3)
b.popleft()

print(a)
print(b)

# list에서 append와 pop이 모두 오른쪽 끝을 기준으로 이루어졌다는 점에 주목
```

## Queue와 환형QUeue의 이해

선형적 자료구조의 한계

수 많은 곳에서 강력한 힘을 발휘하는 선형적 자료구조, 그러나 아직까지 보이는 한계

stack : 컴퓨터 함수 호출 및 프로그램 실행 등
queue : cpu 스케줄링 등

한계
- 인사체계 등을 선형적 자료구조로 나타내면 ?
- 출발역과 도착역 사이 연결 여부 등이 잘 들어나는 지하철 노선도를 표현한다면 ? 

