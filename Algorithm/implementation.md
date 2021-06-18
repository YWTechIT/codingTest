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

---
## 📍 백준 2578 - 빙고

<a href='https://www.acmicpc.net/problem/2578'>백준 2578 - 빙고</a>

## ⚡️ 나의 풀이
구현력을 묻는 문제였는데, `21.5.17.`부터 풀기 시작하다 중간에 막혀 <a href='https://ywtechit.tistory.com/134'>boj_10703 유성</a>문제를 풀고 다시 풀어봤는데 감이 잡혀서 정답판정을 받은 문제다.

이 문제의 핵심 부분은 다음과 같다.
1. 사회자가 부르는 수를 차례로 지워가면서 `check` 한다.(수가 불리면 `0`으로 초기화시킨다.)
2. `check` 할 때 가로, 세로, 대각선 각각 `check`한다. 이때, 한 줄 혹은 한 열 혹은 한 대각선에서 0이 5개가 나오면 `bingo+=1`을 한다.
3. `bingo >= 3`이면 해당 숫자가 몇 번째 `cnt`된 숫자인지 출력한다.

다음으로 가로, 세로, 대각선에서 `bingo`를 판단하는 방법을 살펴보자.
1. 가로(row): `count.('[0, 0, 0, 0, 0]')`이 되면 `+1`을 해주었다. 주의 할 점은 판별하려는 값을 `str`형으로 변환한다음 `count`를 사용하자.
2. 세로(column): `arr`을 세로로 돌려야하는데 `lambda` 함수를 사용해서 열로 만들어주고 `count` 함수를 사용했다.
3. 대각선(diagonal): 대각선 전체의 값이 0이 되는지를 확인했다. 정 대각선 방향, 역 대각선 방향 두 가지의 경우를 판단해야한다.

처음에는 `정 대각선`, `역 대각선` 판단 변수를 각각 따로 설정했는데, 그럴 필요가 없이 두 경우를 합쳐서 `index`를 2개줘도 됐었다. 

또, 문제를 풀다보면 느끼겠지만 이미 `bingo`가 되었던 값을 또 누적시키는 상황이 생긴다. (이 문제를 푸는데 오래 걸린 이유도 여기서 막혔기 때문이다.) 결론은 간단하지만 결론까지오기에 많은 시간이 걸렸다. 결론적으로 `check_row`, `check_column`, `check_diagonal` 변수를 사용해서 `bingo`가 되는 행, 열, 대각선 `index`는 `True`로 바꿔놓고 다음 `bingo`를 판단하는 조건은 `bingo`이면서 행, 열, 대각선 `index`가 `False`인 값만 통과하게 설정했더니 이전 `bingo`가 누적이 되는 일은 없었다. `bingo`가 3개 이상되면 `break` 대신 `exit`를 선언해서 전체 반복문을 끝내버렸다.

정답판정을 받고 다른사람의 코드를 보다가 처음 4중 반복문을 3중 반복문으로 끊어놓은 사람도 있었다. 그 점을 참고해서 살짝 수정했는데, `MC`의 리스트를 2차원이 아닌 1차원으로 선언하고 처음 반복문의 범위를 `25`까지 설정해놓은 다음에 순서대로 `index`를 가져오는 방법이었다. 사회자는 차례대로 숫자를 부르기때문에 굳이 2차원배열을 선언 할 필요가 없었다. (어떻게 이런 생각을.. ㄷㄷ 🥶 🥶)

```python
# 나의 코드
n = 5
arr = [list(map(int, input().split())) for _ in range(n)]
MC = [list(map(int, input().split())) for _ in range(n)]

bingo, order = 0, 0
check_row, check_column, check_diagonal = [False] * n, [False] * n, [False] * 2

def check(arr):
    global bingo, check_diagonal
    temp_right, temp_reverse = 0, 0

    for i in range(n):
        if str(arr[i]).count('[0, 0, 0, 0, 0]') and not check_row[i]:  # check row
            bingo += 1
            check_row[i] = True

        temp_column = list(map(lambda x: x[i], arr))  # check column
        if str(temp_column).count('[0, 0, 0, 0, 0]') and not check_column[i]:
            bingo += 1
            check_column[i] = True

        temp_right += arr[i][i]    # check diagonal
        temp_reverse += arr[i][n - i - 1]

    if not temp_right and not check_diagonal[0]:
        check_diagonal[0] = True
        bingo += 1

    if not temp_reverse and not check_diagonal[1]:
        check_diagonal[1] = True
        bingo += 1

    return bingo

for numbers in MC:
    for target in numbers:
        for i in range(n):
            for j in range(n):
                if target == arr[i][j]:
                    arr[i][j] = 0
                    check(arr)
                    order += 1
                    if bingo >= 3:
                        print(order)
                        exit()

```

```python
# 내 코드 + 다른사람의 코드
n = 5
arr = [list(map(int, input().split())) for _ in range(n)]

MC = []
for _ in range(5):
    MC += list(map(int, input().split()))

bingo, order = 0, 0
check_row, check_column, check_diagonal = [False] * n, [False] * n, [False] * 2

def check(arr):
    global bingo, check_diagonal
    temp_right, temp_reverse = 0, 0

    for i in range(n):
        if str(arr[i]).count('[0, 0, 0, 0, 0]') and not check_row[i]:  # check row
            bingo += 1
            check_row[i] = True

        temp_column = list(map(lambda x: x[i], arr))  # check column
        if str(temp_column).count('[0, 0, 0, 0, 0]') and not check_column[i]:
            bingo += 1
            check_column[i] = True

        temp_right += arr[i][i]    # check diagonal
        temp_reverse += arr[i][n - i - 1]

    if not temp_right and not check_diagonal[0]:
        check_diagonal[0] = True
        bingo += 1

    if not temp_reverse and not check_diagonal[1]:
        check_diagonal[1] = True
        bingo += 1

    return bingo

for target in range(25):
    for i in range(5):
        for j in range(5):
            if MC[target] == arr[i][j]:
                arr[i][j] = 0
                check(arr)
                order += 1
                if bingo >= 3:
                    print(order)
                    exit()
```

---
## 📍 백준 1110 - 하얀 칸

<a href='https://www.acmicpc.net/problem/1110'>백준 1110 - 하얀 칸</a>

## ⚡️ 나의 풀이
문제 중 `번갈아가며 색칠 되어있다.`라는 힌트에서 규칙을 찾을 수 있다.  저번에 풀었던 <a href='https://ywtechit.tistory.com/129'>boj_1018 체스판 다시 칠하기</a>에서 규칙을 볼 수 있다. 또, 이 문제를 풀고 `boj_1018 체스판 다시 칠하기`문제를 풀어보는것을 추천한다. 

1. 입력을 받는다.
2. 8 * 8 배열에서 가장 왼쪽 위칸이 흰색이므로 짝수인 자리와 동시에 말(`F`)인 값을 찾는다.
3. `cnt`를 누적시킨다.

```python
chess = [input() for _ in range(8)]

cnt = 0
for i in range(8):
    for j in range(8):
        if not (i+j) % 2 and chess[i][j] == 'F':
            cnt += 1
print(cnt)
```

---
## 📍 백준 3009 - 네 번째 점

<a href='https://www.acmicpc.net/problem/3009'>백준 3009 - 네 번째 점</a>

## ⚡️ 나의 풀이 
수학적으로 어떻게 풀어야할지 많은 고민을 했는데 결론적으로 각각의 입력 중에서 입력[0]을 `column`, 입력[1]을 `row`라고 했을 때, 세 개의 입력[0] 중 두 개의 입력[0]이 같은 값이면 나머지 두개도 같은 값이 되어야한다. 내가 풀었던 방법은 다음과 같다.

1. `defaultdict`를 선언한다.
2. `입력[0]`번만 모아놓은 `column` 리스트와 `입력[1]`번만 모아놓은 `row` 리스트를 선언한다.
3. `value`만큼 `+=1` 을 해준다.
4. `index`가 1개인 `column_dict`와 `row_dict`를 각각 `a`와 `b`로 선언해준다.

다른사람의 코드를 보면 굳이 `defaultdict`를 사용하지 않더라도 `count`함수를 사용해서 1개인 값을 출력해 `a`와 `b`에 손쉽게 대입해도 됐었다.

```python
# 나의 코드
from collections import defaultdict
column, row = [], []
a, b = -3333, -3333
column_dic, row_dic = defaultdict(int), defaultdict(int)

for _ in range(3):
    x, y = map(int, input().split())
    column.append(x)
    row.append(y)

for i in range(3):
    column_dic[column[i]] += 1
    row_dic[row[i]] += 1

for key, index in column_dic.items():
    if index == 1:
        a = key

for key, index in row_dic.items():
    if index == 1:
        b = key
print(a, b)
```

```python
# 다른사람의 코드
n = 3
column, row = [], []
a, b = -3333, -3333

for _ in range(3):
    x, y = map(int, input().split())
    column.append(x)
    row.append(y)

for i in range(n):
    if column.count(column[i]) == 1:
        a = column[i]
    if row.count(row[i]) == 1:
        b = row[i]
print(a, b)
```

---
## 📍 백준 2490 - 윷놀이

<a href='https://www.acmicpc.net/problem/2490'>백준 2490 - 윷놀이</a>

## ⚡️ 나의 풀이 
윷짝들의 상태를 보고 `도(A)`, `개(B)`, `걸(C)`, `윷(D)`, `모(E)`를 판별하는 문제다. 윷짝들을 구성하는 값은 0 또는 1임을 알 수있다. 하지만 윷짝들이 주어질 때 0과 1의 순서가 뒤바뀔 수 있음을 인지하자. 나는 총 2가지 방법으로 풀었는데

1. 주어지는 각각의 줄마다 `합(sum)`을 구해 출력을 구분했다.
2. 0과 1의 개수를 파악하도록 `count`함수를 사용했다.

정답판정을 받고 다른 사람의 코드를 봤는데 1번의 `sum`은 입력을 받을 때 한번에 선언해줘도 됐고, 2번의 `count`는 0과 1 둘 다 할 필요없이 둘 중에 하나만 해줘도 구분이 가능했다. 

```python
# sum
yut = [list(map(int, input().split())) for _ in range(3)]

for i in yut:
    if sum(i) == 3:
        print('A')
    elif sum(i) == 2:
        print('B')
    elif sum(i) == 1:
        print('C')
    elif not sum(i):
        print('D')
    elif sum(i) == 4:
        print('E')
```

```python
# count
yut = [list(map(int, input().split())) for _ in range(3)]

for i in yut:
    if i.count(0) == 1 and i.count(1) == 3:
        print('A')
    elif i.count(0) == 2 and i.count(1) == 2:
        print('B')
    elif i.count(0) == 3 and i.count(1) == 1:
        print('C')
    elif i.count(0) == 4:
        print('D')
    elif i.count(1) == 4:
        print('E')
```

```python
# 다른 사람의 코드
# sum
yut = [sum(map(int, input().split())) for _ in range(3)]

for i in yut:
    if i == 3:
        print('A')
    elif i == 2:
        print('B')
    elif i == 1:
        print('C')
    elif not i:
        print('D')
    elif i == 4:
        print('E')

# count
yut = [list(map(int, input().split())) for _ in range(3)]

for i in yut:
    if i.count(0) == 1:
        print('A')
    elif i.count(0) == 2:
        print('B')
    elif i.count(0) == 3:
        print('C')
    elif i.count(0) == 4:
        print('D')
    elif i.count(1) == 4:
        print('E')
```

---
## 📍 백준 1244 - 스위치 켜고 끄기

<a href='https://www.acmicpc.net/problem/1244'>백준 1244 - 스위치 켜고 끄기</a>

## ⚡️ 나의 풀이 
문제가 조금 길었지만, 핵심 포인트는 다음과 같다.

1. 남학생: 자기가 받은 수의 배수인 스위치 번호의 상태를 바꾼다.
2. 여학생: 자기가 받은 수와 같은 번호인 스위치 번호를 중심으로 좌우가 대칭이면서 가장 많은 스위치를 포함하는 구간의 상태를 모두 변경한다.

그리고 처음에 `index`를 편하게 보기위해 `arr[0]`에 이 문제와 관련없는 값인 `-3333`을 넣었다.

남학생의 경우에서 `index`가 `배수`인 경우를 찾을 때 `if not i % target`과 같은 방법을 사용했는데 그럴 필요없이 시작점을 `target`으로 하여 `for i in range(target, n+1, target)`을 선언하면 배수의 `index`만 출력 할 수 있다. 그리고 스위치의 상태를 바꿀 때 `0 -> 1` `1 -> 0` 밖에 없으므로 `1`을 더한 값에 `2`로 나누면 코드를 더욱 간결하게 작성 할 수 있다.

여학생의 경우는 `try, except` 구문을 사용했는데, `target`을 중심으로 `left_index`, `right_index`를 선언한 다음 `left`와 `right`가 같은지 비교하고 같다면 `left`와 `right` 범위를 넓히고 다르다면 종료 시키는 `flag`문을 적용했다. 범위는 무한정으로 늘어날 수 없으므로 `arr[index]`가 벗어나면 `error`가 발생하는데, 이때 `try-except`문을 작성하면 `indexError` 에 걸리지 않는다. 이후 넓혀진 범위 만큼 스위치의 상태를 바꿔야하는데 스위치는 `0 -> 1` `1 -> 0` 밖에 없으므로 `1`을 더한 값에 `2`로 나누면 코드를 더욱 간결하게 작성 할 수 있다.

마지막으로 출력은 한 줄에 `20`개씩 끊어서 출력하는데 이때 `index`를 1부터 시작하여 `i`가 20과 나누어 떨어진다면 줄바꿈해주는 코드인 `print()`를 주면된다.

```python
# 나의 코드
n = int(input())
arr = [-3333] + list(map(int, input().split()))    # append useless index arr[0] 

def male(switch, target):    # male case
    for i in range(1, n + 1):    # change switch state
        if not i % target:
            if not switch[i]:
                switch[i] = 1
            else:
                switch[i] = 0
    return switch

def female(switch, target):    # female case
    left, right = target - 1, target + 1
    flag = True

    try:    # prevent indexError
        while flag:
            if switch[left] == switch[right]:
                left -= 1
                right += 1
            else:
                flag = False
    except:
        pass

    for i in range(left + 1, right):    # change switch state
        if not switch[i]:
            switch[i] = 1
        else:
            switch[i] = 0
    return switch

student = int(input())
for _ in range(student):
    sex, number = map(int, input().split())
    if sex == 1:
        male(arr, number)
    else:
        female(arr, number)
    print(arr)

for i in range(1, len(arr)):    # print each 20 index
    print(arr[i], end=' ')
    if not i % 20:
        print()
```

```python
# 간결한 코드
n = int(input())
arr = [-3333] + list(map(int, input().split()))    # append useless index arr[0] 

def male(switch, target):    # male case
    for i in range(target, n + 1, target):    # change switch state
        switch[i] = (switch[i] + 1) % 2
    return switch

def female(switch, target):    # female case
    left, right = target - 1, target + 1
    flag = True

    try:    # prevent indexError
        while flag:
            if switch[left] == switch[right]:
                left -= 1
                right += 1
            else:
                flag = False
    except:
        pass

    for i in range(left + 1, right):    # change switch state
        switch[i] = (switch[i] + 1) % 2
    return switch

student = int(input())
for _ in range(student):
    sex, number = map(int, input().split())
    if sex == 1:
        male(arr, number)
    else:
        female(arr, number)

for i in range(1, len(arr)):    # print each 20 index
    print(arr[i], end=' ')
    if not i % 20:
        print()
```

---
## 📍 백준 20436 - ZOAC 3

<a href='https://www.acmicpc.net/problem/20436'>백준 20436 - ZOAC 3</a>

## ⚡️ 나의 풀이 
없는 것을 짜낼려니까(?) 조금 힘들었던 문제였다. 

처음에 2차원 리스트로 문자 하나하나씩 끊어서 `keyboard = [['q', 'w', 'e', 'r', 't', 'y', 'u', 'i', 'o', 'p'], ['a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'], ['z', 'x', 'c', 'v', 'b', 'n', 'm']]`로 선언했는데, 이것보다 하단에 있는 코드처럼 하나의 리스트로 감싸고 문자열에 `'str'`처리를 해주면 결과는 동일하지만 코드는 더욱 간결해지는 모습을 볼 수 있다.

이 문제에서 핵심적으로 판단해야하는 부분은 다음과 같다. 

1. 문자를 키보드의 좌표로 변환한다.
`check_coordinate`함수를 선언해서 해당 `key`의 `column`과 `index`의 위치를 반환했다.

2. 현재 문자가 키보드의 한글 자음인지 한글 모음인지 구분한다. 잘 모르겠다면 다음 사진을 보자.

![](https://images.velog.io/images/abcd8637/post/9febecf8-9155-43dd-9cd7-a7faff38f248/KakaoTalk_Photo_2021-06-01-11-16-08.jpeg)

3. 해당 문자열을 출력하는데 걸리는시간을 구한다. 
`문자열의 전체 길이`(각 키를 누르는데 걸리는 시간) + 이전 `key`에서 다음 `key`로 넘어가는 시간 택시거리를 통해 다음 `key`로 넘어가는 시간을 구했는데, 여기서 주의할 점은 입력은 정확히 2글자가 아니기 때문에 기존에 계산한 값을 갱신시켜줘야 한다는 점이다. 


```python
import sys
keyboard = ['qwertyuiop', 'asdfghjkl', 'zxcvbnm']    # keyboard position

def check_coordinate(key):    # find coordinate, index key
    for i in range(3):
        if key in keyboard[i]:
            return i, keyboard[i].index(key)

sl, sr = input().split()
st = sys.stdin.readline().strip()
time, distance = len(st), 0    # 문자열의 전체 길이
  
cur_sl_column, cur_sl_row = check_coordinate(sl)    # 처음 주어지는 sl의 좌표
cur_sr_column, cur_sr_row = check_coordinate(sr)    # 처음 주어지는 sr의 좌표

for i in st:
    column, row = check_coordinate(i)
    if (column <= 1 and row <= 4) or (column == 2 and row <= 3):    # 자음 자판을 입력하는 경우
        distance += abs(cur_sl_column - column) + abs(cur_sl_row - row)    # 택시 거리
        cur_sl_column = column    # cur_column 값 갱신
        cur_sl_row = row    # cur_row 값 갱신
    else:    # 모음 자판을 입력하는 경우
        distance += abs(cur_sr_column - column) + abs(cur_sr_row - row)    
        cur_sr_column = column
        cur_sr_row = row

time += distance    # 문자열의 전체 길이 + `key`가 움직인 총 거리
print(time)
```

---
## 📍 백준 2902 - KMP는 왜 KMP일까?

<a href='https://www.acmicpc.net/problem/2902'>백준 2902 - KMP는 왜 KMP일까?</a>

## ⚡️ 나의 풀이 

이름의 첫번째 글자, 하이픈 뒤는 항상 대문자기 때문에 대문자로 따로 바꿔주는 코드가 따로 필요없다.

1. 하이픈을 기준으로 입력을 나눈다.
2. `names`를 반복문을 돌려 `i[0]`만 출력한다. 사람의 성의 첫 글자만 따서 부르기 때문이다.

```python
import sys
input = sys.stdin.readline

names = input().split('-')

for i in names:
    print(i[0], end='')
```

---
## 📍 백준 2615 - 오목

<a href='https://www.acmicpc.net/problem/2615'>백준 2615 - 오목</a>

## ⚡️ 나의 풀이 

`IndexError`와 `단락연산자`의 중요성을 매우 매우 잘 배운 문제였다..(그만큼 많이 시도했다..) 까먹지 않게 정답판정을 받고 바로 글을 작성하는 중이다.

![](https://images.velog.io/images/abcd8637/post/b2b7a710-cd0c-412a-8a7e-2470420a3a1f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-03%2009.36.32.png)

제일 어려웠던 부분은 `IndexError(범위설정)`, `육목판정` 이고 그 다음은 `가장 왼쪽에 있는 바둑알` 이었다. 내가 작성하면서 코드를 정확히 분석했어야 했는데 미흡해서 아쉬웠다.

큰 흐름은 다음과 같다.
1. 19 * 19 입력을 받는다.
2. 바둑알이 있는 값`(arr[x][y]:)`이 있는지 확인한다.
3. `하`, `우하`, `우`, `우상` 순서로 탐색한다.
4. 현재값과 다음값이 연속으로 있는지 `while`문으로 확인한다.
5. 육목판정 1, 2를 진행한다.
6. 육목판정의 조건을 지났는데도 `cnt == 5`면 오목으로 판단하고 `return` 한다.
7. 승부가 나지 않으면 0을 `return` 한다.

## 🤔 Trial and Error 
1️⃣  `IndexError`
31번 코드를 `while 0 <= nx + dx[i] < n and 0 <= ny + dy[i] < n and arr[x][y] == arr[nx][ny]:`처럼 작성했다. 물론 `IndexError`가 발생했는데, 만약 현재 `cnt = 4`이고 다음 `cnt`를 셀 차례인데, 여기서 `+ dx[i], + dy[i]` 칸 만큼 더 가면 `n`의 범위를 벗어나기 때문에 오류가 발생한다.

2️⃣  `단락연산자`
처음에 35번과 37번 각각 코드 순서를 앞뒤로 바꾸어서 작성했었다.(35번: `if arr[nx][ny] == arr[nx + dx[i]][ny + dy[i]] and 0 <= nx + dx[i] < n and 0 <= ny + dy[i] < n:`, 37번: `if arr[x][y] == arr[x - dx[i]][y - dy[i]] and 0 <= x - dx[i] < n and 0 <= y - dy[i] < n:`) 이렇게 작성하니까 역시 `IndexError`가 발생했는데, 만약 현재좌표 `arr[x][y]`가 `index` 마지막 위치(`arr[n][n]`)에 있다고 가정하면, 다음 비교 할 좌표인 `arr[nx + dx[i]][ny + dy[i]]`는 `n`의 범위를 벗어났기 때문에 비교 할 수 없다. 따라서 오류가 발생한다. 이때 앞 뒤 순서를 바꾸면 앞 조건인 `0 <= nx + dx[i] < n and 0 <= ny + dy[i] < n:`에 먼저 걸리게 되고 이후 단락평가에 의해 뒤 조건은 비교하지 않고 곧바로 `False` 처리한다. 37번 코드도 마찬가지이다.

단락평가를 잘 모르겠다면 <a href='https://ywtechit.tistory.com/26'>이전 글</a>을 보자!

3️⃣ `육목 평가`
연속된 바둑알이 육목인지 판별하는 방법은 2가지가 있다. 첫 번째는 연속된 바둑알의 제일 마지막 좌표와 해당 좌표에서 한 칸(`+ dx[i], + dy[i]`) 더 이동한 좌표가 같은지 살펴보고, 두 번째는 제일 처음 좌표와 해당 좌표에서 한 칸(`- dx[i], - dy[i]`) 덜 이동한 좌표가 같은지 살펴보는 것이다. 말로 복잡해서 아래 사진같이 직접 표로 그려봤다.

![](https://images.velog.io/images/abcd8637/post/9c619cc8-6faa-43a3-819f-b97140ba0a67/KakaoTalk_Photo_2021-06-03-10-25-08.jpeg)

4️⃣ `return 인자 개수`
승부가 났을 때 `return`하는 인자의 개수와 승부가 나지 않았을 때 `return`하는 인자의 개수가 달랐다. 그래서 `return`과 `print()`를 각각 사용하려다가 코드가 깔끔하지 않은 것 같아서 고민하다가 하나만 `return`하는 인자에 임의로 `-1, -1`을 붙여 3개로 맞췄고, 0을 `return`한 값에는 `0`만 출력하게 작성했다. 기발한 발상이었다.


마지막으로 문제를 풀며 작성한 `T.C`를 하나 가져왔는데 문제가 안 풀린다면 테스트해보자. (`19 * 19`로 만들기 귀찮아서 `6 * 6`로 만들었다.)

```python
'''
@ input
1 1 1 1 1 1
1 1 1 1 1 1
1 1 1 1 1 1
1 1 1 1 1 1
0 0 0 0 0 0
2 2 2 2 2 1

@ output
2
6 1
'''
```

이 문제를 풀기 위해 총 3일이 걸렸는데, 오늘 배웠던 내용들을 언젠간 써먹을 수 있게 잊지 말아야겠다.

```python
n = 19
arr = [list(map(int, input().split())) for _ in range(n)]

dx = [1, 1, 0, -1]    # 하(↓), 우하(⬊), 우(➞), 우상(⬈)
dy = [0, 1, 1, 1]    

def omok():
    for x in range(n):
        for y in range(n):
            if arr[x][y]:
                for i in range(4):
                    nx = x + dx[i]
                    ny = y + dy[i]
                    cnt = 1

                    if nx < 0 or ny < 0 or nx >= n or ny >= n:
                        continue

                    while 0 <= nx < n and 0 <= ny < n and arr[x][y] == arr[nx][ny]:
                        cnt += 1

                        if cnt == 5:
                            if 0 <= nx + dx[i] < n and 0 <= ny + dy[i] < n and arr[nx][ny] == arr[nx + dx[i]][ny + dy[i]]:    # 육목 판정 1
                                break
                            if 0 <= x - dx[i] < n and 0 <= y - dy[i] < n and arr[x][y] == arr[x - dx[i]][y - dy[i]]:    # 육목 판정 2
                                break
                            return arr[x][y], x+1, y+1    # 육목이 아닌 오목이면 return

                        nx += dx[i]
                        ny += dy[i]
    return 0, -1, -1    # 승부가 나지 않을 때

color, x, y = omok()
if not color:
    print(color)
else:
    print(color)
    print(x, y)
```

---
## 📍 백준 11586 - 지영 공주님의 마법 거울

<a href='https://www.acmicpc.net/problem/11586'>백준 11586 - 지영 공주님의 마법 거울</a>

## ⚡️ 나의 풀이
2차원 행렬을 좌우, 상하 반전을 할 수 있느냐 없느냐를 묻는 문제였다. 나는 함수를 선언해서 하나하나씩 출력하는 방법을 사용했다. 이번에는 출력에 `sys.stdout`을 사용했는데, 저번에 <a href ='https://ywtechit.tistory.com/134'>유성</a>문제를 푼 이후에 문자열을 `print()`할 때는 뭔가 써야 할것같은 느낌이었다. 그러나 최대 입력이 `10,000`이어서 사용하지 않아도 됐었다. 다음번에 문제 풀 때는 최대 `10,000,000`까지면 `sys.stdout`을 사용해봐야지

정답판정을 받고 다른사람의 코드를 보니까 `*(Asterisk, unpacking)`을 사용해서 코드를 상당히 간결하게 구현했다. 머리속에 번뜩 저런 코드가 떠오르면 얼마나 좋을까?! 번뜩 떠오르는것이 쉽지 않으니 일단 머릿속에 넣자. 😂 😂

```python
# 나의 풀이
import sys
input = sys.stdin.readline

n = int(input())
arr = [input().strip() for _ in range(n)]
K = int(input())

def original():
    for i in range(n):
        for j in range(n):
            sys.stdout.write(arr[i][j])
        sys.stdout.write('\n')

def reverse_row():
    for i in range(n):
        for j in range(n-1, -1, -1):
            sys.stdout.write(arr[i][j])
        sys.stdout.write('\n')

def reverse_column():
    for i in range(n-1, -1, -1):
        for j in range(n):
            sys.stdout.write(arr[i][j])
        sys.stdout.write('\n')

if K == 1:
    original()
elif K == 2:
    reverse_row()
else:
    reverse_column()
```

```python
# 다른 사람의 풀이
n = int(input())
mirror = [input() for _ in range(n)]
k = int(input())

if k == 1:    # 원본 출력
    print(*mirror, sep='\n')
elif k == 2:    # 좌우 반전
    print(*[i[::-1] for i in mirror], sep='\n')
else:    # 상하 반전
    print(*mirror[::-1], sep='\n')
```

---
## 📍 백준 1009 - 분산처리

<a href='https://www.acmicpc.net/problem/1009'>백준 1009 - 분산처리</a>

## ⚡️ 나의 풀이
문제 자체는 어렵지 않았다. 단순하게 `a ** b % 10`을 구하면 되는 문제였는데, 2가지를 신경쓰지 못했다.
1. 정수 `b`의 범위: `1 <= b < 1,000,000`인데, 거듭제곱형태라서 나중에 값이 무한정으로 커지게 된다.
2. `a ** b % 10`: 만약, `a ** b`가 10이 나오면 0이 출력되기 때문에 따로 조건을 넣어줘야한다.

1번은 `**` 대신 `pow` 내장함수를 이용했는데 결론적으로 `x ** y`의 시간복잡도는 `O(N)`이고, `pow(x, y)`의 시간복잡도는 `O(1)`이다. 왜 그런지는 <a href='https://stackoverflow.com/questions/48839772/why-is-time-complexity-o1-for-powx-y-while-it-is-on-for-xy'>스택오버플로우 질문</a>을 참고하자. 그리고 `pow`함수에서 세번째인자까지 넘겨 줄 수 있는데 `pow(base, -exp, mod)` 세번째 인자는 `mod`연산을 할 수 있다.

2번은 `x % 10`를 할 때 `10 % 10`이면 0이 되므로 `0`일 때는 10을 더해주는 조건을 추가했다.

```python
T = int(input())

for _ in range(T):
    a, b = map(int, input().split())
    result = pow(a, b, 10)
    if not result:
        print(result+10)
    else:
        print(result)
```

여담으로 `x ** y`, `pow(x, y)`, `math.pow(x, y)` 함수 중 제일 빠른 함수는 `math.pow(x, y)`인데, 다음 코드를 한번 실행하면 곧장 알 수 있다.

```python
import timeit

def show_timeit(command, setup):
    print(setup + '; ' + command + ':')
    print(timeit.timeit(command, setup))
    print()

# Comparing small integers
show_timeit('a ** b', 'a = 3; b = 4')
show_timeit('pow(a, b)', 'a = 3; b = 4')
show_timeit('math.pow(a, b)', 'import math; a = 3; b = 4')

# Compare large integers to demonstrate non-constant complexity
show_timeit('a ** b', 'a = 3; b = 400')
show_timeit('pow(a, b)', 'a = 3; b = 400')
show_timeit('math.pow(a, b)', 'import math; a = 3; b = 400')

# Compare floating point to demonstrate O(1) throughout
show_timeit('a ** b', 'a = 3.; b = 400.')
show_timeit('pow(a, b)', 'a = 3.; b = 400.')
show_timeit('math.pow(a, b)', 'import math; a = 3.; b = 400.')
```

---
## 📍 백준 1076 - 저항

<a href='https://www.acmicpc.net/problem/1076'>백준 1076 - 저항</a>

## ⚡️ 나의 풀이
저항 문제의 핵심은 첫번째와 두번째 색은 더해주고 마지막 색은 곱해주는 방법인데, 무작정 `str`형으로 바꿔 더해주는 방법만 생각했다. 그것보다 첫번째 색에 `10`을 곱하고 두번째 색은 그대로 더해주는게 가독성이 더 좋았다. 그리고 `10`의 거듭제곱을 이용하면 쉽게 계산 할 수 있는데 규칙을 파악하지 못해 `resisters[color][2]`에 무작정 `10`의 거듭제곱을 넣었다. 다른 사람의 코드를 보니까 규칙의 중요성을 한번 더 느꼈다.

```python
# 나의 코드
colors = [input() for _ in range(3)]
resisters = {'black': [0, 1], 'brown': [1, 10], 'red': [2, 100], 'orange': [3, 1000],
             'yellow': [4, 10000], 'green': [5, 100000], 'blue': [6, 1000000], 'violet': [7, 10000000],
             'grey': [8, 100000000], 'white': [9, 1000000000]}

value = str(resisters[colors[0]][0]) + str(resisters[colors[1]][0])
result = int(value) * resisters[colors[2]][1]

print(result)
```

```python
# 다른 사람의 코드
a = input()
b = input()
c = input()
resisters = {'black': 0, 'brown': 1, 'red': 2, 'orange': 3,
             'yellow': 4, 'green': 5, 'blue': 6, 'violet': 7,
             'grey': 8, 'white': 9}

print((resisters[a] * 10 + resisters[b]) * (10 ** resisters[c]))
```

---
## 📍 백준 3047 - ABC

<a href='https://www.acmicpc.net/problem/3047'>백준 3047 - ABC</a>

## ⚡️ 나의 풀이
문제 따라 대소관계를 비교하면 `C > B > A`가 된다. 그런데, 입력에서 주어진 순서대로 출력해야하므로 `반복문 + 조건문`을 사용하여 출력했다.

```python
# 나의 코드
arr = list(map(int, input().split()))
arr.sort()
A, B, C = arr

for i in input():
    if i == 'A':
        print(A, end=' ')
    elif i == 'B':
        print(B, end=' ')
    else:
        print(C, end=' ')

# 나의 다른 코드
arr = list(map(int, input().split()))
A = min(arr)
C = max(arr)
arr.remove(A)
arr.remove(C)
B = int(*arr)

for i in input():
    if i == 'A':
        print(A, end=' ')
    elif i == 'B':
        print(B, end=' ')
    else:
        print(C, end=' ')
```

---
## 📍 백준 7567 - 그릇

<a href='https://www.acmicpc.net/problem/7567'>백준 7567 - 그릇</a>

## ⚡️ 나의 풀이
단순 구현문제인데, 그릇을 포갤때의 방향이 일치하는지 아닌지 판별하면된다. 맨 처음 그릇은 이전 그릇과 비교 할 수 없기때문에 맨 처음 그릇의 점수 10점을 선언해준상태에서 반복문의 범위를 `index`가 1인 지점부터 len(bowl)까지 확인한다. 반복문내부에서 `이전 그릇과 같으면 5점을 누적`시키고, `다르면 10점을 누적`시킨다.

```python
bowl = input()
score = 10

for i in range(1, len(bowl)):
    if bowl[i-1] == bowl[i]:
        score += 5
    else:
        score += 10
print(score)
```

---
## 📍 백준 16935 - 배열 돌리기 3

<a href='https://www.acmicpc.net/problem/16935'>백준 16935 - 배열 돌리기 3</a>

## ⚡️ 나의 풀이
2차원배열을 `상하`, `좌우`, `시계 방향으로 90도 회전`, `반시계 방향으로 90도 회전`, `부분 배열 시계방향 회전`, `부분 배열 반시계방향 회전` 하는 문제다. 이 문제를 풀 때 `indexError`를 조심하자.

3번, 4번 연산에서는 반복문의 범위를 `n`, `m`을 서로 바꿔주었는데, `n != m` 일때 범위가 달라지기 때문이다. 그래서 `temp` 선언도 서로 자리를 바꿔주었다. 주의할점은 마지막에 `oper`를 실행시킬 때 `n, m = m, n`을 선언해줘서 가로, 세로가 바뀌지 않게 선언하자. 

5번, 6번 연산은 조금 어려울 수 있는데 규칙을 알면 어렵지 않다.(규칙을 찾는 과정이 어렵긴하지만..😅) 다음 사진을 보자.

![](https://images.velog.io/images/abcd8637/post/9d376d99-9fb5-4ab7-8d2b-182e0d5b18c5/KakaoTalk_Photo_2021-06-15-11-25-26.jpeg)

1. `arr`과 범위는 같지만 값은 0인 `temp`를 선언한다.
2. `a`를 `2`로 옮겨야하므로 `arr`의 `a` 좌표를 가져올 반복문을 선언한다.
3. `a`의 첫번째 좌표부터 시작해서 `b`의 첫번째 좌표와 하나씩 넣을 수 있게 설정한다.
4. 나머지 `b`, `c`, `d`좌표도 동일한 과정을 거친다.
   
```python
def calc_1():
    temp = [[0] * m for _ in range(n)]
    for i in range(n):
        temp[i] = arr[n-1-i]
    return temp

def calc_2():
    temp = [[0] * m for _ in range(n)]
    for i in range(n):
        for j in range(m):
            temp[i][j] = arr[i][m-1-j]
    return temp

def calc_3(arr, n, m):
    temp = [[0] * n for _ in range(m)]
    for i in range(m):
        for j in range(n):
            temp[i][j] = arr[n-1-j][i]
    return temp

def calc_4(arr, n, m):
    temp = [[0] * n for _ in range(m)]
    for i in range(m):
        for j in range(n):
            temp[i][j] = arr[j][m - 1 - i]
    return temp

def calc_5():
    temp = [[0] * m for _ in range(n)]
    for i in range(n // 2):    # move position: 1 -> 2
        for j in range(m // 2):
            temp[i][j + m // 2] = arr[i][j]

    for i in range(n // 2):    # move position: 2 -> 3
        for j in range(m // 2, m):
            temp[i + n // 2][j] = arr[i][j]

    for i in range(n // 2, n):    # move position: 3 -> 4
        for j in range(m // 2, m):
            temp[i][j - m // 2] = arr[i][j]

    for i in range(n // 2, n):    # move position: 4 -> 1
        for j in range(m // 2):
            temp[i - n // 2][j] = arr[i][j]

    return temp

def calc_6():
    temp = [[0] * m for _ in range(n)]
    for i in range(n // 2):    # move position: 1 -> 4
        for j in range(m // 2):
            temp[i + n // 2][j] = arr[i][j]

    for i in range(n // 2, n):    # move position: 4 -> 3
        for j in range(m // 2):
            temp[i][j + m // 2] = arr[i][j]

    for i in range(n // 2, n):    # move position: 3 -> 2
        for j in range(m // 2, m):
            temp[i - n // 2][j] = arr[i][j]

    for i in range(n // 2):    # move position: 2 -> 1
        for j in range(m // 2, m):
            temp[i][j - m // 2] = arr[i][j]

    return temp

n, m, r = map(int, input().split())
arr = [list(map(int, input().split())) for _ in range(n)]
operation = list(map(int, input().split()))

for oper in operation:
    if oper == 1:
        arr = calc_1()
    elif oper == 2:
        arr = calc_2()
    elif oper == 3:
        arr = calc_3(arr, n, m)
        n, m = m, n
    elif oper == 4:
        arr = calc_4(arr, n, m)
        n, m = m, n
    elif oper == 5:
        arr = calc_5()
    else:
        arr = calc_6()

for i in arr:
    print(*i)
```

---
## 📍 백준 11723 - 집합

<a href='https://www.acmicpc.net/problem/11723'>백준 11723 - 집합</a>

## ⚡️ 나의 풀이
`add`와 `remove`에서 중복된 경우는 무시한다는 조건을 보아 `set`자료형을 사용했다. 그런데, 정답을 제출하니까 `keyError`가 떴었다 뭐때문인지 찾아보다가 `remove` 함수 때문이었는데, 값이 없는 경우에 `remove`를 사용하게 되면 `keyError`가 난다. 이럴 때는 `discard`함수를 사용하자. 값이 없는 상태에서 `discard`를 사용해도 에러가 나지 않는다. 또 `empty`는 빈 집합으로 바꿔야하는데 그냥 `set()`으로 초기화해줘도 되지만 `clear` 함수를 사용해줘도 된다. 시간복잡도는 크게 차이가 없었다.


```python
import sys
input = sys.stdin.readline

empty_set = set()

def add(x):
    empty_set.add(x)

def remove(x):
    empty_set.discard(x)

def check(x):
    if x in empty_set:
        return 1
    return 0

def toggle(x):
    if x in empty_set:
        empty_set.discard(x)
    else:
        empty_set.add(x)

def set_all():
    global empty_set
    empty_set = {i for i in range(1, 21)}

def empty():
    empty_set.clear()

for _ in range(int(input())):
    command = input().split()
    if command[0] == 'add':
        add(int(command[1]))
    elif command[0] == 'remove':
        remove(int(command[1]))
    elif command[0] == 'check':
        print(check(int(command[1])))
    elif command[0] == 'toggle':
        toggle(int(command[1]))
    elif command[0] == 'all':
        set_all()
    else:
        empty()
```

---
## 📍 백준 10820 - 문자열 분석

<a href='https://www.acmicpc.net/problem/10820'>백준 10820 - 문자열 분석</a>

## ⚡️ 나의 풀이

1. 문자열 `n`개가 몇 번째까지인지 모르기 때문에 `try except`를 사용했다.(`except EOFError`)
2. 소문자: `islower()`, 대문자: `isupper()`, 숫자: `isdigit()`, 공백: `else`
3. 각 `count`누적

```python
while True:
    try:
        lower_case, upper_case, number, blank = 0, 0, 0, 0

        for i in input():
            if i.islower():
                lower_case += 1
            elif i.isupper():
                upper_case += 1
            elif i.isdigit():
                number += 1
            else:
                blank += 1
        print(lower_case, upper_case, number, blank)

    except EOFError:
        break

```

---
## 📍 백준 1292 - 쉽게 푸는 문제

<a href='https://www.acmicpc.net/problem/1292'>백준 1292 - 쉽게 푸는 문제</a>

## ⚡️ 나의 풀이
문제 이름은 쉽게 푸는 문제였는데 나는 어렵게 푼 문제였다. 구간의 시작과 끝을 기준으로 구간 합을 구해야 하기 때문에 `prefix_sum`을 이용했다. `1, 2, 2, 3, 3, 3, 4, 4, 4, 4 ...` 수열을 만들때 더 쉽게 떠올릴 수 있어야하는데 `str`형으로 어렵게 푼것 같다.

나의 풀이

1. `arr`에 `0`을 넣은 상태로 선언한다. (`index` 고려)
2. `a`, `b`를 입력받는데 `b`는 `index`를 고려 할 값이기 때문에 반복문의 범위를 반으로 줄였다. 
3. `cnt`는 `1`씩 증가하면서 똑같은 값이 하나씩 증가한다.
4. `현재 항`과 `이전 항`을 더해 `누적 합`을 계산해준다.
5. `arr[b] - arr[a-1]`으로 `구간 합`을 구한다.

정답판정을 맞고 다른사람의 코드를 봤는데 코드길이가 반으로 줄 정도로 간단한 문제였는지 몰랐다. 😅 😅

다른사람의 풀이

1. `a`, `b`의 범위는 `1,000`까지였기 때문에 반복문의 범위는 `46`까지만 구해도 된다. (`len(arr) = 1036`)
2. `i`값을 기준으로 이중 반복문을 사용하는데 빈 `arr`에 `i`를 추가한다. 값이 `1`부터 `arr`에 들어간다. (`j`를 추가하는 것이 아님!!)
3. `sum`함수를 이용해서 풀었다.(구간합을 구하지 않고 기존 arr에서 사용가능하다.)

`구간 합`을 구할 때 `누적 합`을 구하지 않고도 `sum + slicing` 함수로 구할 수 있다는 것을 배웠다.

```python
# 나의 코드
a, b = map(int, input().split())

arr = [0]
cnt = 1
for i in range(1, (b+1) // 2 + 1):    # 범위를 반으로 나눠서 시간 단축
    for j in range(cnt):
        arr.append(cnt)
    cnt += 1

for i in range(1, b+1):
    arr[i] += arr[i-1]
print(arr[b] - arr[a-1])
```

```python
# 다른 사람의 코드
a,b = map(int,input().split())

arr = [0]
for i in range(46):
    for j in range(i):
        arr.append(i)

print(sum(arr[a:b+1]))
```

---
## 📍 백준 6359 - 만취한 상범

<a href='https://www.acmicpc.net/problem/6359'>백준 6359 - 만취한 상범</a>

## ⚡️ 나의 풀이
언뜻 보면 저번에 풀었던 <a href='https://ywtechit.tistory.com/144'>백준 1244 - 스위치 켜고 끄기</a>문제와 비슷한데, 범위 전체를 살펴보면서 상태를 바꾼다는 점이 조금 다르다. (`1244` 문제는 주어진 n의 배수만 상태를 바꾸면 됐음)

주어진 문제 그대로 구현하다보니까 생각을 잘 못했는데 `1 ~ 2` 라운드도 `3 ~ k` 라운드와 마찬가지로 열려있으면 잠그고, 잠겨있다면 여는 방법을 사용해도 답은 같게 나온다.
그리고 `1, 0` 상태를 바꿀 때 `🍯 tip`인데 `if not gate[j]: gate[j] = 1` or `if gate[j]: gate[j] = 0` 대신 `gate[j] = (gate[j] + 1) % 2`를 사용해도 결과는 같지만 코드는 훨씬 간결해진다. <a href='https://ywtechit.tistory.com/146'>이전</a> 에 공부한 내용이다. 다른사람의 코드를 보니까 경악을 금치 못했는데 제곱근으로 구했다.(어떻게 저런 생각을.. 🤭 🤭) `1 ~ 3: 1`, `4 ~ 9: 2` 이런 규칙을 잘 봤어야하는데 아쉽다!

처음 푼 흐름 
1. `n`만큼 수를 초기화 한다. (`-3333`은 `index`를 쉽게 계산하려고 넣었다.)
2. `1 ~ 2` 라운드에서 `2`의 배수만 상태를 바꾼다.
3. `3 ~ n` 라운드까지 `i`의 배수 자리만 상태를 바꾼다.

나중에 푼 흐름
1. `n`만큼 수를 초기화 한다. (`-3333`은 `index`를 쉽게 계산하려고 넣었다.)
2. `1 ~ n` 라운드까지 `i`의 배수 자리만 상태를 바꾼다.

다른 사람의 코드
1. 제곱근을 구한다. `int(n**0.5)` 

```python
# 나의 코드
T = int(input())

def game(n):
    gate = [-3333]    # declare garbage value for easy count index
    gate += [1] * n    # 0: close, 1: open

    for i in range(1, n + 1):    # 1 ~ 2 round
        if not i % 2:
            gate[i] = 0

    for i in range(3, n + 1):    # 3 round ~ n round
        for j in range(i, n + 1, i):  
            gate[j] = (gate[j] + 1) % 2

    return gate.count(1)    # count open gate

for _ in range(T):
    n = int(input())
    print(game(n))
```

```python
# 단축 코드
T = int(input())

def game(n):
    gate = [-3333]    # declare garbage value for easy count index
    gate += [1] * n    # 0: open, 1: closed

    for i in range(1, n + 1):
        for j in range(i, n + 1, i): 
            gate[j] = (gate[j] + 1) % 2
        print(gate)

    return gate.count(0)    # count open gate

for _ in range(T):
    n = int(input())
    print(game(n))
```

```python
# 다른 사람의 코드
T = int(input())
for i in range(T):
    n = int(input())
    print(int(n ** 0.5))
```