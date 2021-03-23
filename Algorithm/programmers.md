## 📍 프로그래머스 tip들

### 📌 2차원 리스트 뒤집기
```python
mylist = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
new_list = list(map(list, zip(*mylist)))

👉🏽 [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```
---
### 📌 i번째 원소와 i+1번째 원소
```python
mylist = [83, 48, 13, 4, 71, 11]
result = []

# 기존
for i in range(len(mylist)-1):
    result.append(abs(mylist[i] - mylist[i+1]))

# 개선
for i, j in zip(mylist, mylist[1:]):
    print(i, j)
👉🏽 
83, 48
48, 13
13, 4
4, 71
71, 11
```

---
### 📌 i번째 원소와 -i번째 원소
```python
mylist = [83, 48, 13, 4, 71, 11]
result = []

for i, j in zip(mylist, mylist[::-1]):
    print(i, j)
👉🏽 83, 11
48, 71
13, 4
4, 13
71, 48
11, 83
```

---
### 📌 모든 원소 타입(type) 변환하기
map함수는 두번째 인자의 각 원소에 첫번째 인자로 들어온 함수를 적용해준다.

```python
mylist = ['1', '100', '33']
print(list(map(int, mylist))
👉🏽 [1, 100, 33]
```

---
### 📌 배열 내 길이(len) 반환하기
```python
my_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(list(map(len, my_list)))
👉🏽 [3, 3, 3]
```

---
### 📌 sequence 멤버를 하나로 이어붙이기
```python
mylist = (1, 2, 3)
print(''.join(map(str, mylist)))
👉🏽 123

mylist = ['1', '2', '3']
print(''.join(mylist))
👉🏽 123
```

---
### 📌 곱집합(Cartesian product, 데카르트의 곱)
A = {a, b}, B = {c, d}
A x B = {(a, c), (a, d), (b, c), (b, d)}

```python
import itertools

A = {'a', 'b'}
B = {'c', 'd'}

result = [*(itertools.product(A, B))]
print(result)
👉🏽 [('b', 'c'), ('b', 'd'), ('a', 'c'), ('a', 'd')]

result = [''.join(i) for i in itertools.product(A, B)]
print(result)
👉🏽 ['bc', 'bd', 'ac', 'ad']
```

---
### 📌 2차원 리스트를 1차원 리스트로 만들기
```python
import itertools

mylist = [["A", "B"], ["X", "Y"], ["1"]]

result = sum(mylist, [])
👉🏽 ['A', 'B', 'X', 'Y', '1']

result = list(itertools.chain(*mylist))
👉🏽 ['A', 'B', 'X', 'Y', '1']
```

---
### 📌 순열과 조합
```python
import itertools
mylist = [1, 2, 3]

# 방법 1
result = [list(i) for i in itertools.permutations(mylist)]
result = sorted(result)

# 방법 2
result = list(map(list, itertools.permutations(mylist)))
result = sorted(result)
```

---
### 📌 가장 많이 등장하는 알파벳 찾기

푸는시간이 오래 걸린 문제다.
저번에 풀었던 <a href='https://www.acmicpc.net/problem/1157'>백준 1157 - 단어 공부</a> 문제와 비슷하지만 
지금 문제는 동일 max값이 2개 이상 존재할때도 값을 출력하는점이 저번문제와 조금 다르다. 접근방식을 조금 다르게 했어야하는데, 저번 풀이방법과 비슷하게 하다보니까 명확하게 문제를 해결하지 못했다.

어쩌다보니 문제를 풀면서 문법을 같이 공부하게 되었는데, `sort()`, `sorted()`함수의 차이점을 잘 알았다.
보통의 경우라면 `sorted()`를 사용하는편이 낫다.

1. sort()
  * 공간절약을 위해 시퀀스를 제자리에서 정렬한다.
  * 새로운 변수로 반환시 `None`을 출력한다.(리스트를 제자리에서 수정하기 때문)
  * 리스트에서만 사용가능하다.

2. sorted()
  * `iterable` 값들을 새로 돌려준다.

reference: <a href='https://docs.python.org/ko/3/library/functions.html#sorted'>파이썬 공식문서</a>

#### 💡 나의 풀이
풀이 순서는 다음과 같다.
>1. `Counter` 모듈 선언
>2. 입력값을 `dict`형으로 바꾸기
>3. `values`만 추출 
>4. `max`값을 찾기위해 정렬(sorted())
>5. `dict`를 돌면서 `value`값이 `max`값과 동일하면 리스트에 추가
>6. 사전순으로 출력해야하므로 재 정렬

```python
from collections import Counter

mylist = input().strip()
dic = dict(Counter(mylist))

values = [i for i in dic.values()]
values = sorted(values, reverse=True)

big = values[0]

result = [i for i, k in dic.items() if big == k]
result = ''.join(sorted(result))
print(result)
```

---
### 📌 flag대신 for-else 사용하기
>1. 제곱수: 어떤 자연수를 2번 곱해서 나오는 정수
>2. 완전제곱수: 어떤 정수를 제곱해서 만들 수 있는 정수

```python
# 1. flag사용
result = 1
flag = True

for i in range(5):
    n = int(input())
    result *= n
    if result**0.5 == int(result ** 0.5):
        flag = False
        print('found')
        break

if flag:
    print('not found')

# 2. for - else 사용
result = 1
for i in range(5):
    n = int(input())
    result *= n
    if int(result**0.5) == result**0.5:
        print(int(result**0.5), result**0.5)
        print('found')
        break
else:
    print('not found')
```