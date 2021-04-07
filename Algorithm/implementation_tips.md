## 💡 implementation_tips
> python: python코드를 C언어로 바꾸는 것이 아니라, 컴파일 하여 `bytecode`로 바꾸고 다음 인터프리터가 실행된다.
> pypy: 프로그램을 실행하기 전에 컴파일 하는 대신, 프로그램을 실행하는 시점에서 필요한 부분들을 즉석으로 컴파일 하는 방식, pypy3에서는 자주 쓰이는 코드를 캐싱하는 기능이 있기 때문에, 메모리를 조금 더 사용하여 저장하며, 실행속도를 개선할 수 있다.

결론
1. 간단한 코드: `python3`가 메모리, 속도 측에서 우세
2. 복잡한 코드(반복): `pypy3`가 우세

---
## 📍 단락평가(Short Circuit Evaluation)
논리연산에서 코드의 앞만 보고 값을 정할 수 있는 경우 뒤에 나타나는 코드는 분석하지 않고도 값을 결정하는 방법을 뜻하는데,
쉽게 말하면 어떤 논리연산자(`and`, `or`)가 오느냐에따라 비교대상이 달라진다는 의미이다.
이전에 프로그래머스 `level-1` 문제를 풀고 다른사람의 코드를 볼 때 궁금했던 코드가 있었다.

예를 들면, `return 10 % 2 == 0 and 'even' or 'odd'`와 같은 코드인데, 이 코드를 한번에 해석할 수 있다?!라고 하면 이 글을 넘겨도 된다.
하지만, 모르는 사람도 있기에 간략하게나마 작성하려 한다. (자세한 내용은 <a href='https://dojang.io/mod/page/view.php?id=2192'>코딩도장</a>의 강의를 듣자.)

결론적으로 `and`, `or`연산자가 있을 때 단락평가는 다음과 같다.
>1. `A and B`: A가 `True`면 뒤의 값을 반환하고, A가 `False`면 앞의 값을 반환한다.
>2. `A or B`: A가 `True`면 앞의 값을 반환하고, A가 `False`면 뒤의 값을 반환한다. 

내용이 확 와닿지 않는가? 그럼 다음 사진을 보자. 다음 사진은 `and`와 `or`의 진리표이다.
두 진리표를 보면 규칙을 찾을 수 있는데, 
>1. `and`: 앞이 `False`면 뒤는 쳐다보지않고 그대로 앞의 값(`False`)을 출력한다. 반면에 앞이 `True`면 뒤의 값을 분석해야하기 때문에 뒤의 값을 출력한다.
>2. `or`: 앞이 `True`면 뒤는 쳐다보지않고 그대로 뒤의 값(`True`)를 출력한다. 반면에 앞이 `False`면 뒤의 값을 분석해야하기 때문에 뒤의 값을 출력한다.

보통 `숫자, 숫자`와 같은 값들은 비교하기 쉬운데 `숫자, 문자` 혹은 `문자, 숫자` 등 섞여있는 형들은 한눈에 비교하기가 쉽지 않다.
다음의 문제를 보고 답이 무엇인가 곰곰이 생각해보자. 해답은 코드 밑을 드래그해보자! 


```python
# 1. and
print('python' and 'JS')
print('python' and 0)
print(0 and 'python')
print(0 and False)

# 2. or
print('python' or 'JS')
print('python' or 0)
print(0 or 'python')
print(0 or False)

# 3. arr or -1
arr = []
print(arr or -1)

arr = [1]
print(arr or -1)
```

정답은 다음과 같다.
1. 'JS'
2. 0
3. 0
4. 0
5. 'python'
6. 'python'
7. 'python'
8. False
9. -1
10. [1]

지금까지 단락평가에 대해서 짧게 배워봤다.
이를 토대로 프로그래머스 문제 풀 때 잘 써먹을 수 있을 것 같다.

---
## 📍 자릿수 만큼 0채우기
주어진 자릿수 만큼 이진수의 값에 0을 채우기

```python
# 7번째 자리까지 출력
n = 7

print('{0:>0{1:}}'.format(int(bin(9)[2:]), n))
print(bin(9)[2:].zfill(n))
print('0'*(n-len(bin(9)[2:])) + bin(9)[2:])
👉🏽 0001001
```

---
## 📍 dictionary max key, min key 가져오기
`max(arr, key= arr.get)`, `min(arr, key= arr.get)`

```python
info_dict = {'bob': 20, 'tony': 15, 'suzy': 30,  "mario": 100}

print(max(info_dict, key= info_dict.get))
👉🏽 mario
print(min(info_dict, key= info_dict.get))
👉🏽 tony
```

---
## 📍 모든 대문자, 소문자, 대소문자, 숫자 가져오기
```python
import stringx

print(string.ascii_lowercase)
👉🏽 abcdefghijklmnopqrstuvwxyz
print(string.ascii_uppercase)
👉🏽 ABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.ascii_letters)
👉🏽 abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.digits)
👉🏽 0123456789
```

---
## 📍 람다식을 사용한 간편한 식
1. 2개의 배열을 zip함수를 사용하여 비트or연산하기
   
```python
# 5자리수까지 출력
n = 5
arr1 = [1, 2, 3, 4, 5]
arr2 = [5, 6, 7, 8, 9]

arr = list(map(lambda x: x[0] | x[1], zip(arr1, arr2))
arr = list(map(lambda x: bin(x)[2:].zfill(n), arr))
```

---
## 📍 반복문을 두번 돌아야할 때 한번만 돌기
```python
result = []
for i in arr:
    i = i.replace('1', '#')
    i = i.replace('0', ' ')
    result.append(i)
print(result)
```

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
동일한 개수로 이루어진 자료형을 묶어주는 함수다. 여러개의 `iterable`을 동시에 순회할 때 사용한다.

```python
# 각 리스트의 앞 정수만 출력해서 새로운 배열 만들기
mylist = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
new_list = list(map(list, zip(*mylist)))
👉🏽 [[1, 4, 7], [2, 5, 8], [3, 6, 9]]

# 각 리스트를 dict형태로 만들기
animals = ['cat', 'dog', 'lion']
sounds = ['meow', 'woof', 'roar']
answer = dict(zip(animals, sounds))
👉🏽 {'cat': 'meow', 'dog': 'woof', 'lion': 'roar'}
```

```python
fruits = ['alpha', 'bravo', 'charlie']
name = [1, 2, 3]

for f, n in zip(fruits, name):
    print(f, n)

👉🏽 alpha 1
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

---
## 📍 자신은 제외하고 뽑을 때 
```python
numbers = [1, 2, 3, 4, 5]

for i in range(len(numbers)):
    for j in range(i+1, len(numbers)):
        print(i, j,end=' ')
    print()
    
👉🏽
0 1 0 2 0 3 0 4 
1 2 1 3 1 4 
2 3 2 4 
3 4 
```

---
## 📍 max값의 자리수(index)를 찾을 때
1. max값이 1개: index()
   
```python
# 1. index()
result = [1, 2, 3, 4]
print(result.index(max(result)))
👉🏽 3

# 2. for()
for i in range(len(result)):
    if result[i] == max(result):
        print(i)
👉🏽 3
```

2. max값이 2개이상: for(), enumerate()
```python
result = [1, 7, 2, 3, 7, 7]

# for()
answer = [i for i in range(len(result)) if result[i] == max(result)]
👉🏽 1 4 5

# enumerate()
answer = [idx for idx, v in enumerate(result) if v == max(result)]
👉🏽 1 4 5
```

---
## 📍 sum을 표현하는 3가지 방법
```python
# 1.
result = 0
for i in range(1, 10+1):
    result += i

# 2.
result = sum(i for i in range(1, 10+1))

# 3.
result = sum(range(1, 10+1))
```