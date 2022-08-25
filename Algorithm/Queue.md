# 큐



## 큐의 특성

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
- 큐의 뒤에서 삽입만 하고, 큐의 앞에서는 삭제만 이루어 지는 구조
- 선입선출구조(FIFO, *first in fist out*)



## 큐의 연산

기본 연산

- 삽입 : enQueue
- 삭제 : deQueue

주요 연산



## 선형 큐

- 1차원 배열을 이용한 큐

  큐의 크기 = 배열의 크기

  front: 저장된 첫번째 원소의 인덱스

  rear : 저장된 마지막 원소의 인덱스

- 상태 표현

  초기 상태: front == rear == 1

  공백 상태: front == rear

  포화 상태: rear == n - 1 ( n: 배열의 크기, n-1: 배열의 마지막 인덱스)

- 문제점

  - 잘못된 포화상태 인식

    :앞에 공간이 있는 경우에도 꽉찼다고 인식

    - 해결 : 매 연산이 이루어 질 때 마다 저장된 원소들을 배열의 앞으로 이동 → 효율성 급감
    - 해결 : 원형 큐의 논리적 구조



**[큐를 클래스로 만든 경우]**

```python
class Queue:
    def __init__(self, size):
        self.size = size
        self.queue = [None] * (size)
        self.front = 0
        self.rear = 0

    def isfull(self):
        return (self.rear + 1) % self.size == self.front

    def isempty(self):
        return self.rear == self.front

    def enqueue(self, item):
        if self.isfull():
            print("Queue is full")               # 이거 없으면 que 사이즈 지정개수만큼 가능
        else:
            self.rear = (self.rear + 1) % self.size
            self.queue[self.rear] = item

    def dequeue(self):
        if self.isempty():
            print("Queue is empty")
        else:
            self.front = (self.front + 1) % self.size
            return self.queue[self.front]
```



## 원형 큐

- 초기 공백 상태

  front = rear = 0

- Index의 순환

  - front 와 rear의 위치가 배열의 마지막 인덱스인 n-1를 가리킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동해야 함
  - 이를 위해 나머지 연산자 mod를 사용함

- front 변수

  공백 상태와 포화 상태 구분을 쉽게 하기 위해

  front가 있는 자리는 사용하지 않고 항상 빈자리로 둠

- 삽입 위치 및 삭제 위치

  |        | 삽입 위치               | 삭제 위치                 |
  | ------ | ----------------------- | ------------------------- |
  | 선형큐 | rear = rear + 1         | front = front + 1         |
  | 원형큐 | rear = (rear + 1) mod n | front = (front + 1) mod n |

```python
class Queue:
    #createQueue
    def __init__(self, n):        #n의 사이즈
        self.size = n
        self.items = [None] * n
        self.front = -1
        self.rear = -1
    
    def enQueue(self, item):        #item: queue에 들어갈 데이터
        if self.isFull():
            print("Queue id full")
        else:
            self.rear += 1
            self.items[self.rear] = item

    def deQueue(self):
        if self.isEmpty():
            print("Queue id empty")
        else:
            self.front += 1
            return self.items[self.front]

    def isEmpty(self):
        # if self.rear == self.front:
        #     return True 
        # else:
        #     return False
        return self.rear == self.front
        

    def isFull(self):
        if self.rear == self.size - 1:
            return True
        else:
            return False

    def Qpeek(self):
        return self.items[self.front]

q = Queue(3)
q.enQueue(1)
q.enQueue(2)
q.enQueue(3)
print(q.items)
print(q.deQueue())
print(q.deQueue())
print(q.deQueue())
```



## 우선순위 큐 (Priority Queue)

- 특성

  - 우선순위를 가진 항목들을 저장하는 큐
  - FIFO 순서가 아니라 우선순위가 높은 순서대로 먼저 나가게 된다.

- 적용 분야

  - 시뮬레이션 시스템
  - 네트워크 트래픽 제어
  - 운영체제의 테스크 스케줄링

- 우선순위 큐의 구현

  1. 배열을 이용해서 구현

     문제점 : 삽입이나 삭제 연산이 일어날 때 원소의 재배치가 발생

     ```
                  → 이에 소요되는 시간이나 메모리 낭비가 크다.
     ```

  2. 리스트를 이용해서 구현



## 큐의 활용 : 버퍼 (Buffer)

:데이터를 한곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역

버퍼링 : 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작을 의미한다.

크기의 제약이 있다.

### 자료 구조

- 일반적으로 입출력 및 네트워크 관련된 기능에서 이용
- 순서대로 입력/출력/전달 되어야 하므로 FIFO방식의 자료구조인 큐가 활용된다.





# BFS(Breadth First Search)

: 탐색 시작점의 인접한 장점들을 먼저 모두 차례로 방문한 후에,

방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식

인접한 정점들에 대해 탐색을 한 후, 차례로 다시 너비우선탐색을 진행해야하므로,

선입선출 형태의 자료구조인 큐를 활용함



### 초기상태

1. visited 배열 초기화
2. Q생성
3. 시작점 enqueue

```python
#미로의 거리(가장 짧은 곳에서 3(도착)찾으면 바로 멈춤)
#짧은 거리
def bfs(N):
    visited = [[0]*N for _ in range(N)]
    queue = []
    cnt = 0
    for i in range(N):
        for j in range(N):
            if nums[i][j] == 2:
                queue.append((i, j))
                visited[i][j] = 1

    while queue:
        i, j = queue.pop(0)
        if nums[i][j] == 3:
            return visited[i][j]
        for di, dj in [[0,1], [1,0], [0,-1], [-1,0]]:
            ni, nj = i + di, j + dj
            if 0 <= ni < N and 0 <= nj < N:
                if nums[ni][nj] != 1 and visited[ni][nj] == 0:
                    queue.append((ni, nj))
                    visited[ni][nj] = visited[i][j] + 1
    return 2

T = int(input())

for t in range(T):
    N = int(input())
    nums = [list(map(int,list(input()))) for _ in range(N)]

    print(f'#{t+1} {bfs(N)-2}')
```

```python
#미로찾기 성공 유1무0
def bfs(N):
    visited = [[0] * N for _ in range(N)]
    queue = []

    for i in range(N):
        for j in range(N):
            if nums[i][j] == 2:
                queue.append((i, j))
                visited[i][j] = 1

    while queue:
        i, j = queue.pop(0)
        if nums[i][j] == 3:
            return 1
        for di, dj in [[0, 1], [1, 0], [0, -1], [-1, 0]]:
            ni, nj = i + di, j + dj
            if 0 <= ni < N and 0 <= nj < N:
                if nums[ni][nj] != 1 and visited[ni][nj] == 0:
                    queue.append((ni, nj))
                    visited[ni][nj] = 1
    return 0

for _ in range(10):
    t = int(input())
    nums = [list(map(int,list(input()))) for _ in range(16)]
    print(f'#{t} {bfs(16)}')
```

```python
#**방향성 없는** 노드의 거리 찾기

def bfs(v,t):
    q = []
    q.append(v)
    visited = [0] * (N)
    visited[v] = 1
    while q:
        v = q.pop(0)
        for w in adjlist[v]:
            if w == t:
                return visited[v]
            if visited[w] == 0:
                q.append(w)
                visited[w] = visited[v] + 1
    return 0

T = int(input())
for t in range(T):
    V, E = map(int, input().split())
    N = V + 1
    adjlist = [[] for _ in range(N)]

    for i in range(E):
        a, b = map(int, input().split())
        adjlist[a].append(b)
        adjlist[b].append(a)                           #양쪽으로 노드 이어줌

    S, G = map(int, input().split())
    print(f'#{t+1} {bfs(S,G)}')
```



### 탐색 방법

- 경로 존재(빠짐없이, 중복없이) : BFS, DFS
- 최단 거리 : BFS, DFS
- 경로의 수 : DFS
- 확산(출발이 여러군데) : BFS