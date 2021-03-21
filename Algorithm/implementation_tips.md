## 💡 implementation_tips
> python: python코드를 C언어로 바꾸는 것이 아니라, 컴파일 하여 `bytecode`로 바꾸고 다음 인터프리터가 실행된다.
> pypy: 프로그램을 실행하기 전에 컴파일 하는 대신, 프로그램을 실행하는 시점에서 필요한 부분들을 즉석으로 컴파일 하는 방식, pypy3에서는 자주 쓰이는 코드를 캐싱하는 기능이 있기 때문에, 메모리를 조금 더 사용하여 저장하며, 실행속도를 개선할 수 있다.

결론
1. 간단한 코드: `python3`가 메모리, 속도 측에서 우세
2. 복잡한 코드(반복): `pypy3`가 우세

---
## 📍 list에서 첫번째, 마지막 값만 변수로 선언하기
```python
array = [10, 20, 30, 40, 50]

first_index, *rest, last_index = array

print(first_index)
👉🏽 10
print(*rest)
👉🏽 20 30 40
print(last_index)
👉🏽 50
```

---
## 📍 Swap
두 변수의 값을 바꾸는 기능
```python
# 기존
a = 'MyName'
b = 'AYW'

temp = a
a = b
b = temp
👉🏽 AYW MyName

# 향상
a = 1
b = 2

a, b = b, a
print(a, b)
👉🏽 2 1
```

---
## 📍 Packing
하나의 변수에 여러 값을 할당하는 방법
```python
a, b, c = [1, 2, 3]
d = a, b, c

print(d)
👉🏽 (1, 2, 3)
```

---
## 📍 Unpacking
for문을 사용하지 않고도 iterable한 결과를 출력하고 싶을 때
`tuple`, `set`형도 가능하다.

```python
array = [1, 2, 3, 4, 5]

for i in array:
    print(i, end=' ')
👉🏽 1 2 3 4 5

print(*array)
👉🏽 1 2 3 4 5
```

---
## 📍 zip
동일한 개수로 이루어진 자료형을 묶어주는 함수다
```python
fruits = ['alpha', 'bravo', 'charlie']
name = [1, 2, 3]

for f, n in zip(fruits, name):
    print(f, n)

👉🏽alpha 1
bravo 2
charlie 3

print(list(zip(fruits, name)))
👉🏽 [('alpha', 1), ('bravo', 2), ('charlie', 3)]

print(dict(zip(fruits, name)))
👉🏽 {'alpha': 1, 'bravo': 2, 'charlie': 3}
```

>reference: <a href='https://github.com/VSFe/Algorithm_Study/blob/main/Concept/00_Special/Pythonic_Code_For_Coding_Test.md'>VSfe_github</a>

---
## 📍 n번째 자리까지 무조건 출력하기

```python
# 소수점 넷째자리에서 반올림하여 무조건 소숫점 셋째 자리까지 출력 할 때.
a, b = map(float, input().split())
print('%.3f' %(a/b))
👉🏽 2.000
```

---
## 📍 원본 리스트에 중복된 숫자가 있는지 확인 할 때
```python
# 1. set형 중복확인
import random

n = int(input())
A = random.sample(range(-n, n + 1), n)
set_A = set(A)

def check_string(n):
    if len(A) > len(set_A):
        return print('겹치는 원소가 존재합니다.')
    else:
        return print('겹치는 원소가 존재하지 않습니다.')

check_string(A)

# 2. 원소 하나씩 확인
import random

n = int(input())
A = random.sample(range(-n, n + 1), n)
A.sort()

def check(n):
    for i in range(len(A)):
        if i < len(A) -1 and A[i] in A[i+1:]:
            return '겹치는 원소가 존재합니다.'
    else:
        return '겹치는 원소가 존재하지 않습니다.'

print(check(A))
```

---
## 📍 빈 리스트에 입력값을 바로 추가할 때
```python
'''
3
1
2
3
'''
import sys
input = sys.stdin.readline
N = int(input())
data = [0] * N

for i in range(N):
    data[i] = int(input())
print(data)
👉🏽 [1, 2, 3]
```
