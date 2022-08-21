# 문자열

- 코드 체계 : 영어 대소문자 합쳐서 52이므로 6비트(2^6)(64)비트면 모두 표현할 수 있음

## 문자의 표현

### ASCII

7bit 인코딩 128개 문자 표현

33개의 출력 불가능한 제어 문자들과 공백을 비롯한 95개의 출력 가능한 문자

### 확장 ASCII

1B 내의 8bit를 모두 사용 (추가적인 문자 표현 가능)

### 유니코드

한글도 완성형으로 포함되어 있음

### Byte order

**big-endian**

**little-endian**

### strlen()함수 만들기

‘\0’을 만나면 ‘\0’을 제외한 글자수를 리턴

\#while을 써서 함수를 만드시오

~~~python
```조건
a = ['a','b','c','\\0']
print(strlen(a))
```

def strlen(a): 
    num = 0 
    i = '' 
    while i != '\0': 
        for i in a: 
            if i != '\0': 
                num += 1 
    print(num) 
    
a = ['a','b','c','\0'] 
print(strlen(a))
~~~

def strlen(a): num = 0 i = '' while i != '\0': for i in a: if i != '\0': num += 1 print(num) a = ['a','b','c','\0'] print(strlen(a))

### Python에서의 문자열 처리

문자열 클래스에서 제공되는 메소드

replace(), split(), isalpha(), find(), index()

find : 오류나면 -1

index : 오류나면 에러 (중요도에 따라 둘 중에 하나 사용)

### <참고>

```python

a = list(input())
print(a)

>> a b c
>>['a',' ','b',' ','c']

----------------------------------------------

 s = 'apple'

s[-2::] 
>> 'ie'
```



### 연습문제

문자열 뒤집어서 확인하기

```python
n = list(input())

if n[:] == n[::-1]:
    print('O')
else:
    print('X')

```

```python
def pel(a):
    n = list(a)
    if n[:] == n[::-1]:
        ans = True
    else:
        ans = False
    return ans

print(pel('anna'))
```



## 패턴 매칭

| 패턴 이름                   | 수행 시간 |
| --------------------------- | --------- |
| 고지식한 패턴 검색 알고리즘 | O(mn)     |
| 카프-라빈 알고리즘          | O(n)      |
| KMP 알고리즘                | O(n)      |



### 고지식한 패턴 검색 알고리즘 (Brute Force)

(무식하게 처음부터 하나씩) 패턴내의 문자들을 일일이 비교하는 방식

```python
#for를 이용한 Brute Force method#
source = "This is a book~!"
pattern = 'is'

def BruteForce(pattern, source):
    for idx in range(len(source)-len(pattern) + 1):
        for j in range(len(pattern)):
            if source[idx + j] != pattern[j]:
                break
        else:
            return idx
    else:
        return -1

print(BruteForce(pattern, source))
```



### 보이어-무어 알고리즘

문자열이 불일치할 확률이 뒷부분에서 더 높음

첫글자를 잡고, 찾을문자열 길이 끝에 찾고있는 문자열 중에 없는 문자가 있으면 한번에 그만큼을 버림

검색 엔진에 문자를 검색했을 때, 보이어-무어 방식으로 많이 찾음



### 카프-라빈 알고리즘

미리 준비한  Hash table을 통해 패턴의 연산값을 구함

Hash 값이 일치하는 window를 찾아냄



### KMP 알고리즘

불일치가 발생한 텍스트 스트링의 앞 부분에 어떤 문자가 있는지를 미리 알고 있으므로, 불일치가 발생한 앞 부분에 대하여 다시 비교하지 않고 매칭을 수행



## 문자열 암호화



### 시저 암호

```python
def caesar(s, n):
    s = list(s)
    for i in range(len(s)):
        if s[i].isupper():
            s[i]=chr((ord(s[i])-ord('A')+ n)%26+ord('A'))
        elif s[i].islower():
            s[i]=chr((ord(s[i])-ord('a')+ n)%26+ord('a'))
 
    return "".join(s)
 
print(caesar("a B z", 4)) # 'e F d'
```