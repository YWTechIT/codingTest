## 입출력(input(), sys.stdin())

`python`에서 입력을 받을 때 주로 `input()`을 사용한다.
하지만, 많은 수의 입력을 받을 때 `input()`을 사용하면 동작시간이 느려 시간초과로 오답 판정을 받을 수 있다.

이 때는 파이썬 `sys` 라이브러리에 정의되어 있는 `sys.stdin.readline()` 함수를 이용하자.

현재까지 정의되어있는 `입출력` 동작 순서는 다음과 같다.

> `sys.stdin.readline() > raw_input() > input()`

`sys.stdin.readline()`은 한 줄의 문자열을 반환하는데 이것을 `int()`로 묶어서 정수로 변환하는것이 더 빠르다.
`raw_input()`은 문자열을 반환한다.
`input()`은 `raw_input()`을 `evaluate`한 결과를 반환한다.

* `input()`에서 값을 입력받으면 `str형`, `list`에서 `''`없이 사용 시 `int형`

출처: <a href='https://www.acmicpc.net/board/view/855'>백준</a>

---

### 📍 input()값을 한 문자씩 바꿀 때
```python
array = input()
result=list(array)
print(result)
👉🏽 ['a', 'r', 'r', 'a', 'y']
```
---

### 📍 한 줄, 여러 줄

```python
# 한 줄 입력 받을 때
import sys
array = list(map(int, sys.stdin.readline().split()))

# 여러 줄 입력 받을 때
import sys
for line in sys.stdin:
    print(line)

# 여러개의 테스트케이스일때
while True:
    a, b = map(int, input().split())
    if a == 0 and b == 0:
        break
    else:
        print(a+b)
```

---

### 📍sys.stdin.readline()
입력한 한 라인을 `interable`에 저장한다.
`띄어쓰기`와 `\n`까지 포함하므로 `split()`을 이용하자.

중간에 `.rstrip()` 붙이는 경우가 많은데 공백을 제거할때 사용하는 함수다. 
보통, 문자열 자체에 변수를 저장하고 싶을 때 많이 사용하지만, `int`, `split()`을 그대로 사용할 수 있다.
즉, `int(sys.stdin.readline())`, `int(sys.stdin.readline().split()` 와 같은 말이다.
쉽게 표현하고 싶으면 input_data = sys.stdin.readline()을 사용하여 코드를 간결하게 하자.

---
## 📍 출력 형태
```python
# sep
print('abcd8637', 'naver.com', sep='@')
👉🏽 abcd8637@naver.com
print('2021', '2', '21', sep='.')
👉🏽 2021.2.21
``` 

```python
# end
print('%s' %('My name is'), end=' ')
print('%s' %('Yeongwoo An'), end=' ')
print('%s' %("What's your name?"))
👉🏽 My name is Yeongwoo An What's your name?
```

```python
# format
print('{a} and {b}' .format(a='here', b='there'))
print('{} 과 {}' .format(1, 2))
print('{0} and {1} and {0}'. format(1,2))
print("%s's number is %d" %('yeongwoo', 7) )
👉🏽 here and there
1 과 2
1 and 2 and 1
yeongwoo's number is 7
```

```python
'''
arr = [1, 2, 3, 4]
'''

print(*arr)
👉🏽 1 2 3 4
```

---
## 📍 원하는 만큼 입출력을 받고 싶을 때
```python
n, m = map(int, input().split())

for i in range(n):
    data = list(map(int, input().split()))

👉🏽 입력: 3 3 
1 1 
2 2 
3 3

출력: [3, 3]
```
---

## 📍 입력 테스트케이스만큼 계산 및 출력할 때
```python
# T = 테스트케이스
# n, m만큼 횟수를 입력받는다.
# n번째 테스트케이스 계산이 끝나면 출력

T = int(input())

for i in range(T):
    n, m = map(int, input().split())
    for j in range(e):
        a, b = map(int, input().split())
        print(a)
```

---

## 📍 임의의 개수의 정수를 리스트에 저장할 때
```python
# sys.stdin 
import sys
n = int(input())

array = []

for i in range(n):
    matrix.append(list(map(int,sys.stdin.readline().split())))

print(matrix)
```

```python
# input()

n = int(input())

array = []

for i in range(n):
    matrix.append(input().split())

print(matrix)
```
---

## 📍 각각의 입력을 한 곳에 저장하기
```python
'''
5
10 -1
10 1 -1
4 1 -1
4 3 1 -1
3 3 -1
'''
# 첫번째 수마다 시간 정보를 담고 있음
time = [0] * (n+1)

for i in range(1, n+1):
    array = list(map(int, input().split()))
    time[i] = array[0]
👉🏽 [0, 10, 10, 4, 4, 3]

# [1:-1] 범위를 저장하기
for i in range(1, n+1):
    
    for x in array[1:-1]:
        print(x, end=' ')
👉🏽 1 1 3 1 3 

# `i` 범위 내 [1:-1] 범위 중 해당되는 값만 차수 증가
indegree = [0] * (n+1)

for i in range(1, n+1):
    for x in array[1:-1]:
        indegree[i] = indegree[i] + 1
👉🏽 [0, 0, 1, 1, 2, 1]
```

## 📍 정수와 배열이 한 줄로 들어오는경우
```python
'''
4 10 20 30 40
3 7 5 12
3 125 15 25
'''

N, *arr = map(int, input().split())
print(N)
👉🏽 4

print(*arr)
👉🏽 10 20 30 40
```

---
## 📍 [ list ]에서 중복 값을 제거하기
```python
array = [1, 2, 2, 3, 3, 3, 4, 5, 6]
array_set = list(set(array))
👉🏽 [1, 2, 3, 4, 5, 6]
```
---

## 📍 1차원 배열
```python
n = 5
array = [0] * n
👉🏽 [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
---

## 📍 2차원 배열
```python
# 풀어서 만들기
list1 = []
list2 = []
value = 1

for i in range(4):
    for j in range(3):
        list1.append(value)
        value+=1
    list2.append(list1)
    list1 = []
print(list2)
👉🏽 [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]

for i in list2:
    for j in i:
        print(j, end= ' ')
        result += j
    print()

print(result)
👉🏽 78

# 3행 4열
n = 3
m = 4
array = [[0] * m for _ in range(n)]
print(array)
👉🏽 [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

# 2차원 리스트의 맵 정보 입력받기
graph = []
for i in range(n):
    graph.append(list(map(int, input())))

# 2차원 배열 comprehension으로 받기
n = int(input())
map = [list(map(int, input().split())) for i in range(n)]
print(map)
```

---
## 📍 [list]형을 string형으로 출력 할 때
```python
a, x = map(int, input().split())
result = list(map(int, input().split()))

array = []

for i in result:
    if i < x:
        array.append(i)
print(' '.join(map(str, array)))
```
---

## 📍 각 자리수의 값을 더할 때

```python
numbers = 222
number = str(numbers)
result = 0

# 1번
for i in range(len(number)):
    result = result + int(number[i])
print(result)
👉🏽 6

# 2번
return sum([int(i) for i in str(s)])

# 3번
return sum(list(map(int, str(s))))
```
---

## 📍 n의 배수일 때, 배수가 아닐 때

```python
# n이 4의 배수로 나누어 떨어질 때
n = 12

if n % 4 == 0 
    print('4의 배수입니다.')
elif n % 4 != 0:
    print('4의 배수가 아닙니다.')
```

---
## 📍 원하는 튜플기준으로 출력하고 싶을 때
```python
n = int(input())

array = []
for i in range(n):
    input_data = input().split()
    array.append((input_data[0], int(input_data[1]))

# 점수 기준 sort(오름차순)
array = sorted(array, key = lambda student: student[1])

# 점수 기준 sort(내림차순)
array = sorted(array, key = lambda student: student[1], reverse=True)

for score in array:
    print(score[1], end=' ')

👉🏽 입력
3
이순신 93
장보고 50
문성공 99

👉🏽 출력
50 93 99 (오름차순)
99 93 50 (내림차순)

# 이름 기준 sort(오름차순)
array = sorted(array, key = lambda student: student[0])

# 이름 기준 sort(내림차순)
array = sorted(array, key = lambda student: student[0], reverse=True)

for name in array:
    print(name[0], end=' ')

👉🏽 입력
3
이순신 93
장보고 50
문성공 99

👉🏽 출력
문성공 이순신 장보고 (오름차순)
장보고 이순신 문성공 (내림차순)
```
---

---
## 📍 sorted(key = lambda) 사용
우선순위

1. 식별자를 제외한 문자열 모두를 검사한다.
2. 그럼에도 불구하고 문자열 모두가 동일하다면 식별자를 기준으로 정렬한다.

```python
logs = ["dig1 8 1 5 1", "let1 art can", "dig2 3 6", "let2 own kit dig", "let3 art zero"]

def solution(logs):
    letters, digits = [], []

    for i in logs:
        if i.split()[1].isdigit():
            digits.append(i)
        else:
            letters.append(i)

    letters = sorted(letters, key= lambda x: (x.split()[1:], x.split()[0]))

    return letters + digits
```