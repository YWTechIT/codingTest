## implementation(구현)
머릿속으로는 잘 떠오르지만 막상 코드로 작성하면 잘 떠오르지 않는 문제들

## 📍 list를 str로 변환하기
```python
array = ''.join([str(_) for _ in range(10)])
char = ''.join([chr(i) for i in range(65, 71)])

👉🏽 '0123456789'
'ABCDEF'

```

---

## 📍 pass, continue, break
```python
# pass
for i in range(10):
    if i % 2 == 0:
        pass
        print(i)
    else:
        print('나머지')
👉🏽 0
나머지입니다.
2
나머지입니다.
4

# continue
for i in range(5):
    if i % 2 == 0:
        continue
        print(i)
    else:
        print('나머지')
👉🏽 나머지입니다.
나머지입니다.

# break
for i in range(5):
    if i % 2 == 0:
        break
        print(i)
    else:
        print('나머지')
👉🏽 빈 화면
``` 
> 1. pass: 조건문에서 넣어줄 조건이 딱히 없을경우
> 2. continue: 해당 조건을 건너 뜀
> 3. break: 해당 반복문 자체를 멈춤

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

## 📍 입력마다 최대값을 갱신할 때
```python

max_index = 0
index = 0

for i in range(1, 10):
    number = int(input())
    if number > max_index:
        max_index = number
        index = i
print(max_index)
print(index)
👉🏽 85
8
```
---

## 📍 리스트 내부 인덱스에 접근하기
```python
array = [1, 2, 3, 4, 5]
print(array.index(2))
👉🏽 3
```
---

## 📍 리스트컴프리헨션을 이용한 i제곱
```python
import sys
sys.stdin.readline
array = [i*i map(int, input().split())]
print(sum(array)%10)
```
---

## 📍 중복되는 문자열 정렬
```python
# 만약, list(array)와 중복된 단어를 정렬한 array와 같다면 count+=1
n = int(input())
for i in range(n):
    array = input()
    if list(array) = array.sorted(array, key=array.find):
        count+=1
```
---

## 📍 array[i] == array[i+1] 범위 설정
```python
# 1번
for i in range(len(array)):
    if i < len(array) -1 and array[i] == array[i+1]:

# 2번
for i in range(len(array)):
    if i != len(array) -1 and array[i] == array[i+1]:
```
---

## 📍 이중반복문 내부 숫자배열
반복문 1개당 시간복잡도: O(N)

```python
array = 'scv'
for i in range(3):
    for j in range(len(array)):
        print(i)
👉🏽 0 0 0 1 1 1 2 2 2 (s s s c c c v v v)

for i in range(3):
    for j in range(len(array)):
        print(j)
👉🏽 0 1 2 0 1 2 0 1 2 (s c v s c v s c v)
```

---

## 📍 백준 1152 - 단어의 개수
<a href='https://www.acmicpc.net/problem/1152'>백준 1152 - 단어의 개수</a>

### ⚡️ 나의 풀이

주어진 문자열에서 단어의 개수를 찾고 싶을 때는 띄어쓰기를 기준으로 나누고 + 1을 해주면된다.

예외상황으로 문자열의 제일 앞, 뒤는 `strip()` 함수를 사용해서 공백을 제거해준다.

그리고, `input=' '` 공백일때를 고려해서 공백이라면 print(0) 아니면 `cnt+=1`을 하는 코드를 작성했다.

```python
array = input().strip()

if len(array) == 0:
    print(0)
else:
    print(array.count(' ')+1)
```

---

## 📍 백준 2675 - 문자열 반복
<a href='https://www.acmicpc.net/problem/2675'>백준 2675 - 문자열 반복</a>

### ⚡️ 나의 풀이

시간복잡도를 최소화하기 위해 반복문도 최소화선언

```python
# 1번
T = int(input())

for i in range(T):
    case = input().split()
    n, s = int(case[0]), list(case[1])
    for j in range(len(s)):
        for k in range(n):
            print(s[j], end='')
    print()

# 2번 
T = int(input())

for i in range(T):
    n, s = input().split()
    for j in range(len(s)):
        print(int(n) * s[j], end='')
    print()

```

---

## 📍 백준 8958 - OX 퀴즈

<a href='https://www.acmicpc.net/problem/8958'>백준 8958 - OX퀴즈</a>

### ⚡️ 나의 풀이

첫 번째 반복문이 종료되면, `cnt, sum` 변수들을 초기화시켜야한다.

연속되는 숫자는 `sum+=1`, 연속되지 않는 숫자를 만나면 `cnt=1`로 초기화 시키기.

```python
'''
5
OOXXOXXOOO
OOXXOOXXOO
OXOXOXOXOXOXOX
OOOOOOOOOO
OOOOXOOOOXOOOOX
'''

import sys

input = sys.stdin.readline
T = int(input())

for _ in range(T):
    quiz = input()
    cnt = 0
    result = 0
    for i in range(len(quiz)):
        if quiz[i] == 'O':
            cnt += 1
            result += cnt
        else:
            cnt = 0
    print(result)
👉🏽 10 9 7 55 30
```
---

## 📍 백준 11721 - 열 개씩 끊어 출력하기

<a href='https://www.acmicpc.net/problem/11721'>백준 11721 - 열 개씩 끊어 출력하기</a>

### ⚡️ 나의 풀이

for문에 몇 개씩 끊어 출력하도록 기준을 잡을 수 있다.

```python
# 내가 푼 코드
import sys
input = sys.stdin.readline
s = input()

for i in range(len(s)):
    if i < 10:
        print(s[i],end='')
    elif i % 10 == 0:
        print()
        print(s[i], end='')
    else:
        print(s[i], end='')
```

```python
# 다른 사람이 푼 코드
import sys
input = sys.stdin.readline
s = input()

for i in range(0, len(s), 10):
    print(s[i:i+10])
```

---
## 📍 백준 1977 - 완전 제곱수

<a href='https://www.acmicpc.net/problem/1977'>백준 1977 - 완전 제곱수</a>

### ⚡️ 나의 풀이

완전제곱수를 만들 때는 root만 계산하면 되는줄 알았는데, 반례가있기 때문에 다시 제곱을 취해줘야한다는것을 처음 알았다.

그리고 root를 취할 때 `math.sqrt` 대신 `i ** 0.5`를 하면 간편하게 계산 할 수 있다. (이것도 처음 알았다.)

>1. first = int(i ** 0.5)
  * 처음 수를 root를 취하자(i^0.5)
>2. second = first ** 2
  * first에 다시 거듭제곱(i^2) 

굳이 while문을 사용하지 않아도된다.
만약, append값이 없으면 `( num == [] )`과 같이 사용한다.
 
```python
m = int(input())
n = int(input())

num = []
for i in range(m, n+1):
    root = int(i ** 0.5)
    if i == root ** 2:num.append(i)

if num == []:
    print(-1)
else:
    print(f'{sum(num)}\n{min(num)}')
```
---
## 📍 백준 4673 - 셀프 넘버

<a href='https://www.acmicpc.net/problem/4673'>백준 4673 - 셀프넘버</a>

### ⚡️ 나의 풀이

int형을 str로 바꿔 계산하자. 
조건에 n이 10000까지기 때문에 for문의 범위를 10001로 설정했다.

문제를 풀다가 잘 안풀리면 곧장 포기하고 다른 방법으로 풀려는 경향이 있는데, 끈질기게 끝까지 매달리는 능력을 길러야겠다.

```python
def d(n):
    result = 0
    for i in str(n):
        result = result + int(i)
    return result + int(n)

a=[]
for j in range(1, 10001):
    n = d(j)
    a.append(n)

for k in range(1,10001):
    if k not in a:
        print(k)
```
---

## 📍 백준 2577 - 숫자의 개수

<a href='https://www.acmicpc.net/problem/2577'>백준 2577 - 숫자의 개수</a>

### ⚡️ 나의 풀이
어제 풀었던 문제와 동일하게 입력 받은수를 `str`로 변환하여 풀면 되는 문제였다.
`string.count()` 함수를 사용 할 생각을 안하고 또 `cnt+=1`로 풀려고해서 잠깐 먼 여정을 떠날 뻔 했다..😅

비슷한 패턴이 떠올라 뒤져보던 찰나 `count()`함수가 떠올라서 작성했고 정답 판정을 받았다.

기억하자! `str`형태면 `count()`를 사용할수 있다는것을...

```python
A = int(input())
B = int(input())
C = int(input())

n = A*B*C

for i in range(10):
    print(str(n).count(str(i)))
```
---



