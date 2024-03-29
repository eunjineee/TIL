# 배열 1(Array 1)



## 알고리즘

어떠한 문제를 해결하기 위한 절차

### 무엇이 좋은 알고리즘인가?

1. 정확성 : 얼마나 정확하게 동작하는가
2. 작업량 : 얼마나 적은 연산으로 원하는 결과를 얻어내는가
3. 메모리 사용량 : 얼마나 적은 메모리를 사용하는가
4. 단순성 : 얼마나 단순한가
5. 최적성 : 더 이상 개선할 여지없이 최적화되었는가?

### 알고리즘 성능 측정

- 시간복잡도



## 배열

일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조





# 정렬

2개 이상의 자료를 특정 기준에 의해 작은 값부터 큰 값(오름차순 : ascending), 혹은 그 반대의 순서대로(내림차순: descending) 재배열하는 것



## 버블 정렬 (Bubble Sort)

**인접한 두 개의 원소를 비교하며 자리를 계속 교환하는 방식**

- **정렬과정**

  첫 번째 원소부터 인접한 원소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동

  한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬됨

  교환하며 자리를 이동하는 모습 = 물 위로 거품이 올라오는 모습 = 버블 정렬

```python
def BubbleSort(a,N)            #오름차순
	for i in range(N-1, 0, -1)
		for j in range(0, i):
			if a[j] > a[J+1]:
				a[j]. a[j+1] = a[j+1], a[j]
```



## 카운팅 정렬 (Counting sort)

항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업을 하여, 선형 시간에 정렬하는 효율적인 알고리즘

**제한 사항**

정수나 정수로 표현할 수 있는 자료에 대해서만 적용가능

: 각 항목의 발생 회수를 기록하기 위해, 정수 항목으로 인덱스 되는 카운트들의 배열을 사용하기 때문

카운트들을 위한 충분한 공간을 할당하려면 집합 내의 가장 큰 정수를 알아야 한다.

- 카운트 배열의 최대 크기 = 1000000(백만)

```python
defCounting_Sort(A, B, k)
	# A [] ---입력 배열(1 to k)
	# B [] --- 정렬된 배열
	# C [] --- 카운트 배열
	
c = [0]* (k+1)
	for i in range(0, len(A)):
		C[A[i]] += 1

	for i in range(1, len(C)):
		C[i] += C[i-1]

	for i in range(len(B)-1, -1, -1):
		C[A[i]] -= 1
		B[C[A[i]]] = A[i]
```



## 완전 검색 (Exaustive Search)

문제의 해법으로 생각할 수 있는 모든 경우의 수를 나열해보고 확인하는 기법

Btute-force 혹은 generate-and-test 기법이라고도 함

모든 경우의 수를 테스트한 후, 최종 해법을 도출함

일반적으로 경우의 수가 상대적으로 작을 때 유용함



## 그리디 (Greedy Algorithm)

탐욕 알고리즘

최적해를 구하는 데 사용되는 근시안적인 방법

여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달함

각 선택의 시점에서 이루어지는 결정은 지역적으로는 최적이지만, 그 선택들을 계속 수집하여 최종적인 해답을 만들었다고 하여, 그 것이 최적이라는 보장은 없다.

일반적으로, 머릿속에 떠오르는 생각을 검증없이 바로 구현하면 Greedy접근이 된다.

### 그리디 알고리즘 동작과정

1. 해 선택 : 현재 상태에서 부분 문제의 최적 해를 구한 뒤, 이를 부분해 집합에 추가한다
2. 실행 가능성 검사 : 새로운 부분해 집합이 실행 가능한지를 확인한다. 곧, 문제의 제약 조건을 위반하지 않는지를 검사한다.
3. 해 검사 : 새로운 부분해 집합이 문제의 해가 되는지를 확인한다. 아직 전체 문제의 해가 완성되지 않았다면 1)의 해 선택부터 다시 한다.

| 알고리즘    | 평균 수행시간 | 최악 수행시간 | 알고리즘 기법 | 비고                                               |
| ----------- | ------------- | ------------- | ------------- | -------------------------------------------------- |
| 버블 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 코딩이 가장 쉽다                                   |
| 카운팅 정렬 | O(n+k)        | O(n+k)        | 비교환 방식   | n이 비교적 작을 때만 가능(최대 있음)               |
| 선택 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | 교환의 횟수가 버블, 삽입보다 작다                  |
| 퀵 정렬     | O(n log n)    | O(n^2)        | 분할 정복     | 최악의 경우 O(n^2)이지만, 평균적으로는 가장 빠르다 |
| 삽입 정렬   | O(n^2)        | O(n^2)        | 비교와 교환   | n의 개수가 작을 때 효과적이다.                     |
| 병합 정렬   | O(n log n)    | O(n log n)    | 분할 정복     | 연결리스트의 경우 가장 효율적인 방식               |