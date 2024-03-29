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
## 📍 리스트, 문자열 거꾸로 출력하기
```python
arr = [1, 2, 3, 4, 5]

# 1. 슬라이싱
for i in arr[::-1]:
    print(i, end = ' ')
👉🏽 1, 2, 3, 4, 5

# 2. 범위 거꾸로 선언하기
for i in range(len(arr)-1, -1, -1):
    print(arr[i], end = ' ')
👉🏽 1, 2, 3, 4, 5

# 3. 출력 거꾸로 선언하기
for i in range(len(arr)):
    print(arr[-i-1], end = ' ')
👉🏽 1, 2, 3, 4, 5
```

```python
s = 'soju'

# 1. 슬라이싱
for i in s[::-1]:
    print(i, end = ' ')
👉🏽 u j o s

# 2. 범위 거꾸로 선언하기
for i in range(len(s)-1, -1, -1):
    print(s[i], end = ' ')
👉🏽 u j o s

# 3. 출력 거꾸로 선언하기
for i in range(len(s)):
    print(s[-i-1], end = ' ')
👉🏽 u j o s
```

---
## 📍 2차원 행렬에서 대각선 값만 출력하기
```python
n = 3
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# (0, 0), (1, 1), (2, 2) 
for i in range(n):
    print(arr[i][i], end=' ')
👉🏽 1 5 9


# (0, 2), (1, 1), (2, 0)
for i in range(n):
    print(arr[i][n-i-1])
👉🏽 3 5 7
```

---
## 📍 가장 큰 value, 큰 value를 갖는 key찾기
```python
dic = {'a':0, 'b':1, 'c':2}
print(max(dic.values()))
print(max(dic.keys(), key=lambda x: a[x]))
```

---
## 📍 2차원 행렬에서 90도 회전하기
```python
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
result = list(map(list, zip(*arr[::-1])))
👉🏽 [[7, 4, 1], [8, 5, 2], [9, 6, 3]]
```

---
## 📍 2차원 행렬에서 최소값, 최대값 구하기
```python
graph = [[6, 8, 2, 6, 2], [3, 2, 3, 4, 6], [6, 7, 3, 3, 2], [7, 2, 5, 3, 6], [8, 9, 5, 2, 7]]
max_graph = max(map(max, graph))
min_graph = min(map(min, graph))
print(max_graph, min_graph)
👉🏽 2 9
```

---
## 📍 정수의 각 자리수를 제곱하기
```python
def solution(n):
    return sum([int(i) ** 2 for i in str(n)])
print(solution(57))
👉🏽 74
```

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
# 일반적인 zip 사용법
arr1 = ['a', 'c', 'e']
arr2 = ['b', 'd', 'f']

result = list(map(list, zip(arr1, arr2)))
print(result)
👉🏽 [['a', 'b'], ['c', 'd'], ['e', 'f']]

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

---
## 📍 각 자리의 수 더하기
```python
n = 126

# 1. 재귀 함수
def sum_digit(n):
    if n < 10:
        return n
    return n % 10 + sum_digit(n//10)

print(sum_digit(n))
👉🏽 9

# 2. map 함수
result = sum(map(int, str(n)))

print(result)
👉🏽 9

# 3. 반복문
temp = 0
for i in str(n):
    temp += int(i)
    
print(temp)
👉🏽 9
```

---
## 📍 if, elif 다중 조건
`if`를 다중조건으로 사용하면 모든 `if`를 검사한다. 반면에, `if` + `elif`를 다중조건으로 사용하면 `if`에 조건이 걸리면 `elif`는 모두 지나친다.

```python
x, y, z = 10, 20, 30

# if 다중조건
if x == 10:
    print(x)
if y == 20:
    print(y)
if z == 30:
    print(z)

👉🏽 
10
20
30

# if + elif 다중 조건
if x == 10:
    print(x)
elif y == 20:
    print(y)
elif z == 30:
    print(z)

👉🏽 10
```

---
## 📍 cnt 유용하게 사용하기

각각의 `index`마다 `cnt`를 세고 싶으면 배열만큼 초기화해준다음 반복문 내부 `i`번째에서 해당 `cnt[i]`를 증가시켜주자.

```python
# before
n = int(input())
people = [tuple(map(int, input().split())) for _ in range(n)]
result = []

for i in range(n):
    prize = 1
    for j in range(n):
        if people[i][0] < people[j][0] and people[i][1] < people[j][1]:
            prize += 1
    result.append(prize)
print(' '.join(map(str, result)))
```

```python
# after
n = int(input())
people = [tuple(map(int, input().split())) for _ in range(n)]
result = []
prize = [1] * n

for i in range(n):
    for j in range(n):
        if people[i][0] < people[j][0] and people[i][1] < people[j][1]:
            prize[i] += 1
print(' '.join(map(str, result)))
```

---
## 📍 이중 반복문에서 print의 위치 별 출력
`n*n행렬` 문제를 풀 때마다 `print`를 어디에다 써야할지 헷갈려서 참고하기 위한 글이다.

다음은 `1`씩 증가하는 `n*n` 배열에서 `arr[i][j]`가 `10`보다 클 경우 cnt가 증가하는 코드이다.

1. 1번위치: `number`가 10보다 큰 조건일때만 `cnt` 출력: `10 1`, `11 2`, `12 3`, `13 4`, `14 5`, `15 6`, `16 7`
2. 2번위치: 조건에 상관없이 모든 좌표에서 `cnt` 출력: `1 0`, `2 0`, `3 0`, `4 0`, `5 0`, `6 0`, `7 0`, `8 0`, `9 0`, `10 1`, `11 2`, `12 3`, `13 4`, `14 5`, `15 6`, `16 7`
3. 3번위치: `j`번은 다 돌고 `i`번째 돌 때 출력 즉, 행을 돌때 출력한다. 주의 할 점은 누적된 값을 출력한다. 4행이니까 4번 출력: `4 0`, `8 0`, `12 3`, `16 7`
4. 4번위치: 모든 경우의 수를 다 돌고나서 출력: `16 7`

```python
'''
1 2 3 4 
5 6 7 8 
9 10 11 12 
13 14 15 16 
'''

n, number, cnt = 4, 0, 0
arr = [[0] * n for _ in range(n)]

for i in range(n):    # 1부터 증가하는 배열 만들기
    for j in range(n):
        number += 1
        arr[i][j] = number

for i in range(n):    # print 확인하는 코드
    for j in range(n):
        if arr[i][j] >= 10:
            cnt += 1
            print(arr[i][j], cnt)    # 1번 위치
        print(arr[i][j], cnt)    # 2번 위치
    print(arr[i][j], cnt)    # 3번 위치
print(arr[i][j], cnt)    # 4번 위치

👉🏽 1번 위치: 10 1 11 2 12 3 13 4 14 5 15 6 16 7
👉🏽 2번 위치: 1 0 2 0 3 0 4 0 5 0 6 0 7 0 8 0 9 0 10 1 11 2 12 3 13 4 14 5 15 6 16 7
👉🏽 3번 위치: 4 0 8 0 12 3 16 7
👉🏽 4번 위치: 16 7
```

---
## 📍 `n * n` 행렬에서 `target * target` 크기만큼 자르기
가로세로가 동일한 `n*n` 행렬에서 `n`보다 작은 `target*target` 행렬만큼 잘라 출력하고 싶을 때는 다음과 같이 작성하자.

예를 들어, `n = 5`, `target = 3`일때는 다음과 같은 과정을 거친다.
1. `arr`행렬을 초기화해준다. 출력값이 제대로 나오는지 확인하기위해 `arr`은 1부터 차례대로 증가하는 행렬로 초기화한다. 
2. 범위를 `n`으로 하는 이중 반복문을 선언한다. 이때 `index`오류를 방지하기위해 `n`을 `target-1`로 빼준다. `-1`을 빼주지 않으면 제일 마지막 행과 열은 계산하지 않으니까 꼭 빼주도록 하자.
3. 이중 반복문안에 이중반복문을 한번 더 선언한다. 가독성을 위해 `each_case`라는 함수를 선언했는데, 중요한 점은 출력하려는 좌표에 `i+a, j+b`를 해줘야 모든 좌표를 출력 할 수 있다.

```python
n = 5
target = 3

arr = [[0] * n for _ in range(n)]
cnt = 0

# use def function
def each_case(a, b):    # target * target 행렬 출력
    for i in range(target):
        for j in range(target):
            print(arr[i+a][j+b], end=' ')
        print()
    print()

for i in range(n):    # arr 행렬 초기화
    for j in range(n):
        cnt += 1
        arr[i][j] = cnt

for i in range(n-(target-1)):    # n * n 행렬 안에서 each_case 함수 실행
    for j in range(n-(target-1)):
        each_case(i, j)

# not use def function
for i in range(n):
    for j in range(n):
        cnt += 1
        arr[i][j] = cnt

for i in range(n-(target-1)):
    for j in range(n-(target-1)):
        for k in range(target):
            for l in range(target):
                print(arr[k + i][l + j], end=' ')
            print()
        print()

👉🏽 출력은 동일
1 2 3 
6 7 8 
11 12 13 

2 3 4 
7 8 9 
12 13 14 

3 4 5 
8 9 10 
13 14 15 

6 7 8 
11 12 13 
16 17 18 

7 8 9 
12 13 14 
17 18 19 

8 9 10 
13 14 15 
18 19 20 

11 12 13 
16 17 18 
21 22 23 

12 13 14 
17 18 19 
22 23 24 

13 14 15 
18 19 20 
23 24 25 
```

---
## 📍 if와 elif의 차이
다중조건에서 `if`를 사용하면 모두 검사하는데, `if, elif`를 사용하게 되면, `if`절을 만족했을때, `elif`는 검사하지않고 그대로 건너뛴다.

```python
x, y, z = 10, 20, 30

if x == 10:
    print(x)
if y == 20:
    print(y)
if z == 30:
    print(z)

👉🏽 10 20 30

if x == 10:
    print(x)
elif y == 20:
    print(y)
elif z == 30:
    print(z)

👉🏽 10
```

---
## 📍 2차원 행렬에서 세로로 최대값, 최소값 갱신하기
`세로 R`, `가로 S`인 2차원 행렬에서 세로로 최대값과 최소값을 갱신 할 때 어떻게 할까? 예를들어 다음과 같은 2차원 행렬이 있다고 가정해보자.

```python
'''
R, S = 10, 4
x...
xx..
.xx.
..xx
...x
....
#...
##..
.##.
..##
...#
'''
```

여기서 `x`일 때 각 세로축에서의 최대값, `#`일 때 각 세로축에서의 최소값을 구하려면 다음과 같이 구할 수 있다. 
다음과 같이 가로길이만큼 빈 리스트를 선언해준 다음 현재 좌표가 `x` 일 때 해당하는 열을 빈리스트의 `index`로 사용한다. 이때 비교해야하는 값은 `i(row)`다. 높이는 `row`값이기 때문이다. `min`값도 마찬가지로 해당하는 열을 `index`로 사용하고 그때의 `row`값을 비교하여 더 작은값을 갱신해주면 된다. 

입력을 받아야하는 문제를 풀때 `arr = [input() for _ in range(R)]`로 선언해주면 되는데 `input()`에도 `list()`를 씌우지 않아도 되는 이유는 문자열에서도 인덱싱이 가능하기 때문이다.

```python
R, S = 10, 4
arr = ['x...', 'xx..', '.xx.', '..xx', '....', '#...', '##..', '.##.', '..##', '...#']

max_dot = [-3333] * S
min_sharp = [1 << 14] * S

for i in range(R):
    for j in range(S):
        if arr[i][j] == 'x':
            max_dot[j] = max(max_dot[j], i)
        elif arr[i][j] == '#':
            min_sharp[j] = min(min_sharp[j], i)

print(max_dot)
👉🏽 [1, 2, 3, 3]
print(min_sharp)
👉🏽 [5, 6, 7, 8]
```

---
## 📍 여러 줄의 입력을 한 줄로 출력 하고 싶을 때
아래 보기와 같은 입력일때 1줄로 출력하려면 어떻게 할까? 리스트끼리는 덧셈이 가능한데, `1차원 리스트 + 1차원 리스트` = `1차원 리스트`가 된다.

```python
'''
5 10 7 16 2
4 22 8 17 13
3 18 1 6 25
12 19 23 14 21
11 24 9 20 15
'''

n = 5
num = []
for _ in range(n):
    num += list(map(int, input().split()))

print(num)
👉🏽 [5, 10, 7, 16, 2, 4, 22, 8, 17, 13, 3, 18, 1, 6, 25, 12, 19, 23, 14, 21, 11, 24, 9, 20, 15]
```

---
## 📍 2차원 행렬에서 세로(column) 열만 추출하기
1부터 25까지 순서대로 있는 `5 * 5`행렬에서 `세로 (열(column))`만 추출하는 방법을 알아보자. 총 3가지 방법으로 `2중 반복문`, `lambda`, `zip`함수를 사용했다. (더 좋은 방법이 있으면 댓글로 알려주세요!!) 결과는 모두 동일하다.

```python
# 1 ~ 25까지 배열 만들기
arr = [[0] * 5 for _ in range(5)]
cnt = 0

for i in range(5):
    for j in range(5):
        cnt += 1
        arr[i][j] = cnt

# 2중 반복문
result = [[arr[j][i] for j in range(5)] for i in range(5)]

# lambda 함수
result = [list(map(lambda x: x[i], arr)) for i in range(5)]

# zip 함수
result = list(map(list, zip(*arr)))

👉🏽 [[1, 6, 11, 16, 21], [2, 7, 12, 17, 22], [3, 8, 13, 18, 23], [4, 9, 14, 19, 24], [5, 10, 15, 20, 25]]
```

---
## 📍 한 줄에 n개씩 끊어서 출력하기
`1~25`까지 있는 리스트를 n개씩 끊어서 출력하는 코드를 작성 할 때 다음과 같이 작성 할 수 있다. 

1. `index` 계산을 위해 앞에 `-3333`을 채운다.
2. `1, n+1`까지 반복문을 선언한 후 `i`가 `i % n == 0`이면 `print()`를 추가한다.

```python
n = 25
arr = [-3333] + [i for i in range(1, 25+1)]

for i in range(1, n+1):
    print(arr[i], end= ' ')
    if not i % 5:
        print()

👉🏽 
1 2 3 4 5 
6 7 8 9 10 
11 12 13 14 15 
16 17 18 19 20 
21 22 23 24 25 
```

---
## 📍 n의 배수인 index만 출력하기
n의 범위가 20인 `arr`에서 3의 배수인 `index`만 출력하는 코드를 작성해라

```python
n = 20
target = 3
arr = [i for i in range(20)]

# 나머지 
for i in range(1, n+1):
    if not i % 3:
        print(arr[i], end=' ')

# step = target
for i in range(target, n+1, 3):
    print(arr[i], end=' ')

👉🏽 3 6 9 12 15 18
```

---
## 📍 0과 1만있는 값에서 상태 변화하기
`0`: 스위치가 꺼져있는 상태
`1`: 스위치가 켜져있는 상태

`index`가 3의 배수인 자리면, `0`일 때는 `1`로, `1`일 때는 `0`으로 변경하는 코드를 작성하라. (`arr`은 1부터 센다.)

```python
n = 10
target = 3
arr = [-3333, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

for i in range(target, n + 2, 3):
    arr[i] = (arr[i] + 1) % 2

print(arr[1:])
👉🏽 [0, 0, 1, 0, 0, 1, 0, 0, 1, 0]
```

1부터 n까지 i번째의 배수마다 상태를 변화하는 코드 

```python
for i in range(1, n + 1):
    for j in range(i, n + 1, i):
        gate[j] = (gate[j] + 1) % 2
    print(gate)
```

---
## 📍 여러줄 문자열 입력에서 좌우, 상하 반전 출력하기
보통 여러줄(`n*n` 크기)로 문자열을 입력받을 때의 좌우, 상하 반전 방법이다. 코드가 짧기 때문에 외워두면 좋을 것 같다.

```python
s = ['ABC', 'DEF', 'GHI']

# 그대로 출력
print(*s, sep='\n')
👉🏽
ABC
DEF
GHI

# 좌우 반전
print(*[i[::-1] for i in s], sep='\n')
👉🏽
CBA
FED
IHG

# 상하 반전
print(*s[::-1], sep='\n')
👉🏽
GHI
DEF
ABC
```

---
## 📍 함수(def)에서 return 인자의 수가 다를 때
코딩테스트 문제를 풀다보면 `False`일때 `-1`만 `return` 시키고 `True`면 `a, b`처럼 1개 이상을 `return`해야 할 때 다음과 같이 작성 할 수 있다.
만약, `a+b`값이 20을 넘으면 `a, b`을 리턴해야하고, 아니면 `-1`을 리턴해야한다면 다음과 같은 코드가 될 것이다.

```python
a, b = map(int, input().split())

def check():
    if a + b >= 20:
        return a, b
    else:
        return -1
    
print(check())
```

하지만, `-1`의 리턴값에 임의의 수 `0`을 넣고 똑같이 2개를 리턴하게 작성한 다음 첫번째 값이 `-1`이면 -1을 출력시키고 아니면 `c, d`를 출력하게 할 수 있다.

```python
a, b = map(int, input().split())

def check():
    if a + b >= 20:
        return a, b
    else:
        return -1, 0

c, d = check()
if c == -1:
    print(-1)
else:
    print(c, d)
```

---
## 📍 나머지(%) 사용 할 때 조건 추가하기
<a href='https://ywtechit.tistory.com/152?category=930542'>저번</a>에 풀었던 <a href='https://www.acmicpc.net/problem/1009'>boj 1009 - 분산처리</a> 문제와 이것과 비슷했던<a href='https://ywtechit.tistory.com/91'>문제</a>인 <a href='https://www.acmicpc.net/problem/10250'> boj 10250 - ACM 호텔</a> 역시 동일하게 나머지(%)를 사용하면 나머지 조건을 추가해줘야 한다.

예를 들어, `arr = [-3333, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ...]` 처럼 표현하고 싶다면 (`arr[1]`부터 세기위해 `arr[0]`에 `-3333`을 넣었다.) 해당 패턴은 `index`의 값은 `10`으로 나눈 나머지가 될 것이다. 하지만 단순하게 나머지 값만 추가하면 `arr[10]`은 10이 아니라 0이 된다. 이 때문에 나머지를 사용해서 수를 셀 때는 나머지 조건을 붙여줘야한다. 다음 코드처럼 말이다.

```python
index = 20
arr = [0] * 50
calculate = index % 10

# 나머지가 0인 조건을 고려하지 않은 코드
arr[index] = calculate

print(arr[index])
👉🏽 0

# 나머지가 0인 조건을 고려한 코드
if not calculate:
    arr[index] = calculate + 10
else:
    arr[index] = calculate

print(arr[index])
👉🏽 10
```

---
## 📍 3개의 주사위를 던져 n개의 동일한 값 찾기
제목을 어렵게 지었지만 간단하게 말하면 3개의 값을 비교했을 때 `3개가 동일한 경우`, `2개가 동일한 경우`, `모두 다른 경우`를 찾는 조건문을 작성하는 방법이다.
<a href='https://www.acmicpc.net/problem/2480'>boj_2480 - 주사위 세개</a>를 풀면 이를 활용한 문제라는 것을 알 수 있다.

```python
a, b, c = map(int, input().split())

if a == b and b == c:    
    print('3개가 동일한 경우')

elif a == b or b == c:
    print('2개가 동일한 경우')

elif a == c:
    print('2개가 동일한 경우')

else:
    print('모두 다른 경우')
```

---
## 📍 2차원 행렬 상하, 좌우 반전하기
크기가 `n * m`인 2차원 `arr`배열이 있을 때, 상하 좌우 반전하는 방법을 알아보자. 2가지 방법이 있는데, `반복문`, `문자열 슬라이싱`을 사용하는 방법이 있다.

```python
# 상하 반전
n, m = 4, 6
arr = [[1, 2, 3, 4, 5, 6], [7, 8, 9, 10, 11, 12], [13, 14, 15, 16, 17, 18], [19, 20, 21, 22, 23, 24]]
temp = [[0] * m for _ in range(n)]

# 1. 반복문
for i in range(n):
    temp[i] = arr[n-1-i]

# 2. 문자열 슬라이싱
arr = arr[::-1]

👉🏽 
19 20 21 22 23 24 
13 14 15 16 17 18
7 8 9 10 11 12
1 2 3 4 5 6 
```

```python
# 좌우 반전
n, m = 4, 6
arr = [[1, 2, 3, 4, 5, 6], [7, 8, 9, 10, 11, 12], [13, 14, 15, 16, 17, 18], [19, 20, 21, 22, 23, 24]]
temp = [[0] * m for _ in range(n)]

# 1. 반복문
for i in range(n):
    for j in range(m):
        temp[i][j] = arr[i][m-1-j]

# 2. 문자열 슬라이싱
for i in range(n):
    arr[i] = arr[i][::-1]

👉🏽
6 5 4 3 2 1
12 11 10 9 8 7
18 17 16 15 14 13
24 23 22 21 20 19 
```

---
## 📍 2차원 행렬 시계, 반시계 방향으로 90도 뒤집기
크기가 `n * m`인 2차원 `arr`배열이 있을 때, 시계, 반시계 방향으로 90도 뒤집는 방법을 알아보자. 2가지 방법이 있는데, `반복문`, `zip`을 사용하는 방법이 있다.

```python
# 시계방향으로 90도 뒤집기
n, m = 4, 6
arr = [[1, 2, 3, 4, 5, 6], [7, 8, 9, 10, 11, 12], [13, 14, 15, 16, 17, 18], [19, 20, 21, 22, 23, 24]]
temp = [[0] * m for _ in range(n)]

# 1. 반복문
for i in range(m):
    for j in range(n):
        temp[i][j] = arr[n-1-j][i]

# 2. zip함수
arr = list(map(list, zip(*arr[::-1]))

👉🏽
19 13 7 1
20 14 8 2
21 15 9 3
22 16 10 4
23 17 11 5
24 18 12 6
```

```python
# 반시계방향으로 90도 뒤집기
n, m = 4, 6
arr = [[1, 2, 3, 4, 5, 6], [7, 8, 9, 10, 11, 12], [13, 14, 15, 16, 17, 18], [19, 20, 21, 22, 23, 24]]
temp = [[0] * m for _ in range(n)]

# 1. 반복문
for i in range(m):
    for j in range(n):
        temp[i][j] = arr[j][m-1[i]]

# 2. zip함수
arr = list(map(list, zip(*arr))[::-1]

👉🏽
6 12 18 24
5 11 17 23
4 10 16 22
3 9 15 21
2 8 14 20
1 7 13 19
```

---
## 📍 삼각수(계차수열) 나타내기
삼각수의 정의: <a href='https://ko.wikipedia.org/wiki/%EC%82%BC%EA%B0%81%EC%88%98'>위키백과</a>

`6`의 배수씩 증가하는 계차수열을 구할 때는 다음과 같이 작성하자. `temp`은 종료조건을 넣기위해 넣었다.

```python
temp = 100
difference = 1
i = 1

while temp > difference:
    difference = difference + ( 6 * i )
    i += 1
print(difference)
```

---
## 📍 리스트 중 front, back에서부터 target index까지 어느쪽이 더 가까운지 판단하기
길이가 `10`인 리스트 `arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` 일 때, `target_index = 3(값은 4)`는 앞에서부터 더 가까운지 아니면 뒤에서부터 가까운지 판단하고 싶을 때 다음과 같은 코드를 작성하면 된다.

응용문제로는 <a href='https://www.acmicpc.net/problem/1021'>백준 1021 - 회전하는 큐</a>가있다.

1. `front`와 `back`을 나누는 기준은 `len(arr) // 2`이다.
2. 만약, `target_index`가 기준보다 작다면 앞에서부터 가깝고, 기준보다 크다면 뒤에서부터 세는편이 더 빠르다.

![](https://images.velog.io/images/abcd8637/post/3cd416f8-6811-4451-9327-757f3ffe5c09/KakaoTalk_Photo_2021-06-25-11-02-45.jpeg)

```python
n = 10
arr = [i for i in range(1, n+1)]
target_index = 3 # 4

if arr.index(target_index) <= len(arr) // 2:
    print(f'front가 더 가깝습니다. 앞쪽과의 거리 = {arr.index(target_index)+1}, 뒤쪽과의 거리 = {len(arr) - (arr.index(target_index)+1)}, 앞 / 뒤를 나누는 거리 = {len(arr) // 2}')
else:
    print(f'back 더 가깝습니다. 앞쪽과의 거리 = {arr.index(target_index)+1}, 뒤쪽과의 거리 = {len(arr) - (arr.index(target_index)+1)}, 앞 / 뒤를 나누는 거리 = {len(arr) // 2}')

👉🏽 front가 더 가깝습니다. 앞쪽과의 거리 = 3, 뒤쪽과의 거리 = 7, 앞 / 뒤를 나누는 기준 = 5
```

---
## 📍 python에서 음의 정수를 floor 해보기

<a href='https://programmers.co.kr/learn/courses/30/lessons/42586'>프로그래머스 - 기능개발</a> 문제에서 전처리 과정 중 `100 - progress[x] // speeds[x]`을 해야하는 과정이 있었는데 나는 나머지가 `있는 / 없는` 조건을 사용하여 해결했으나 `math.floor` 혹은 `//`를 사용하여 해결한 다른 사람의 코드를 봤다.

바로 음수 `floor`를 사용한것인데, 지금까지 양수 `floor`만 사용해봤어서 음수는 어떤 원리로 계산되는지 궁금했다. 

먼저 `floor`의 <a href='https://docs.python.org/3/library/math.html?highlight=floor#math.floor'>정의(공식문서)</a>는 다음과 같다.
`the largest integer less than or equal to x` 직역하면 `x보다 작거나 같은 가장 큰 정수`를 뜻하는데, 말로만 설명해서는 이해가 잘 되지 않을 수 있으니까 예시를 살펴보자. (하단 코드 참고)

```python
from math import floor

# 양수 floor
print(floor(2))
print(floor(2.00001))
print(floor(2.99999))
👉🏽 2

# 음수 floor
print(floor(-2.0001))
print(floor(-2.9999))
print(floor(-3))
👉🏽 -3
```

양수일때는 `현재 값보다 작거나 같은 가장 큰 정수`는 2인것을 알 수 있다. 같은 값인데도 불구하고 음수의 경우에는 왜 `-2` 대신 `-3`이 나올까?? 예를들어 `-7 // 2`연산을 해보자. 한번에 `floor`처리를 하면 헷갈릴 수 있으므로 다음의 순서를 생각하며 계산하면 쉽다.

1. `-7 / 2 = -3.5` 
2. `floor`처리(`x보다 작거나 같은 가장 큰 정수`)를 한다.
3. `- 7 // 2 = -4`가 된다.

더 자세한 설명은 <a href='https://stackoverflow.com/questions/37283786/floor-division-with-negative-number'>스택오버플로우1</a>, <a href='https://stackoverflow.com/questions/19517868/integer-division-by-negative-number'>스택오버플로우2</a>를 참고하자.

번외로, 각 언어마다 정수 나누기를 수행할 때 `양의 무한대` 혹은 `음의 무한대`로 반올림하는 경우가 다르다. `c`는 양의 무한대로 반올림되는 반면, `python`과 `ruby`에서는 음의 무한대로 반올림된다.

다음은 각 언어별 음의 정수 나누기 결과표이다.

| Language| Code | Result |
|:---:|:---:|:---:|
| ruby      | -1 / 5         |     -1 |
| python    | -1 / 5         |     -1 |
| c         | -1 / 5         |      0 |
| clojure   | (int (/ -1 5)) |      0 |
| emacslisp | (/ -1 5)       |      0 |
| bash      | expr -1 / 5    |      0 |

출처: <a href='https://stackoverflow.com/questions/19517868/integer-division-by-negative-number'>스택오버플로우</a>

결론: `python`에서 `음의 정수의 나눗셈`은 `음의 무한대`로 반올림한다.

---
## 📍 절사평균과 round(반올림) 함수
<a href='https://ko.wikipedia.org/wiki/%EC%A0%88%EC%82%AC%ED%8F%89%EA%B7%A0'>절사평균 - 위키피디아</a> 란, 편차가 큰 자료의 경우 산술평균이 적합하지 않으므로 자료의 총 개수에서 일정비율만큼 가장 큰 부분과 가장 작은부분을 제거 후 평균을 산출한다. 

예를들어, `15%의 절사평균`을 구한다고 하면 전체 값의 상위 `5 * 0.15 = 0.75`, 하위 `5 * 0.15 = 0.75`개 만큼 제외 후 평균을 구한다는 뜻이다. (문제에 따라 소수점으로 나오게 되면 반올림을 하거나 하지 않는경우가 있기 때문에 반올림하지 않고 소수점으로 놔뒀다.)

주어진 표본집단 `arr`에서 `15% 절사평균`을 구한다고 가정하면 (소수점일때 반올림한다.) `python`에서 다음과 같이 작성 할 수 있다. 이때 `slicing`을 2가지 방법으로 구현했다.

```python
n = 5
arr = [10, 20, 30, 40, 50]

trunc = round(n * 0.15)    # 1, 앞 뒤로 1개씩 제외시키기

print(arr[trunc: -trunc])    # arr[1:-1]
👉🏽 [20, 30, 40] 

print(arr[trunc: n-trunc])    # arr[1:4]
👉🏽 [20, 30, 40]
```

여담으로, 알고리즘 문제(예: <a href='https://www.acmicpc.net/problem/18110'>boj_18110 - solved.ac</a>)에서 위와 같은 로직으로 제출하면 오답판정을 받는데 왜냐하면 `python`에서 `round` 함수를 사용할 때 우리가 알고있는 반올림 형태인 4사 5입(`4` 이하는 버리고 `5` 이상부터 반올림)이 아니라 5사 5입(`ROUND_HALF_EVEN` or `round_to_nearest_even`: 앞자리가 홀수면 올리고 앞자리가 짝수면 버리는 방법)을 기반으로 실행되기 때문이다. 

공학이나 자연과학에서 `5사 5입` 방법을 많이 사용하는데 맨 뒷자리가 필연적으로 손실되는 계산 특성상 오사오입으로 처리하는 것이 오차가 가장 적기 때문이다. 추가적인 내용이 궁금하다면 <a href='https://docs.python.org/ko/3.6/tutorial/floatingpoint.html'>부동 소수점의 문제점과 한계(python.org)</a>를 살펴보자.

5사 5입(`ROUND_HALF_EVEN` or `round_to_nearest_even`)의 예시는 다음과 같다. 

```python
print(round(0.5))    # 0
print(round(1.5))    # 2
print(round(2.5))    # 2
print(round(3.5))    # 4
print(round(4.5))    # 4
print(round(5.5))    # 6
```

결론적으로 부동소수점을 반올림을 할 때 우리가 평소에 사용하는 십진법으로 계산하고 싶다면 `직접 함수를 만들거나`, `decimal` 라이브러리를 이용해야하는데 다음과 같이 사용하자.

```python
# 함수 만들기
def round2(num):
    return int(num) + (1 if num - int(num) >= 0.5 else 0)

print(round2(0.5))    # 1
print(round2(1.5))    # 2
print(round2(2.5))    # 3
print(round2(3.5))    # 4
print(round2(4.5))    # 5
print(round2(5.5))    # 6

# decimal 라이브러리 사용
from decimal import Decimal
value = Decimal('0.1') * Decimal('0.1')

print(value)
👉🏽 0.01
```

여담이지만, 두 실수가 같은지 판단하려면 `==` 대신 `math.isclose` 혹은 `sys`를 이용해서 확인 할 수 있다. 참고로 `sys.float_info.epsilon`에 저장된 값은 머신 앱실론(machine epsilon)이라고 부르는데, 어떤 실수를 가장 가까운 부동소수점 실수로 반올림 했을 때 상대 오차는 항상 머신 앱실론 이하다. 그래서 두 값이 같은지 다른지를 비교하려면 비교대상을 머신 앱실론으로 정하고 이보다 작거나 같으면 `True` 처리가 된다.

또, `python 3.5` 이상부터는 `math_isclose` 함수를 사용하여 비교 할 수도 있다.

```python
# epsilon 사용
import math, sys

x = 0.1 + 0.2
print(math.fabs(x - 0.3) <= sys.float_info.epsilon)
👉🏽 True

print(sys.float_info.epsilon)
👉🏽 2.220446049250313e-16    # epsilon 값

# math.isclose 사용
print(math.isclose(0.1 + 0.2, 0.3))
👉🏽 True
```

>reference: 
1. <a href='https://m.blog.naver.com/PostView.nhn?blogId=herbdoc95&logNo=221574077380&proxyReferer=http:%2F%2Fblog.naver.com%2FPostView.nhn%3FblogId%3Dherbdoc95%26logNo%3D221574077380'>naver-blog</a>
2. <a href='https://docs.python.org/ko/3/library/decimal.html'>python - decimal 라이브러리</a>
3. <a href='https://dojang.io/mod/page/view.php?id=2466'>코딩도장</a>

---
## 📍 2차원 행렬 시계방향으로 한 칸씩 회전하기

카카오 코딩테스트를 보다가 2차원 행렬을 시계방향으로 회전하라길래 <a href='https://ywtechit.tistory.com/169'>저번</a>에 <a href='https://www.acmicpc.net/problem/16935'>배열돌리기 3</a> 문제를 풀어본 경험이 있어 풀 수 있을것 같았는데 못 풀었다. 😂 😂 눈물을 머금으며 다음엔 꼭 풀겠다는 취지로 글을 남긴다.

이번에는 `90도` 회전이 아닌 `시계방향` 혹은 `반시계방향`으로 한칸씩 이동하는 방법을 배워보려고 한다. 이때 전체 범위를 회전하지 말고 주어진 범위 내에서 테두리의 값만 이동하자. 다음과 같이 `5*5`행렬이 있을 때 파란색 빗금 친 범위만 시계방향으로 바꾸려고 한다.

![](https://images.velog.io/images/abcd8637/post/a5ea5486-01c1-4fcc-97f5-69b3967723e6/KakaoTalk_Photo_2021-07-15-09-53-27.jpeg)

처음 로직을 구현할 때 `dx`, `dy`를 이용해서 옮길 좌표를 우측으로 한 칸 혹은 아래쪽으로 한 칸 이렇게 짜는 줄 알았더니 `dx`, `dy`는 사용하지 않고, 범위를 설정해서 `row+1` 혹은 `column+1` 을 해주는 방법을 사용해야한다.

![](https://images.velog.io/images/abcd8637/post/a8459017-0f51-43d9-aac2-62d9be85f4b1/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3.jpeg)

순서는 다음과 같다.
1. 우리가 퍼즐을 맞출 때 한 칸을 따로 빼두고 진행하는것처럼 배열에서 `temp`에 저장 할 값 1개를 빼둔다. (그래야 빼둔칸으로 한 칸씩 밀어 올릴 수 있다. 나는 `temp`를 `7`로 정했다.)
2. 시계방향으로 움직인다고 해서 `temp`를 기준으로 시계방향으로 이동하는 것이 아니라 우리는 반 시계방향으로 값을 하나씩 이동시켜준다. 여기서 중요한 포인트는 한 반복문에서 값을 이동시킬 때 맨 마지막 값은 그대로 남아있다는것이다. (이 포인트를 생각하지못해서 감을 못 잡았었다.)
3. 반복문의 범위는 이동시키려고 하는 값의 반대 방향으로 선언해야한다. (1번과 2번은 `linear`, 3번과 4번은 `reverse`)
4. 하단 그림의 4번까지 끝내고나서 `temp`는 맨 처음 `temp` 위치에서 `column + 1` 값에 넣어준다. (반시계방향이면 `row-1`이겠지??)

![](https://images.velog.io/images/abcd8637/post/fa782f40-c580-4881-9989-253450aafe9a/KakaoTalk_Photo_2021-07-15-10-05-36.jpeg)

```python
row, column = 5, 5
queries = [[2, 2, 4, 4]]    # x1, y1, x2, y2 (x1, y1 부터 x2, y2 범위)

arr = [[0] * column for _ in range(row)]
cnt = 0

for i in range(row):
    for j in range(column):
        cnt += 1
        arr[i][j] = cnt

for t, l, b, r in queries:
    top, left, bottom, right = t - 1, l - 1, b - 1, r - 1    # index 계산을 편하게 하기 위해서 빼준다.
    temp = arr[top][left]

    for k in range(top, bottom):    # 1번
        arr[k][left] = arr[k + 1][left]
 
    for k in range(left, right):    # 2번
        arr[bottom][k] = arr[bottom][k + 1]

    for k in range(bottom, top, -1):    # 3번
        arr[k][right] = arr[k - 1][right]

    for k in range(right, left, -1):    # 4번
        arr[top][k] = arr[top][k - 1]

    arr[top][left + 1] = temp    # temp 넣기

    for i in arr:
        print(*i, end=' ')
        print()

👉🏽
1 2 3 4 5 
6 12 7 8 10 
11 17 13 9 15 
16 18 19 14 20 
21 22 23 24 25 
```

---
## 📍 공백으로 들어온 int를 공통으로 빼주기
예를들어 공백으로 들어온 입력을 전체 `-1`처리를 해줘야 한다면, 두가지 방법이 있을 것이다.

1. 입력을 모두 받고나서 `-1` 해주기
2. 입력을 받을 때마다 `-1` 해주기

결론적으로 같은 출력이지만 조금이나마 코드를 간결하게 작성할 수 있기 때문에 `lambda` 함수를 사용해 입력을 `int`로 바꾸면 2번처럼 사용할 수 있다. 다음의 코드를 참고하자.

```python
# 입력: 1 2

# 방법 1
temp_a, temp_b = map(int, input().split())
a, b = temp_a-1, temp_b-1
print(a, b)
👉🏽 0 1

# 방법 2
a, b = map(lambda x: int(x)-1, input().split())
print(a, b)
👉🏽 0 1
```