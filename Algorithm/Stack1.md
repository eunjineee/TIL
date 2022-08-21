# 스택

### Srack의 특성

선형구조를 가짐

후입 선출



### 자료구조

: 자료를 선형으로 저장할 저장소

- 배열 사용가능
- 저장소 자체를 스택이라 부르기도 함
- 스택에서 마지막 삽입된 원소의 위치를 top라고 한다



### 스택의 구현

- 연산
  - 삽입: push
  - 삭제: pop
  - 스택 공백 확인 : isEmpty
  - 스택의 top에 있는 원소를 반환하는 연산 : peek



### 스택의 push 알고리즘

: append 메소드를 통해 리스트의 마지막에 데이터를 삽입

```python
def push(item, size):
	global top
	top += 1
	if top == size:
		print('overflow!')
	else:
		stack[top] = item

size = 10
stack = [0] * size
top = -1

push(10,size)
top += 1                   #push(20)
stack[top] = 20 
```



### 스택의 pop 알고리즘

```python
def pop():
	if len(s) == 0:
		# underflow
		return
	else:
		return s.pop(-1)
```

[참고]

```python
def pop():
	global top
	if top == -1:
		print('underflow!')
		return 0
	else:
		top -= 1
		return stack[top+1]

print(pop())

if top > -1:         #pop()
	top -=1
	print(stack[top]) 
##
stacksize = 10
stack = [0] * stacksize
top = -1

top += 1
stack[top] = 1

top += 1
stack[top] = 2

top += 1
temp = stack[top + 1]
print(temp)

temp = stack[top]
top -= 1
print(temp)

stack2 = []
stack2.append(10)
stack2.append(20)
print(stack2.pop())
print(stack2.pop())
```

## 스택의 응용 1 : 괄호검사

## 스택의 응용 2 : function call



# 재귀호출

: 자기 자신을 호출하여 순환 수행되는 것

함수에서 실행해야하는 작업의 특성에 따라 재귀호출방식을 사용하여 함수를 만들면 프로그램의 크기를 줄이고 간단하게 작성

### 💡재귀호출에서 return을 하는 이유

내려오면서 저장되어있던거 버려서 용량 줄이는건지

return의 의미를 모르겠음

### Facrotial 함수

```python
def factorial(n):
	if(n > 1):
		return n *factorial(n-1)
	else:
		return 1

a = 5
print(factorial(a))
```

### 피보나치 함수

```python
def fibo(n):
	if n < 2:
		return n
	else:
		return fibo(n-1) + fibo(n-2)

print(fibo(5))
```



# Memorization

: 컴퓨터 프로그램을 실행할 때 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여 전체적인 실행 속도를 빠르게 하는 기술, **동적 계획법의 핵심이 되는 기술**

```python
def fibo1(n):
	global memo
	if n >= 2 and len(memo) <= n:
		memo.append(fibo1(n-1) + fibo1(n-2))
	return memo[n]

memo = [0,1]

fibo1(5)
#memo를 위한 배열을 할당하고 모두 0으로 초기화 한다
#memo[0]을 0으로 memo[1]는 1로 초기화 한다
```

### 사용 방법/ 이유

```python
def fibo(n):
    if n < 2:
        return n
    else:
        return fibo(n-1) + fibo(n-2)

for i in range(101):
    print(i, fibo(i))    #중복호출 횟수가 많아져서 31부터는 느려짐
    
    
#2 메모이제이션 사용
#시간이 많이 줄어들고 바로 나옴
def fibo(n):
    if memo[n]==-1:
        memo[n] = fibo(n-1) + fibo(n-2)
    return memo[n]

memo = [-1] * 101
memo[0] = 0
memo[1] = 1
for i in range(101):
    print(i, fibo(i))
```



# DP (Dynamic Programming)

: 동적 계획 알고리즘은 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.

먼저 입력 크기가 작은 부분 문제들을 모두 해결한 후 그해들을 이용하여 보다 큰 크기의 부분 문제들을 해결하여, 최종적으로 원래 주어진 입력의 문제를 해결하는 알고리즘이다.

### 피보나치 수 DP적용 알고리즘

```python
def fibo2(n):
    f = [0, 1]

    for i in range(2, n+1):
        f.append(f[i-1] + f[i-2])

    return f[n]
```

### 💡 다시보기

```python
def fibo2(n):
    table[0] = 0
    table[1] = 1

    for i in range(2, n+1):
        table[i] = table[i-1] + table[i-2]
    return

table = [0] * 101
fibo2(100)

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    print(f'#{tc} {table[N]}')
```

### DP구현 방식

memoization을 재귀적 구조에 사용하는 것 보다 반복적 구조로 DP를 구현한 것이 성능 면에서 보다 효율적이다

재귀적 구조는 내부에 시스템 호출 스택을 사용하는 오버헤드가 발생하기 때문이다.



# DFS (깊이우선탐색)

비선형구조인 그래프 구조는 그래프로 표현된 모든 자료를 빠짐없이 검색하는 것이 중요함

### 두 가지 방법

- 깊이 우선 탐색 (DFS, Deptrh First Search)
- 너비 우선 탐색 (BFS, Breadth First Search)

시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회방법

가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용

```python
def dfs(v, N):
    visited = [0] * N   # visited 생성
    stack = [0] * N     # stack 생성
    top = -1
    print(v)
    visited[v] = 1 # 시작점 방문 표시
    while True:
        for w in adjList[v]:
            if visited[w] == 0: # if (v의 인접 정점 중 방문 안 한 정점 w가 있으면)
                top += 1
                stack[top] = v  # push(v)
                v = w           # v <- w (w에 방문)
                print(v) # 방문
                visited[w] = 1  # visited[w] <- true
                break
        else:                   # w가 없으면
            if top != -1:# 스택이 비어있지 않은 경우
                v = stack[top]  # pop
                top -= 1
            else:               # 스택이 비어있으면
                break
```