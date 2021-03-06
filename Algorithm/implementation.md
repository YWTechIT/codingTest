## implementation(구현)
머릿속으로는 잘 떠오르지만 막상 코드로 작성하면 잘 떠오르지 않는 문제들

구현 유형의 예시
>1. 알고리즘은 간단한데 코드가 지나칠 만큼 길어지는 문제
>2. 실수 연산을 달고, 특정 소수점 자리까지 출력해야 하는 문제
>3. 문자열을 특정한 기준에 따라서 끊어 처리해야하는 문제
>4. 적절한 라이브러리를 찾아 사용해야하는 문제

---
## 💡 [21. 3. 14.]
### ❏ python에서 시간제한이 1초일 때
1. `N < 500`: 최대 O(N^3), 약 1억번
2. `N < 2,000`: 최대 O(N^2), 약 4백만번
3. `N < 100,000`: 최대 O(NlogN)
4. `N < 10,000,000`: 최대 O(N)
* python은 1초에 5천만번의 연산이 가능
* 채점용 서버에서는 1초에 2천만번의 연산을 처리한다고 생각하자.

## 💡 [21. 2. 18.]
모든 케이스를 계산하는것이 완전탐색이다. 
완전탐색을 사용하려면 먼저, 입력 조건을 살펴보자.
일반적인 코딩테스트의 채점 환경에서 1초에 2,000만에서 1억정도의 연산처리가 가능하므로 그 전까지의 경우의 수는 완전탐색으로 살펴보자.

---

## 💡 행렬
프로그래밍에서의 행렬은 대수학의 좌표와는 다른 의미로 사용된다.
![](https://images.velog.io/images/abcd8637/post/95cbace6-5091-4786-924d-c3970983e3ae/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-02-19%2007.50.19.png)

이중 for문에서 `i`는 세로, `j`는 가로라고 생각하면 편하다.

```python
for i in range(5):
    for j in range(5):
        print('(', i, ',', j, ')', end='')
    print()

👉🏽
( 0 , 0 )( 0 , 1 )( 0 , 2 )( 0 , 3 )( 0 , 4 )
( 1 , 0 )( 1 , 1 )( 1 , 2 )( 1 , 3 )( 1 , 4 )
( 2 , 0 )( 2 , 1 )( 2 , 2 )( 2 , 3 )( 2 , 4 )
( 3 , 0 )( 3 , 1 )( 3 , 2 )( 3 , 3 )( 3 , 4 )
( 4 , 0 )( 4 , 1 )( 4 , 2 )( 4 , 3 )( 4 , 4 )
```

완전 탐색 문제에서는 2차원 공간에서의 방향 벡터가 주로 활용된다.

![](https://images.velog.io/images/abcd8637/post/3458cecc-acd7-45e3-b7aa-e9650fb6de85/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-02-19%2007.56.01.png)

```python
# 동북서남
dx = [0, -1, 0, 1]
dy = [1, 0, -1, 0]

# 현재 위치
x, y = 2, 2

# 다음 위치
for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]
    print(nx, ny)

👉🏽 2 3 (동)
1 2 (북)
2 1 (서)
3 2 (남)
```
---

## 💡 1차원 배열을 입력만큼 회전

```python
# slicing 기법
def rotate(arr, n):
    if not arr:
        return 0

    N = len(n)
    n %= N

    left = [:-n]
    right = [-n:]
    return right + left

print(rotate([1, 2, 3, 4, 5], 2))
👉🏽 [3, 4, 5, 1, 2]
```

```python
# for문을 사용한 기법
def rotate(arr, n):
    if not arr:
        return 0

    N = len(n)
    new_arr = [0 for _ in range(N)]
    n %= N

    for i in range(N):
        new_arr[(i % n) % N] = arr[i]
    return new_arr
    
print(rotate([1, 2, 3, 4, 5], 2))
👉🏽 [3, 4, 5, 1, 2]
```
---

## 💡 2차원 배열 90도, 180도, 270도, 360도 회전
```python
def rotate(arr, n):
    N = len(arr)
    new_arr = [[0] * N for i in range(N)]

    # 90도
    if n % 4 == 1:
        for i in range(N):
            for j in range(N):
                new_arr[j][N - 1 - i] = arr[i][j]
    # 180도
    elif n % 4 == 2:
        for i in range(N):
            for j in range(N):
                new_arr[N - 1 - i][N - 1 - j] = arr[i][j]
    # 270도
    elif n % 4 == 3:
        for i in range(N):
            for j in range(N):
                new_arr[N - 1 - j][i] = arr[i][j]
    # 360도
    else:
        for i in range(N):
            for j in range(N):
                new_arr[i][j] = arr[i][j]
    return new_arr

arr = [[0, 0, 0], [1, 1, 1], [0, 0, 0]]
print(rotate(arr, 1))
```
---


---

## 📍 list가 빈 배열인지 확인하는 코드
```python
a = []

if len(a) == 0:
    print(True)
else:
    print(False)
```
```python
if not a:
    print(True)
else:
    print(False)
```
```python
if a == []:
    print(True)
else:
    print(False)
```
---

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

## 📍 최소값 갱신하기
```python
# 방법 1
a = [15, 68, 77, 10, 3]
min_number = a[0]

for i in a:
    if i < min_number:
        min_number = i
print(min_number)
👉🏽 3

# 방법 2
a = [15, 68, 77, 10, 3]
a = sorted(a)
print(a[0])
👉🏽 3

# 방법 3
a = [15, 68, 77, 10, 3]
print(min(a))
👉🏽 3

```
---

## 📍 최대값 갱신하기
```python
# 방법 1
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

# 방법 2
a = [15, 68, 77, 10, 3]
max_number = a[0]

for i in a:
    if max_number < i:
        max_number = i
print(max_number)

# 방법 3
a = [15, 68, 77, 10, 3]
a = sorted(a, reverse=True)
print(a[0])
👉🏽 77

# 방법 4
a = [15, 68, 77, 10, 3]
print(max(a))
👉🏽 77
```
---

## 📍 리스트 값을 번갈아가면서 출력하기
```python
# zip함수 사용
a = [1, 2, 3]
b = [4, 5, 6]

for i, j in zip(a, b):
    print(i, j, end=' ')
👉🏽 1 4 2 5 3 6  
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
## 📍 중복되는 문자열을 없앨 때(서로 다른 값이 몇 개 있는지 확인 할 때)
```python
arr = [int(input()) % 42 for i in range(10)]
print(len(set(arr)))
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

## 📍 2020 카카오 신입 공채 - 문자열 압축

<a href='https://programmers.co.kr/learn/courses/30/lessons/60057?language=python3'>2020 카카오 신입 공채 - 문자열 압축</a>

### ⚡️ 나의 풀이
뭔가 지금까지 배웠던 문자열 개념들을 총 정리? 하는듯했다.
어떤 코드는 다른 문제들을 풀 때 사용했던 코드를 가져온경우도 있다.
이걸 풀고나서 이래서 많은 문제들을 풀어봐야하는구나 라는 생각이 들었다.

문제를 이해하고 막상 풀려니까 코드로는 작성하기 어려웠다.
이 문제는 <a href = 'https://www.youtube.com/watch?v=jaPH3GLbqfw&list=LL&index=9&t=636s'>유튜브 - 우리밋강의</a>님께서 설명하신대로 푸니까 이해가 잘 됐다.
개인적으로 정규표현식은 잘 사용하지 않았는데, 정규표현식을 통해 문제를 푸니까 신기했다.
나중에 비슷한 문제가 나왔을 때, 문자열을 n씩 쪼개는 코드는 정규표현식을 통해 간단하게 풀 수 있겠다.

```python
import re

def solution(s):
    result_count=[]
    for i in range(1, len(n) // 2 + 1):
        reList = re.sub('(\w{%i})' % i, '\g<1> ', n).split()
        cnt = 1
        result = []
        print(reList)
        for j in range(len(reList)):
            if j < len(reList) -1 and reList[j] == reList[j+1]:cnt+=1
            else:
                if cnt == 1:
                    result.append(reList[j])
                else:
                    result.append(str(cnt) + reList[j])
                    cnt = 1
        result_count.append(len(''.join(result)))
    print(min(result_count))
```
---

## 📍 백준 2920 - 음계

<a href='https://www.acmicpc.net/problem/2920'>백준 2920 - 음계</a>

### ⚡️ 나의 풀이
처음에 `c d e f g a b C`를 각각 1, 2, 3 ... 8의 숫자로 변경한다고 써있길래 `ord()`함수를 사용하여

>1. `c ~ g`까지는 ord(i) - 98
>2. `a ~ b`까지는 ord(i) - 91
>3. `C`는 ord(i) - 59
라는 조건을 세워 1~8까지 나오게 만들어야하나?라고 생각했는데, 예제 입력을 보니까 알파벳이 아닌 숫자가 들어갔다.

곰곰이 생각하다가 그럼, `result = [1, 2, 3, 4, 5, 6, 7, 8`을 선언하고 
>1. result와 같을 때
>2. result[::-1]와 같을 때
>3. else일 때
로 풀면안되나? 했는데 정답판정을 받았다. 😃 😃
더욱 간단하게 푸는 방법을 찾아 좋았다.

```python
n = list(map(int, input().split()))
result = [1, 2, 3, 4, 5, 6, 7, 8]

if n == result:
    print('ascending')
elif n == result[::-1]:
    print('descending')
else:
    print('mixed')
```

---
## 📍 코드업 2920 - 음계

<a href='https://codeup.kr/problem.php?id=6082'>코드업 6082 - 3 6 9 게임이 왕이 되자</a>

### ⚡️ 나의 풀이
`1부터 n+1`범위에서 `3, 6, 9`가 들어간 수가 있으면 `X`로 표현하는 문제인데, 2가지 방법으로 나눠서 풀었다.
>1. i를 10으로 나눴을때의 나머지를 3, 6, 9로 설정할 때
>2. i를 str()형으로 바꾸고 3, 6, 9를 포함할 때

```python
# 1번
n = int(input())

for i in range(1, n+1):
    if i % 10 == 3 or i % 10 == 6 or i % 10 == 9:
        print('X', end=' ')
    else:
        print(i, end= ' ')

# 2번
n = int(input())

for i in range(1, n+1):
    if '3' in str(i) or '6' in str(i) or '9' in str(i):
        print('X', end=' ')
    else:
        print(i, end=' ')
```

---
## 📍 코드업 2442 - 별 찍기 5

<a href='https://www.acmicpc.net/problem/2442'>백준 2442 - 별 찍기5</a>

### ⚡️ 나의 풀이
올바르게 제출했다고 생각하는데 오답판정을 받았다. 왜냐하면 '*'뒤는 값이 없어야하는데 공백으로 채워진 '값'으로 처리됐기 때문이다. 

`formatting` 함수로 구현했는데, `formatting`함수는 값 앞뒤를 모두 공백으로 채워준다. 따라서 값 앞에만 공백으로 채워주자.

```python
n = int(input())
for i in range(1, n+1):
    print(' ' * (n-i) +'*'*((2*i)-1))
```

---
## 📍 코드업 2445 - 별 찍기 8

<a href='https://www.acmicpc.net/problem/2445'>백준 2445 - 별 찍기8</a>

### ⚡️ 나의 풀이
![](https://images.velog.io/images/abcd8637/post/521387a0-7df6-4aac-bc79-b2f7fc013a7a/KakaoTalk_Photo_2021-03-16-09-27-06.jpeg)

예제 출력에서 가로로 2등분하고 풀면 쉽게 접근할 수 있다.
2등분했다는 이야기는 결국 반복문이 총 2개 사용된다는 이야기다.

여기서 세로로 2등분을 또 해보자.
이전의 별 찍기 문제들의 패턴과 유사한 모양들이 나온다.

패턴사이에 있는 공백을 생각해보자.
1번패턴을 보면 출력뒤에 공백이 존재한다는 점을 알 수 있다.
이전에 풀었던 별찍기 1, 2, 3을 보면 출력뒤에 공백이 존재하지 않는다.

이제 공백을 어떻게 줄건지 생각해보자.
공백이 자릿수만큼 정해진것이 아니고 i가 증가할때마다 공백이 줄어드는것을 볼 수 있다.

이를 코드로 구현하면
`'*' * i + ' '*(n-i)`가 될것이고 이를 반대로 작성하면 2번패턴이 될 수 있다.

가로로 2등분을 했으니까 반복문의 범위를 거꾸로해서 작성하면 예제출력과 일치한다.

```python
n = int(input())

for i in range(1, n+1):
    print(('*'*i) + ' '*(n-i) + ' '*(n-i) + ('*'*i))

for j in range(n-1, 0, -1):
    print(('*'*j) + ' '*(n-j) + ' '*(n-j) + ('*'*j))
```

