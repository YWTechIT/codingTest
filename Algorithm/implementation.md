## difference of python 3.5 to 3.6
1. f-strings : 새로운 종류의 문자열 리터럴 사용가능
2. keep order dict: 딕셔너리 순서 유지 
3. defaultdict: python 3.3부터 사용가능

reference: <a href='https://docs.python.org/3/whatsnew/3.6.html'> python 공식문서 </a>

---
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
## 📍 코드업 6082 - 3 6 9 게임이 왕이 되자

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
## 📍 백준 2442 - 별 찍기 5

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
## 📍 백준 2445 - 별 찍기 8

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

---
## 📍 백준 20053 - 최소, 최대 2

<a href='https://www.acmicpc.net/problem/20053'>백준 20053 - 최소, 최대2</a>

## ⚡️ 나의 풀이
주어진 테스트 케이스만큼 `while`문을 사용하여 각 케이스마다 입력을 받아 최소, 최대 값을 출력하게 만들었다.

```python
import sys
input = sys.stdin.readline
T = int(input())

while T:
    N = int(input())
    arr = list(map(int, input().split()))
    print(min(arr), max(arr))
    T -= 1
```

---
## 📍 백준 5597 - 과제 안 내신 분..?

<a href='https://www.acmicpc.net/problem/5597'>백준 5597 - 과제 안 내신 분..?</a>

## ⚡️ 나의 풀이
두 가지 방법으로 풀었는데
1. 입력값을 `list`로 만들어 반복문을 선언하고 해당 i가 전체 범위인 `students`안에 있는지 확인하고 없는 값들을 출력하게 만들었다.
2. 전체범위와 입력값을 모두 `set`형으로 선언한뒤 서로 빼주고 `sorted`했다. 

문제를 자세히 보면 `제출하지 않은 학생의 출석번호 중 가장 작은 것`을 출력하라고 되어있는데, 문제 의도는 1번보다는 2번 코드에 더 가깝다고 볼 수 있다. 왜냐하면 `sorted`를 사용해서 작은 수부터 출력하기 때문이다.

```python
# case 1
students = list(range(1, 31))
report = [int(input()) for i in range(28)]
print('\n'.join(map(str, [i for i in students if i not in report])))

# case 2
students = list(range(1, 31))
report = sorted(int(input()) for i in range(28))
result = set(students) - set(report)
print('\n'.join(map(str, sorted(result))))
```

---
## 📍 백준 20546 - 🐜 기적의 매매법 🐜

<a href='https://www.acmicpc.net/problem/20546'>백준 20546 - 🐜 기적의 매매법 🐜</a>

## ⚡️ 나의 풀이
문제가 생각보다 긴데, 다른 알고리즘 개념은 필요하지 않고 `구현`에 집중한 문제다.
`solved.ac`에서는 `브론즈 2`라고 나와있는데, 나의 구현 실력은 아직 🥉 인가보다.. 푸는데 꽤 시간이 걸렸다.
구현문제를 많이 풀어보면서 감을 익혀야겠다.

준현이와 성민이의 변수를 각각 선언했다. 준현이의 경우는 조금만 생각하면 금방 구할 수 있는데, 성민이의 경우 `3일 연속 전일 대비 상승, 하락` 부분이 힘들었다. 이 부분을 잘 구현하면 쉽게 풀 수 있는 문제다.

각각의 계산 방법들을 알아보자.
1. 준현: 주식을 살 수 있다면 즉시 매수하기 때문에 현재 `j_cash`가 `i`보다 큰지 확인하고 크다면 새로운 변수 `j_stock`에 `j_cash // i`값을 누적시킨다. 주식을 사고 남은 잔돈(나머지(%))은 이전에 갖고있던 `j_cash`에 누적시킨다.
2. 성민: 인덱스 3개를 동시에 비교해서 전일대비상승과 전일대비하락을 나눈다. 전일대비상승이면 전량 매도하기 때문에 `현재 주식 가격 * 보유 주식 수`을 남은 현금에 누적시켜주고 반대로 전일대비하락이면 전량 매수하기 때문에 현재 보유 주식에 `남은 현금 // 현재 주식가격`을 해주고 남은 잔돈에 `주식을 구매한 나머지`를 누적시켜주면 된다.

```python
input_money = int(input())
machine_duck = list(map(int, input().split()))

j_cash, s_cash = input_money, input_money    # init current cash
j_stock, s_stock = 0, 0    # init current stock

for i in machine_duck:    # calculate joonhyun
    if j_cash >= i:
        j_stock += j_cash // i
        j_cash %= i

for i in range(len(machine_duck) - 3):    # calculate sungmin
    if machine_duck[i] > machine_duck[i+1] > machine_duck[i+2]:    # Decreased compared to the previous day (All buy)
        s_stock += s_cash // machine_duck[i+3]
        s_cash %= machine_duck[i+3]

    elif machine_duck[i] < machine_duck[i+1] < machine_duck[i+2]:    # Increased compared to the previous day (All sell)
        s_cash += s_stock * machine_duck[i+3]
        s_stock = 0

j_asset = [j_cash + (machine_duck[-1] * j_stock)]    # joonhyun profit rate
s_asset = [s_cash + (machine_duck[-1] * s_stock)]    # seongmin profit rate

if j_asset > s_asset:
    print('BNP')
elif j_asset < s_asset:
    print('TIMING')
else:
    print('SAMESAME')
```

---
## 📍 백준 1453 - 피시방 알바

<a href='https://www.acmicpc.net/problem/1453'>백준 1453 - 피시방 알바</a>

## ⚡️ 나의 풀이
`defaultdict(int)`를 선언하고 `arr`의 인덱스들을 하나씩 더해줬다. 그리고 마지막에 `lambda x: x-1`을 사용해서 전체 1씩 빼주고 `sum`을 사용했다.
그런데, 다른 사람의 풀이를 보니까 이렇게 어렵게 구현하지 않아도 풀 수 있는 문제였다. 전체 범위를 `False`처리 해두고 해당 `index`가 들어오면 `True`처리, 이후에도 또 들어오면 `cnt+=1`을 해줬다.

```python
# 나의 풀이
import sys
from collections import defaultdict
input = sys.stdin.readline

n = int(input())
arr = list(map(int, input().split()))
computer = defaultdict(int)

for i in range(len(arr)):
    computer[arr[i]] += 1

print(sum(map(lambda x: x-1, computer.values())))

# 다른 사람의 풀이
n = int(input())
arr = list(map(int, input().split()))
check = [False] * 101

cnt = 0
for i in arr:
    if check[i]:
        cnt +=1
    else:
        check[i] = True
print(cnt)
```

---
## 📍 백준 1924 - 2007

<a href='https://www.acmicpc.net/problem/1924'>백준 1924 - 2007</a>

## ⚡️ 나의 풀이
날짜 맞추는 문제다. <a href='https://ywtechit.tistory.com/9'>저번에</a> 풀었는데 오랜만에 풀려니까 까먹었다.
중간에 날짜를 7로 나눈 나머지를 구하는 것과 `array`에 전체 매 달을 넣고 구하는것까지는 기억이 났는데, 그 이후에는 기억이 나지 않았다.

1. 구해야하는 달 이전 달(x-1)까지값을 더하고(sum) 구해야하는 일(y)을 더한다.
2. 전체 값을 7로 나눠주고 나머지값을 `days`에 붙여준다.
3. 문제에 1월 1일이 월요일이라고 나와있어 `days[1]`부터 `MON`을 작성했다.

```python
x, y = map(int, input().split())

months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
days = ['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT']

print(days[(sum(months[:x-1])+y) % 7])
```


---
## 📍 백준 14467 - 소가 길을 건너간 이유1

<a href='https://www.acmicpc.net/problem/14467'>백준 14467 - 소가 길을 건너간 이유1</a>

## ⚡️ 나의 풀이
이번에도 `defaultdict`를 이용해서 풀었다. 

1. 1번부터 10번까지 빈 리스트를 선언한다.
2. 소의 위치를 빈 리스트에 추가한다.
3. `cnt`는 2번 이상 움직인 소부터 증가하기때문에 해당 값만 따로 빼냈다.
4. `1에서 0`으로 이동한 소 혹은 `0에서 1`로 이동한 소만 `cnt`를 증가하게 설정했다. 예제입력을 보면 소가 `1 -> 0 -> 1` 이렇게 이동하지 않고 `1 -> 0 -> 0 -> 1` 혹은 `0 -> 1 -> 1 -> 0`으로 이동했기때문에 바로 다음칸의 원소를 확인하는 코드로 작성해도 오답판정이 안 나는것 같다.

```python
from collections import defaultdict

n = int(input())
cows = defaultdict(list)

for i in range(1, 11):    # 1번부터 10번까지 빈 리스트 선언
    cows[i] = []

for i in range(n):
    cows_num, cows_move = map(int, input().split())
    cows[cows_num].append(cows_move)    # 소의 위치 추가

cow_moves = [i for i in cows.values() if len(i) >= 2]    # 2번이상 움직인 소 꺼내기    

cnt = 0
for i in range(len(cow_moves)):
    result = cow_moves[i]
    for j in range(len(result) - 1):
        if (not result[j] and result[j + 1]) or (result[j] and not result[j + 1]):    # 1 -> 0, 0 -> 1로 이동한 소만 cnt 증가
            cnt += 1
print(cnt)
```

---
## 📍 백준 10250 - ACM 호텔

<a href='https://www.acmicpc.net/problem/10250'>백준 10250 - ACM 호텔</a>

## ⚡️ 나의 풀이
사칙연산 + 구현문제다. 쉬운문제인줄 알고 도전했으나 생각보다 쉽지 않았다. 또, 정답비율이 높지 않았는데 이유를 알 것 같았다. 문제에서 `가로 x 세로`형태로 나오길래 2차원배열로 초기화하는 문제인가? 했는데 아니었다. 이 문제의 핵심은 `N`을 `H`로 나눴을 때 나누어 떨어지는지 아닌지의 경우를 잘 생각하면 풀 수 있는 문제다.

1. 크게 두 가지로 나눠서 풀면된다. 층 수를 구하는 식, 방 번호를 구하는 식
2. 층 수: N번째 방의 층을 구할 때는 `N`을 `H(층)`으로 나눈 나머지를 구하면 된다. 이때 `N`이 `H`로 나눈 나머지가 0이 아니라면 나머지를 `H`층으로 선언해주고 0이라면 `H`층이므로 `H`로 선언해준다. 예를들어 `H, W, N = 4, 3, 4`인 경우를 살펴보자. 이때는 `H % N == 0`이므로 제일 꼭대기에 위치해있을것이다. 따라서 손님에게 배정될 층 수는 `H`층이 된다.

![](https://images.velog.io/images/abcd8637/post/2111bc4a-c1b3-48f7-be06-f27a2faf294b/KakaoTalk_Photo_2021-05-01-09-49-08.jpeg)

3. 호 수: 마찬가지로 `H(층)`를 이용해야하는데, 2번 과정에서 `나머지`를 이용했다면, 이번에는 `몫`을 이용하면 된다. 단, 2번과정을 선행한 이후에 경우의 수를 나누자. 예를들어 `H, W, N = 4, 3, 4`의 경우 2번과정에서 나머지가 없었기 때문에 몫을 그대로 넣어주면 되고, `H, W, N = 4, 3, 6`의 경우 2번과정에서 나머지가 있었기 때문에 그대로 몫에 +1 처리를 해주면 된다. 

```python
T = int(input())

for _ in range(T):
    H, W, N = map(int, input().split())

    if not N % H:
        floor = H
        number = N // H
    else:
        floor = N % H
        number = N // H + 1

    print(floor*100 + number)
```

## 📍 백준 2693 - N번째 큰 수

<a href='https://www.acmicpc.net/problem/2693'>백준 2693 - N번째 큰 수</a>

## ⚡️ 나의 풀이
N번째 큰 값을 출력하는 문제인데, 출력지문을 다시보면 배열 A에서 3번째 큰 값을 출력한다고 정해져있다.

1. 테스트케이스만큼 반복한다.
2. 배열을 입력받는다.
3. 정렬한다.
4. 앞에서 혹은 뒤에서 3번째 수를 출력한다.

```python
import sys
input = sys.stdin.readline
T = int(input())

for i in range(T):
    arr = list(map(int, input().split()))
    arr.sort()
    print(arr[-3])
```

---
## 📍 백준 2167 - 2차원 행렬의 합

<a href='https://www.acmicpc.net/problem/2693'>백준 2693 - N번째 큰 수</a>

## ⚡️ 나의 풀이
```python
n, m = map(int, input().split())
arr = [list(map(int, input().split())) for _ in range(n)]
memo = [[0] * (m+1) for _ in range(n+1)]

for i in range(1, n+1):
    for j in range(1, m+1):
        memo[i][j] = arr[i-1][j-1] + memo[i][j-1] + memo[i-1][j] - memo[i-1][j-1]

k = int(input())

for _ in range(k):
    i, j, x, y = map(int, input().split())
    print(memo[x][y] - memo[x][j-1] - memo[i-1][y] + memo[i-1][j-1])
```

---
## 📍 백준 2948 - 2009년

<a href='https://www.acmicpc.net/problem/2948'>백준 2948 - 2009년</a>

## ⚡️ 나의 풀이
저번에 풀었던 <a href='https://ywtechit.tistory.com/84'> 2007년</a>과 동일한 유형이다. 다만, 문제에 윤년이라고 주어져있지 않기때문에 2월은 28일로 생각하고 풀면 된다.

```python
months = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
days = ["Wednesday", "Thursday", "Friday", "Saturday", "Sunday", "Monday", "Tuesday"]
D, M = map(int, input().split())
print(days[(sum(months[:M-1]) + D) % 7])
```

---
## 📍 백준 5598 - 카이사르 암호

<a href='https://www.acmicpc.net/problem/5598'>백준 5598 - 카이사르 암호</a>

## ⚡️ 나의 풀이
내가 풀었던 하드코딩 방식보다는 다른 사람이 푼 방식이 조금 더 괜찮아보였다.

1. `key`에 1부터 26까지 `value`에 알파벳을 `dict`에 선언한다.
2. 알파벳 문자를 3개씩 건너뛰는데 다른 문자는 상관없지만 `A`, `B`, `C`는 `index_error`가 발생한다.
3. 따라서, 입력중에 `A`, `B`, `C`가 포함되어있으면 `X`, `Y`, `Z`로 출력한다.

```python
# 내가 작성한 코드
s = input()
x = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

alphabet = {}
for i in range(1, 27):
    alphabet[i] = x[i-1]

temp = ''
for i in s:
    if i == 'A' or i == 'B' or i == 'C':
        temp += alphabet[ord(i)-41]
    else:
        temp += alphabet[ord(i)-67]
        
print(temp)
```

## ⚡️ 다른사람의 풀이
문자열 슬라이싱을 이용한 코드

1. `index` 함수를 사용하여 `s`에서 입력문자가 몇번째에 위치해있는지 가르킨다.
2. 해당값에 `-3`을 해준다. (알파벳 문자를 3개씩 건너뛴다는 규칙)
3. 입력 중에 `A`, `B`, `C`가 나오면 음수가 되는데 슬라이싱에서 음수는 문자열 제일 뒤의 값을 출력하기 때문에 자연스럽게 `X`, `Y`, `Z`와 매칭된다.

```python
# .index를 사용한 코드
s = input()
x = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
temp = ''

for i in s:
    temp += x[x.index(i)-3]

print(temp)
```

정석적인 풀이방법

1. 알파벳을 `ASCII`코드로 변경하는 `ord()`에 `-68`을 빼준다.(65를 빼주면 1부터 매칭되지만 카이사르 암호는 `D`부터 시작하기 때문에 3을 더 빼줘서 1이 `D`부터 시작된다.)
2. `A`, `B`, `C`는 음수 처리되기 때문에 알파벳 대문자의 총 개수 26으로 나눠준다.
3. `A`, `B`, `C`는 `X`, `Y`, `Z`와 매칭되어야하므로 65를 더해준다.(`A: 88, B: 89, C: 90, D: 65...`)

```python
s = input()
x = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
temp = ''
for i in s:
    temp += chr(((ord(i) - 68) % 26) + 65)

print(temp)
```

---
## 📍 백준 3460 - 이진수

<a href='https://www.acmicpc.net/problem/3460'>백준 3460 - 이진수</a>

## ⚡️ 나의 풀이

1의 위치를 찾으면 되는 문제이고 입력을 `bin` 함수로 변환했는데 중요한 점은, `bin`함수를 사용하게 되면 `ob1010`처럼 문자열로 출력한다. 따라서, 조건문을 사용할 때 `1` 대신 `'1'`을 사용하도록 하자. 그리고 다른 사람의 코드를 보다가 리스트를 거꾸로 사용해야하는 경우 `range(n-1, -1, -1)` 대신 출력부분에 `[-i-1]`를 사용했다. 일부로 뒤집을 필요없이 단순하게 출력만 바꾸면 되니까 잊지말고 <a href='https://ywtechit.tistory.com/108'>기록</a>해두고 써먹어야겠다.

1. `bin` 함수를 이용하여 10진수 형태의 입력을 2진수 형태로 변경한다. `bin`함수로 변환하게되면 `ob1010`과 같은 값이 나오는데 숫자만 사용하기위해 슬라이싱으로 [2:] 잘라준다.
2. 최하위 비트(least significant bit, lsb)의 위치가 0이므로, 리스트를 거꾸로 뒤집는다.
3. `enumerate` 함수를 이용하여 `value`가 `'1'`인 경우 해당 `index`를 출력해준다.

```python
# 나의 풀이
T = int(input())
for _ in range(T):
    n = bin(int(input()))[2:]
    for idx, val in enumerate(n[::-1]):
        if val == '1':
            print(idx, end=' ')
```

```python
# 다른사람의 풀이
T = int(input())

for _ in range(T):
    n = bin(int(input()))[2:]
    for i in range(len(n)):
        if n[-i - 1] == '1':
            print(i, end=' ')
```

---
## 📍 백준 10214 - Baseball

<a href='https://www.acmicpc.net/problem/10214'>백준 10214 - Baseball</a>

## ⚡️ 나의 풀이
이 문제를 처음에 보고 이해가 명확히 안됐었다. 그러니까.. 테스트 케이스마다 값을 비교해서 출력 하라는건가? 아니면 출력이 잘 못나왔나? 생각했는데 결론적으로 `각 테스트 케이스마다 9번의 값을 각각 비교하여 더 많이 누적된 cnt값을 출력`하는 문제였다... 내가 독해 능력이 낮은건가.. 라고 생각했다.

1. 각각의 테스트 케이스마다 누적할 값 `cnt`를 선언한다.
2. 이중 반복문으로 T번의 테스트 케이스 안에 9번의 입력을 받을 때 변수를 선언한다. 
3. 안에있는 반복문을 도는동안 값을 비교하여 `Ycnt, Kcnt`에 누적시킨다.
4. 한번의 테스트 케이스가 끝날때마다 누가 더 큰지 비교하여 값을 출력한다.

```python
T = int(input())
Ycnt, Kcnt = 0, 0

for _ in range(T):
    for i in range(9):
        Y, K = map(int, input().split())
        if Y > K:
            Ycnt += 1
        elif Y < K:
            Kcnt += 1

    if Ycnt > Kcnt:
        print('Yonsei')
    elif Ycnt < Kcnt:
        print('Korea')
    else:
        print('Draw')
```

---
## 📍 백준 2845 - 파티가 끝나고 난 뒤

<a href='https://www.acmicpc.net/problem/2845'>백준 2845 - 파티가 끝나고 난 뒤</a>

## ⚡️ 나의 풀이
입력에 `사람의 수 * 파티가 열렸던 곳의 넓이`를 해주면 전체 넓이를 알 수 있고 해당 값을 예제 입력을 하나씩 빼주면 답이 나온다. 리스트안에서 각각의 원소들을 빼주는 방법은 `lambda`함수를 사용하여 간단하게 해결해주고 `join` 함수를 이용해 괄호를 풀어줬다.

```python
people, area = map(int, input().split())
news_paper = list(map(int, input().split()))

gap_news_paper = list(map(lambda x: x - (people*area), news_paper))
print(' '.join(map(str, gap_news_paper)))
```

---
## 📍 백준 10801 - 카드게임

<a href='https://www.acmicpc.net/problem/10801'>백준 10801 - 카드게임</a>

## ⚡️ 나의 풀이
어제 풀었던 <a href='https://ywtechit.tistory.com/113'>백준 10214 - Baseball</a>문제와 입력형태를 제외하고 거의 흡사한 문제였다. 입력받은 `A`, `B` 각각의 위치를 대소비교하면 되는데 이럴때 가장 편하게 사용 할 수 있는 `zip`함수를 이용하자. 다만, `zip`함수는 서로 리스트의 길이가 다르면 사용 할 수 없다. 이 문제는 리스트의 길이가 서로 같으므로 `zip`함수를 사용 할 수 있다. 대소비교 이후 값을 누적하고 마지막에 조건에따라 출력해주면 된다.

```python
A = list(map(int, input().split()))
B = list(map(int, input().split()))
A_cnt, B_cnt = 0, 0

for A_card, B_card in zip(A, B):
    if A_card > B_card:
        A_cnt += 1
    elif A_card < B_card:
        B_cnt += 1

if A_cnt > B_cnt:
    print('A')
elif A_cnt < B_cnt:
    print('B')
else:
    print('D')
```

---
## 📍 백준 1110 - 더하기 사이클

<a href='https://www.acmicpc.net/problem/1110'>백준 1110 - 더하기 사이클</a>

## ⚡️ 나의 풀이
문제의 조건대로 구현하면 되는 문제인데, `n`번 사이클을 돌고나서 원래의 수와 같아지는 조건식을 잘못넣어서 조금 헤맸다. 결론적으로 처음 입력을 새로운 변수 `check`로 선언하고 제일 마지막에 나온 값과 비교해주면 됐다.
또, 처음 조건에 주어진 수가 10보다 작으면 앞에 0을 붙인다고 나와있는데, 사실 이 조건은 없어도 되는 조건이다. 예를 들어 처음 주어진 수가 `5`라고 할 때, 앞에 `0`을 붙여주고 각 자리의 숫자를 더하면 `0+5`가 되는데, `0`은 있으나 없으나 같은 값이 되기 때문이다. 따라서 해당 조건은 건너뛰고 생각하면 된다.

여담이지만 각 자리의 숫자를 더하는 방법은 다음과 같다.
1. `재귀함수`를 이용해서 `10으로 나눈 몫`과 `10으로 나눈 나머지`를 `일의 자리수`가 될 때까지 더하기
2. `map`함수를 이용해서 `str`로 바꾸고 `sum`함수로 한번에 더하기
3. `반복문`을 이용해서 `str`로 바꾸고 하나씩 더하기

```python
n = 123

# 1. 재귀함수
def sum_digit(n):
    if n < 10:
        return n
    return n % 10 + sum_digit(n // 10)

print(sum_digit(n))
👉🏽 6    

# 2. map 함수
result = sum(map(int, str(n)))

print(result)
👉🏽 6

# 3. 반복문
temp = 0
for i in str(n):
    temp += int(i)

print(temp)
👉🏽 6
```

새로운 수 `new_n`을 구할 때 `10으로 나누는 방법`과 `문자열인덱싱`으로 제일 마지막의 값만 떼오는 방법을 사용했는데, 메모리는 `28776KB`로 동일했고 실행시간이 `64m/s`, `72m/s`로 `10으로 나누는 방법`이 `8m/s`로 근소하게 빨랐다. 코드는 다음과 같다.

```python
n = int(input())
check = n
flag = True
cnt = 0

# 10으로 나누는 방법
while flag:
    temp = int(n) // 10 + int(n) % 10
    new_n = str(n % 10) + str(temp % 10)
    cnt += 1
    if int(new_n) == check:
        flag = False
    n = int(new_n)
print(cnt)

# 문자열 인덱싱 이용한 방법
while flag:
    temp = int(n) // 10 + int(n) % 10
    new_n = str(n)[-1] + str(temp)[-1]
    cnt += 1
    if int(new_n) == check:
        flag = False
    n = new_n
print(cnt)
```

---
## 📍 백준 4673 - 셀프 넘버

<a href='https://www.acmicpc.net/problem/4673'>백준 4673 - 셀프 넘버</a>

## ⚡️ 나의 풀이
문제는 대충 이해됐지만, 막상 코드로 표현하려니까 막막했다. 시작범위를 어디서부터 잡아야하는지도 잘 몰랐는데, 많은 고민끝에 다음과 같은 방법을 생각했다.

1. 생성자가 없는 숫자를 셀프 넘버라고 칭하니까 생성자가 있는 숫자들을 구하고 새로운 리스트에 담아주자.
2. 전체 `1~10000`까지의 범위를 하나 초기화한다음에, 거기서 생성자가 있는 숫자들을 모두 빼면 나머지는 셀프넘버가 된다.
3. 문제에 `10000`보다 작거나 같은 셀프넘버라고 나와있으니까. 종료범위는 `10000`까지이고, 시작 범위는 문제에 양의 정수 `n`에 대해 계산한다고 나와있으므로 `1`부터 시작한다.

또, 이와같이 생각했음에도 답이 도출되지 않았는데 원인은 `target.append(temp)`에 있었다. 처음에 `temp+=int(i)` 바로 밑에다가 해당 코드를 적었는데, 왜 답이 안나오지?! 하다가 `디버깅`을 하면서 코드를 다시보니까 해당 코드를 이중 반복문 안쪽에다 선언했는데, 이는 한 자리수를 더 할때마다 `target`에 값을 넣는 것이었다. 결론적으로 `n`의 각 자리수를 모두 더하고 새로운 리스트에 넣었어야 했는데, `n`의 각 자리수를 더할 때마다 `target`에 값을 추가했었다. 이중 반복문을 사용하니까 이런 실수도 하는구나를 느꼈다. 다음에는 이런실수를 하지 말아야지.

```python
numbers = list(range(1, 10001))

target = []
for i in range(1, 10001):
    temp = i
    for j in str(temp):
        temp += int(j)
    target.append(temp)

print('\n'.join(map(str, sorted(set(numbers) - set(target)))))
```

---
## 📍 백준 4396 - 지뢰

<a href='https://www.acmicpc.net/problem/4396'>백준 4396 - 지뢰</a>

## ⚡️ 나의 풀이
상당히 고생한 문제다. 이 문제를 맞추기위해 정답을 얼마나 제출 했는지 모르겠다. 난이도가 실버5 였기때문에 쉽게 풀 줄 알았는데 큰 코 다쳤다.

![](https://images.velog.io/images/abcd8637/post/23b69dbc-b6bf-488f-989d-ada48bb71a32/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-20%2011.26.46.png)

처음 짰던 코드는 접근 자체를 잘 못했다. 이때까지 `n*n` 행렬을 초기화 시킬때 무조건 `0`으로 했는데, 꼭 그렇게 할 필요 없다는 생각이 이 문제를 풀면서 떠올랐다. 이 문제에 `다른 모든 지점이 온점(.)`으로 표시되어야하는 조건에서 `result`의 초기값을 `.`으로 해주면 됐었다.

또, 문제를 완벽하게 이해하지 못했는데, 지뢰가 있는 칸이 열렸다면 지뢰가 있으면서 열린칸만 별표`(*)`로 표시하는것이 아니고, 지뢰가 있는 모든 칸이 별표`(*)`로 처리되어야한다. 도저히 모르겠어서 <a href='https://www.acmicpc.net/board/view/68404'>질문</a>까지 남겼는데 다른분이 친절하게 알려주셔서 해결했다. 결국, 2중 반복문을 하나 더 선언해줬다.(전체는 총 4중 반복문이 된다.) 

이해가 안되면 다음 사진을 보자. 두 개의 T.C(테스트 케이스)인데, 구분 할 수 있겠는가?
![](https://images.velog.io/images/abcd8637/post/f8bd8942-249e-4f17-a740-9c14c207ce30/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-20%2011.47.42.png)

`23번째코드`도 `if`와 `elif` 중 어떤 코드를 사용해야할지 헷갈렸는데, 결론적으로 둘다 사용해도 상관없다. 잘 이해가 안된다면 저번에 올렸던 글을 참고하자.
 
1. 초기 값을 `.`(온점)으로 선언한다.
2. 지뢰가 없으면서 열린 칸은 0과 8사이에 숫자를 넣어준다.
3. 지뢰가 있는 칸이 열렸다면 지뢰가 있는 모든 칸이 별표(*)로 표시되어야 한다.
4. 다른 모든 지점은 온점(.)이어야 한다.(1번에서 적용 완료)

문제에서 T.C가 한개밖에 없어 몇가지를 만들었다. 제일 하단을 참고하자.

```python
n = int(input())
mine = [list(input()) for _ in range(n)]
board = [list(input()) for _ in range(n)]
result = [['.'] * n for _ in range(n)]
dx = [-1, -1, -1, 0, 0, 1, 1, 1]
dy = [-1, 0, 1, -1, 1, -1, 0, 1]

for x in range(n):
    for y in range(n):
        if mine[x][y] == '.' and board[x][y] == 'x':    # 지뢰가 없으면서 열린 칸
            cnt = 0
            for i in range(8):
                nx = x + dx[i]
                ny = y + dy[i]

                if nx < 0 or ny < 0 or nx >= n or ny >= n:
                    continue

                if mine[nx][ny] == '*':
                    cnt += 1
            result[x][y] = cnt    # 19번의 조건 절을 통과하지 않아도 cnt 적용

        if mine[x][y] == '*' and board[x][y] == 'x':    # 지뢰가 있는 칸이 열렸다면
            for a in range(n):
                for b in range(n):
                    if mine[a][b] == '*':    # 첫번째 입력 중 지뢰가 있는 칸이면
                        result[a][b] = '*'    # 지뢰가 있는 모든 칸을 별표로 표시
for i in range(n):
    for j in range(n):
        print(result[i][j], end='')
    print()
```

```python
'''
입력

8
...**..*
......*.
....*...
........
........
.....*..
...**.*.
.....*..
xxxx....
....xxxx
xxxx....
....xxxx
xxxx....
....xxxx
xxxx....
....xxxx

2
*.
.*
.x
x.

2
*.
.*
..
.x
'''

'''
출력
001**..*
....33*2
0001*...
....1100
0000....
....3*21
001**.*.
....3*21

.2
2.

*.
.*
'''
```

---
## 📍 백준 20291 - 파일 정리

<a href='https://www.acmicpc.net/problem/20291'>백준 20291 - 파일 정리</a>

## ⚡️ 나의 풀이

1. 확장자 뒤의 값만 담을 `defaultdict` 변수를 선언한다.
2. 공백을 기준으로 분리(`split()`)한다.
3. 동일한 확장자(`split()[1]`)가 입력으로 들어오면 `defaultdict`에 `1`씩 더한다.
4. `dic.items()`를 `sorted`한다.
5. `' '.join`을 사용하여 출력한다.

```python
from collections import defaultdict
import sys
input = sys.stdin.readline

n = int(input())
dic = defaultdict(int)

for _ in range(n):
    file = input().rstrip().split('.')[1]
    dic[file] += 1

for i in sorted(dic.items()):
    print(' '.join(map(str, i)))
```

---
## 📍 백준 10703 - 유성

<a href='https://www.acmicpc.net/problem/10703'>백준 10703 - 유성</a>

## ⚡️ 나의 풀이
이 문제는 내가 구현력이 부족하여 3일동안 잡고 있었다. 정답판정을 받고 복습겸 글을 작성하면서 느끼는건 정답 코드를 볼땐 금방 풀 수 있을것 같은데 막상 풀때는 왜 그렇지 못할까?! 라는 생각이 든다.

중간에 `move`를 계산하는 과정에 막혀 <a href='https://www.acmicpc.net/board/view/68931'>질문</a>을 올렸는데 고수분께서 답변을 해주셔서 너무 감사했다. 문제를 다 풀고 그분의 코드를 보니까 이렇게도 생각 할 수 있구나..! 대박인데?!라고 생각했다. 나도 언젠가 고수가 되어 모르는 분들이 올리는 질문을 자유자재로 답변해주는 수준까지 올라가리라..

이번 문제를 풀며 배운점은 여러가지 있지만 중요하다고 생각하는 내용들을 가져왔다.
1. 문자열 리스트를 입력받을 때 `[list(input())]` 대신 `[input()]`을 사용하자!! 단순히 `list`만 붙였는데도 실행시간이 2배가까이 차이가 났다.
2. 범위가 큰 2차원 문자열 리스트를 출력할 때 `print()` 대신 `sys.stdout.write()`를 사용하자!! `print()`와 `sys.stdout.write()`는 `input()`과 `sys.stdin.readline`만큼 차이는 없지만 문자열을 하나하나 출력하는 경우에 `print()`는 엄청 느릴 수 밖에 없다. 
3. 최대값을 갱신하려는 초기값은 `0`보다는 `음수`를 사용하자. 꼭 필요한건 아니지만 가독성면에서 차이가 난다.
4. 2차원 배열을 하나하나씩 검사 할 때 꼭 좌측 상단에서부터 하라는 법은 없다. 배열 내의 움직임이 많은 문제라면 `좌측 하단`, 혹은 `우측 하단`의 경우도 고려해보자.

![](https://images.velog.io/images/abcd8637/post/bb1e2e6a-4fe0-4d5c-a83e-cd6a3f622d19/KakaoTalk_Photo_2021-05-27-11-59-36.jpeg)

이 문제의 핵심은 유성 좌표 중 가장 높은 행 좌표(좌표가 커야 땅과의 거리가 가깝다.)와 땅 좌표 중 가장 낮은 행 좌표(좌표가 작아야 유성과의 거리가 가깝다.)를 서로 빼야 땅과 부딪히지 않고 유성이 추락 할 수 있다. 그러면 반복문 마다 매 가장 낮은 좌표로 설정하면 되는것 아닌가?라고 할 수 있지만 유성이 없는경우에도 좌표는 최소가 설정 될 수 있기 때문에 `유성이 있으면서 좌표가 가장 낮은 값`을 고려해줘야한다. 그래서 `arr`을 가로가 아닌 세로로 확인하기 위해 `flag`를 설정해 유성이 있는 좌표에서 `True`로 바꿔 `move`를 계산했는데 쉽지 않았던 방식이었다.

이보다 쉬운 방식인 `다른사람의 코드`처럼 `S`의 길이만큼 리스트를 초기화 해주고 현재 유성의 좌표 일 때 현재 `row`값과 초기값을 비교하여 최대 `row`를 갱신시키는 방법, 마찬가지로 현재 땅의 좌표가 일 때 최소 `row`을 갱신시키는 방법을 사용해 쉽게 풀었다. 어떻게 이런 생각을 했지?! 대단하다..

이후에는 최종 `move`만큼 배열을 이동시켜주자. 

잘 모르겠다면 하단의 <a href='https://www.acmicpc.net/board/view/2237'>테스트케이스</a>를 해보고 왜 안되는지 생각해보자. 그럼 금방 알 수 있다.

```
6 8
...X....
........
.......#
.......#
.......#
...#####
 
result:
........
........
.......#
.......#
...X...#
...#####
```

`메모리초과`와 `시간초과`의 연속이었던 문제..

![](https://images.velog.io/images/abcd8637/post/f0551b33-776b-4806-8deb-818fc20e165c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-27%2011.15.19.png)

```python
# 나의 코드
import sys
input = sys.stdin.readline

R, S = map(int, input().split())
meteor = [input() for _ in range(R)]    # 유성 충돌 전
arr = [['.'] * S for _ in range(R)]    # 유성 충돌 후

move = 1 << 14    # 유성이 최종적으로 움직여야하는 거리

for x in range(S):
    temp_meteor = 0    # 가장 높은 유성 행 좌표 (좌표가 높아야 땅과의 거리가 가깝다.)
    temp_ground = 9999    # 가장 낮은 땅 행 좌표 (좌표가 낮아야 유성과의 거리가 가깝다.)
    flag = False    
    for y in range(R):
        if meteor[y][x] == 'X':
            temp_meteor = max(temp_meteor, y)
            flag = True    # 유성이 있는 좌표를 만나면 True
        elif meteor[y][x] == '#':
            temp_ground = min(temp_ground, y)
    if flag:    # 유성이 있는 좌표에서 `move` 계산
        move = min(abs(temp_meteor-temp_ground)-1, move)

for x in range(R):
    for y in range(S):
        if meteor[x][y] == 'X':
            arr[x+move][y] = 'X'    # 유성을 최종 move만큼 움직인다.
        if meteor[x][y] == '#':
            arr[x][y] = '#'

for i in range(R):    # 결과 출력
    for j in range(S):
        sys.stdout.write(arr[i][j])
    sys.stdout.write('\n')
```

```python
# 다른사람의 코드
import sys
input = sys.stdin.readline

R, S = map(int, input().split())
meteor = [input() for _ in range(R)]    
arr = [['.'] * S for _ in range(R)]    

max_meteor = [-3333] * S    # 유성 좌표를 저장 할 리스트
min_ground = [1 << 14] * S    # 땅 좌표를 저장 할 리스트

for x in range(R):
    for y in range(S):
        if meteor[x][y] == 'X':
            max_meteor[y] = max(max_meteor[y], x)    # 현재 유성의 y좌표(열)를 갱신함
        elif meteor[x][y] == '#':
            min_ground[y] = min(min_ground[y], x)    # 현재 땅의 y좌표(열)를 갱신함

move = min((j-i for i, j in zip(max_meteor, min_ground))) - 1    # 최종적으로 가야 할 move 계산

for x in range(R):
    for y in range(S):
        if meteor[x][y] == 'X':
            arr[x+move][y] = 'X'    # 유성을 최종 move만큼 움직인다.
        if meteor[x][y] == '#':
            arr[x][y] = '#'

for i in range(R):    # 결과 출력
    for j in range(S):
        sys.stdout.write(arr[i][j])
    sys.stdout.write('\n')
```