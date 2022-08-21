# 배열2 (Array2)



## 배열 2 : 2차원 배열

### 행 우선 순회

```python
for i in range(n):
	for j in range(m):
		array[i][j]
```

### 열 우선 순회

```python
for j in range(n):
	for i in range(m):
		array[i][j]
```

### 지그재그 순회

```python
for i in range(n):
	for j in range(m):
		array[i][j+(m-1-2*j)*(i%2)]
```

### 전치 행렬

```python
for i in range(n):
	for j in range(m):
		if i < j:		
			arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```



## 비트 연산자

i & (1<<j) : i의 j번째 비트가 1인지 아닌지를 검사

훨씬 짧게 쓸수 있기 때문에 사용함

```python
arr = [1, 2, 3]

n= len(arr)
for i in range(1<<n):
    for j in range(n):
        if i & (1<<j):
            print(arr[j], end=", ")
    print()
print()
```





# 검색



## 이진 검색(Binary search)

: 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법

- 자료가 정렬되어 있어야 함

```python
# 변수 정확하게 알고가기

def binarySearch(a, N, key):
    start = 0
    end = N-1
    while start <= end:
        middle = (start + end) // 2
        if a[middle] == key:
            return True
        elif a[middle] > key:
            end = middle -1
        else:
            start = middle + 1
    return False

binarySearch(0, 50, 48)
```



## 선택 정렬( Selection Sort)

주어진 자료들 중 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식

🚨 버블은 앞으로 오는데 선택은 뒤로감

저장되어 있는 자료부터 k번째로 큰 혹은 작은 원소를 찾는 방법

### 선택 정렬 선택과정

- 정렬 알고리즘을 이용하여 자료 정렬하기
- 원하는 순서에 있는 원소 가져오기





# Plus

### 부분집합 구하는 방법

```python
arr = [7, 2, 5, 3, 4, 3]
N =len(arr)

for i in range(N-1):
	minIdx = I
		for j in range(i+1, N):
			if arr[minIdx] > arr[j]:
				minIdx = j
		arr[minIdx], arr[i] = arr[i], arr[minIdx]
print(arr)
```

[부분집합 구하는 방법 이해하기](https://www.notion.so/b9c4afc1a5c247c48e2fb0447595c6a5)

### 알고리즘에서 중요한 문법

```python
di = [-1, 0, 1, 0], dj = [0, 1, 0, -1]

...

for d in range(4):
    ni = i + di[d]
    nj = j + dj[d]
    if ni가 범위 내, nj가 범위 내:
        결과 += abs(행렬[i][j] - 행렬[ni][nj])
```

### 파이참 사용법(pycharm)

input값 txt로 가져오는 방법

```python
import sys
sys.stdin = open('txt_name')
```

### 행렬 만들기

```python
total = [[0]*10 for _ in range(10)]
a = [x for x in range(1,13)]
```



## 실습 문제

```python
import sys

sys.stdin = open("1210_사다리.txt")

for test_case in range(1, 11):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(100)]
    endX = arr[99].index(2)
    i, j = [99, endX]                       # 도착지점 인덱스 찾아놓기
    while i != 0:                           # i가 0이 아닌동안 진행. 그거까지만 해도 j가 나옴.
        if j-1 >= 0 and arr[i][j-1] == 1:   # 왼쪽 벽을 지정해둠. 그리고 왼쪽에 1이 있을 때
            arr[i][j-1] = 0                 # 현재 자리를 0으로 바꾸고 j 자리를 왼쪽으로 한 칸 옮김.
            j = j - 1
        elif j+1 <= 99 and arr[i][j+1] == 1: # 오른쪽 벽을 정해둠. 그리고 오른쪽에 1이 있을 때
            arr[i][j+1] = 0                  # 현재 자리를 0으로 바꾸고 j의 자리를 오른쪽으로 한 칸 옮김.
            j = j + 1
        else:                                # 그렇지 않은 경우는 현재 자리를 0으로 바꾸고 계속 위로 올라감.
            arr[i-1][j] = 0
            i = i - 1
    print(f'#{test_case} {j}')
```