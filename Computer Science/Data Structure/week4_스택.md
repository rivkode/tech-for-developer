# 자료구조

본 내용은

- 유용재 교수님의 [자료구조 4주차](https://www.youtube.com/watch?v=B1ZSqOtRwQ0&list=PLL3t9Nt4HrfsD64K-x1A51Tpjvq74-QDh&index=3)

을 정리한 내용입니다.

# Stack 자료구조의 이해와 응용

![image](https://user-images.githubusercontent.com/109144975/229331347-c8ee5709-b082-487c-8d2c-6ae42fbaddc7.png)


목차
- 원형 Linked List의 이해
- Stack의 뜻과 특징
- 재귀 호출과 Stack
- Stack의 실제적 구현
- Stack을 활용한 문제 해결
- 스택에 대한 구현


연결형 자료구조인 Linked List, 내재하고 있는 문제점이 있었는데 ?

- 데이터 삭제를 시도하는 경우, 삭제 대상 바로 앞 Node가 무엇인지 알아내야 함
- 하지만 단방향 Linked List의 경우 prev 가 없으므로, 바로 앞 Node를 직접 알아내야 함
- 보이는 순서대로 순회할 경우 기대 이하의 시간복잡도를 가짐


![image](https://user-images.githubusercontent.com/109144975/229331410-30c530ab-b30c-45c5-ae51-c93ecf4e09c7.png)


- Last가 없고 원형으로만 이어져 있다면 어떠한 기준이 없으므로 해당 링크드 리스트의 head, tail을 알 수 없음
- 반면 Last는 head를 알기 쉬움(last의 next = head)
- 하지만 head는 last를 알기 위해서는 모든 Node를 돌아야 함


![image](https://user-images.githubusercontent.com/109144975/229331698-1d90ab0d-f539-4efa-a593-ac1b51c3af62.png)

Stack의 뜻과 특징

책이 수도 없이 많이 쌓여 있을 때..

어떻게 정리할 수 있을까 ?

- 책을 새로 쌓든, 있는 책을 빼든 반드시 책이 쌓인 곳의 최상단에서 작업이 이루어짐
- Last In First Out - 가장 마지막에 쌓인 책이 가장 먼저 빠져나온다

![image](https://user-images.githubusercontent.com/109144975/229331750-cebd2228-5fae-4122-a29c-510887e95c90.png)

<br>

![image](https://user-images.githubusercontent.com/109144975/229331765-5b59e7e9-e04e-4b27-84d4-f60237b7e570.png)

- 2회

- Stack은 마지막으로 들어온 원소가 먼저 나가는 LIFO의 특징을 지님
- 이를 이용하면, 주어진 데이터 열을 원래 순서와 반대로 순회할 수 있음
  - push 반복 - pop 반복


![image](https://user-images.githubusercontent.com/109144975/229331823-2646e1f4-c530-4be8-8d0d-e7d7bdebb6ed.png)

- 2번


![image](https://user-images.githubusercontent.com/109144975/229331849-bd1052d7-b86b-4c18-9007-b16c3403f03c.png)


![image](https://user-images.githubusercontent.com/109144975/229331863-1f869616-b34f-4629-bd1a-12b97b755b72.png)

recursion
- 자기자신을 호출하는 것


**재귀호출을 이용한 문제 해결의 사례**

- 자연수를 인자로 받아 factorial을 계산하는 함수를 재귀적을 정의하면 ?

```python
def fact_func(n):
    if (n ==1):
        return 1
    else:
        return n * fact_func(n-1)

print(fact_func(5))
```


**재귀호출을 이용한 문제 해결의 사례**

- 자연수 n에 대하여, n번째 피보나치 수를 반환하는 함수를 재귀적으로 정의하면 ?

```python
def fibo_func(n):
    if (n == 1) or (n == 2):
        return 1
    else:
        fibo_func(n-1) + fibo_func(n-2)

fibo_func(10)
```

![image](https://user-images.githubusercontent.com/109144975/229331941-cbf7772f-a6e3-4db8-8a50-1c03ce32a5c9.png)

컴퓨터의 관점에서 함수가 실행되고 결과값이 반환되고 종료되는 일련의 과정들이 stack의 자료구조와 유사한 특징을 지닌다고 말할 수 있음


![image](https://user-images.githubusercontent.com/109144975/229332053-49033e91-ca43-4f04-acb8-40f33c4d1ae1.png)

위 과정을 Stack 차원에서 접근해본다면 ?

![image](https://user-images.githubusercontent.com/109144975/229867598-c23d2b41-d95e-4f9f-a6ce-776d7990af2c.png)


![image](https://user-images.githubusercontent.com/109144975/229867876-e570d0c5-d0ca-4970-b5d6-64c640d8b09c.png)



![image](https://user-images.githubusercontent.com/109144975/229818558-a962f9a8-ea06-480a-9d28-5413c2c6fdde.png)

prev 와 next가 필요했던 Linked List..

Stack은 더 단순하게 갈 수 없을까 ?

```python

# 동적 배열을 활용한 Python에서의 stack 생성
stack = list()

# stack에 새로운 원소를 push
stack.append(3)

# stack의 최상단 원소를 pop
stack.pop()

# stack의 최상단 원소를 peek
stack[-1]

```


![image](https://user-images.githubusercontent.com/109144975/229819280-e2f97132-5f0a-48aa-a379-8d67cfde1f82.png)


![image](https://user-images.githubusercontent.com/109144975/229819612-57f99560-c61b-4553-bb53-3b0151c4699b.png)

![image](https://user-images.githubusercontent.com/109144975/229819677-3e632687-9e0b-4ee2-8274-4d67acf2c8d3.png)



![image](https://user-images.githubusercontent.com/109144975/229819815-6528cee4-9990-4120-bc3f-104640bb82dc.png)

- (9-7) * (1+3) = 2 * 4 = 8


![image](https://user-images.githubusercontent.com/109144975/229819893-27a39105-1d92-47c7-89ef-e2939fe1b56b.png)

> 숫자의 연산은 두 수에서만 일어나므로 수가 입력될 경우 stack에 push 연산자를 만난 경우
> 
> 두개의 수를 pop 하여 연산 후 결과를 다시 push


## 스택에 대한 구현

---

스택이란 ?

스택은 가장 뒤에 들어온 것이 가장 먼저 나가는 자료구조이다. 접시 쌓고 빼는 것, 파워포인트, 엑셀 등 모든 편집기는 최근 작업순으로 취소하는 기능
등을 예로 들 수 있다.

스택은 맨 위의 원소만 접근 가능한 것이 특징이다. 맨 위의 원소를 스택 탑이라 한다. 원소 삭제시에는 탑 원소를 삭제후 그 아래 원소가 새 스택 탑이
되게 한다.

### 메소드 종류

__stack[] - 스택의 원소들이 저장되는 리스트

push(x) - 스택의 맨 우에 원소 x를 삽입한다.
pop() - 스택의 맨 위에 있는 원소를 알려주고 삭제한다.
top() - 스택의 맨 위에 있는 원소를 알려준다.
isEmpty() - 스택이 비었는지 알려준다.
popAll() - 스택을 청소한다.

### 원소 삽입

스택에 새 원소를 삽입할 때는 스택 탑 바로 윗자리에 원소를 저장한다. 리스트에서는 맨 끝 원소 다음에 원소를 삽입하면 된다.

-> append() 리스트의 맨 끝에 원소를 추가하는 메서드

```python
def push(self, x):
    self.__stack.append(x)
```

### 원소 삭제

스택에 있는 원소를 삭제할 때는 무조건 탑에 있는 원소를 삭제한다.

```python
def pop(self):
    return self.__stack.pop()
```

### 기타 작업

-> top() , 탑 원소 알려주기

```python
def top(self):
    if self.isEmpty():
        return None
    else:
        return self.__stack[-1]
```

-> isEmpty(), 값이 비었는지 확인

```python
-> isEmpty(self) -> bool:
return not bool(self.__stack)
```

-> popAll(), 스택 비우기

```python
def popAll(self):
    self.__stack = []
```

