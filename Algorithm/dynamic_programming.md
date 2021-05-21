### dynamic_programming(다이나믹 프로그래밍)
다이나믹 프로그래밍은 메모리 공간을 약간 더 사용해 연산 속도를 비약적으로 증가시키는 방법으로, 동적 계획법이라고도 표현한다.

### 📍 [ 예시 ] - 피보나치 수열
```python
# dynamic_recursive(top_down)
memo = [0] * 100

def fibo(x):
    if x == 1 or x == 2:
        return 1
    if memo[x] != 0:
        return memo[x]
    memo[x] = memo[x-1] + memo[x-2]
    return memo[x]
print(fibo(99))
```

```python
# dynamic_for(bottom_up)
memo = [0] * 100
memo[1] = 1
memo[2] = 1
n = 99

for i in range(3, n+1):
    memo[i] = memo[i-1] + memo[i-2]
print(memo[n])
```

---

### ⚡️ [ 문제 1 ] - 1로 만들기
<a href='https://www.acmicpc.net/problem/1463'>유사문제: 1로 만들기</a>

다음 정수 X가 주어질 때 정수 X에 사용할 수 있는 연산은 다음과 같이 4가지이다.
>1. X가 5로 나누어떨어지면, 5로 나눈다.
>2. X가 3으로 나누어떨어지면, 3으로 나눈다.
>3. X가 2로 나누어떨어지면, 2로 나눈다.
>4. X에서 1을 뺀다.

```python
'''
26
'''
n = int(input())

# DP 테이블 초기화
memo = [0] * 30001

for i in range(2, n+1):
    memo[i] = memo[i-1] + 1
    # 현재 수가 2로 나누어 떨어지는 경우
    if i % 2 == 0:
        memo[i] = min(memo[i], memo[i // 2] + 1)
    # 현재 수가 3으로 나누어 떨어지는 경우
    if i % 3 == 0:
        memo[i] = min(memo[i], memo[i // 3] + 1)
    # 현재 수가 5로 나누어 떨어지는 경우
    if i % 5 == 0:
        memo[i] = min(memo[i], memo[i // 5] + 1)
print(memo[n])
👉🏽 3
```
---

### ⚡️ [ 문제 2 ] - 바닥공사
가로의 길이가 N, 세로의 길이가 2인 직사각형 형태의 얇은 바닥이 있다. 태일이는 이 얇은 바닥을 1 x 2의 덮개, 2 x 1의 덮개, 2 x 2 덮개를 이용해 채우고자 한다.

이때, 바닥을 채우는 모든 경우의 수를 구하는 프로그램을 작성하시오. 예를 들어 2 x 3 크기의 바닥을 채우는 경우의 수는 5가지이다.

이 문제는, 점화식을 세우면 간단하게 풀 수 있는 문제이다.
먼저, `N`이 1, 2, 3으로 변할 때마다 경우의수가 어떻게 달라지는지 직접 계산해보자.

재귀함수를 호출하는 `top_down`방식과, 
반복문을 사용하는 `bottom_up` 방식을 사용 할 수 있다.

```python
'''
3
'''
# top_down
n = int(input())

d = [0] * 1001

def tile(x):
    if x == 1:
        d[1] = 1
    if x == 2:
        d[2] = 3

    if d[x] != 0:
        return d[x]

    d[x] = (tile(x-1) + (2*tile(x-2))) % 796796
    return d[x]

print(tile(n))
👉🏽 5
```

```python
'''
3
'''
# bottom_up
n = int(input())

d = [0] * 1001

d[1] = 1
d[2] = 3

for i in range(3, n+1):
    d[i] = (d[i-1] + (2 * d[i-2])) % 796796

print(d[n])
👉🏽 5
```

---

### ⚡️ [ 문제 3 ] - 2 x N 타일링
<a href='https://www.acmicpc.net/problem/11726'> 문제 </a>

<a href='https://www.acmicpc.net/problem/11727'> 유사문제 </a>


```python
'''
2

9
'''
n = int(input())

d = [0] * 1001

d[1] = 1
d[2] = 2

for i in range(3, n+1):
    d[i] = (d[i-1] + d[i-2]) % 10007
print(d[n])
👉🏽 2
👉🏽 55
```

---
### ⚡️ [ 문제 4 ] 개미전사

식량차고를 털지 안 털지를 결정하는 경우, 
특정한 i번째 식량차고에 대해 털지 안 털지의 여부를 생각하자.

> a(i) = max(a(i-1), a(i-2) + k(i))

```python
n = int(input())

array = list(map(int, input().split()))

d = [0] * 102

d[0] = array[0]
d[1] = max(array[0], array[1])

for i in range(2, n):
    d[i] = max(d[i-1], d[i-2] + array[i])

print(d[n-1])
```

---
### ⚡️ [ 문제 5 ] 효율적인 화폐 구성
그리디에서 다루었던 거스름돈 문제와 거의 동일하나, 화폐 단위가 큰 단위가 작은 단위의 배수가 아니라는 점에서 `Greedy` 대신 `DP`를 사용하여 해결한다.

> 1. 방법이 존재하는 경우: `a(i) = min(a(i), a(i-k)+1 )`
> 2. 방법이 존재하지 않는 경우: `a(i) = 10,001`


```python
'''
2 15
2
3

3 4
3
5
7
'''
n, m = map(int, input().split())

array = []
for i in range(n):
    array.append(int(input()))

d = [10001] * (m+1)

d[0] = 0

for i in range(n):
    for j in range(array[i], m+1):
        d[j] = min(d[j], d[j - array[i] + 1])

# M원을 만드는 방법이 없는 경우
if d[m] == 10001:
    print(-1)
else:
    print(d[m])
👉🏽 5 -1
```
---


### ⚡️ [ 문제 6 ] 백준 1219 - 연속합
<a href='https://www.acmicpc.net/problem/1219'> 문제 </a>

<a href=''>참조링크</a>

만약, `array`의 현재값보다 이전 `d`의 최대값 + `array`의 현재값이 더 크면 `d` 현재값은 `array현재값 + d 이전값`

그렇지 않으면, `d` 현재값 = `array 현재값`

```python
'''
10
10 -4 3 1 5 6 -35 12 21 -1

10
2 1 -4 3 4 -4 6 5 -5 1

5
-1 -2 -3 -4 -5
'''
import sys
n = int(input())

array = list(map(int, sys.stdin.readline().split()))

d = [0] * n
d[0] = array[0]

for i in range(1, n):
    if d[i-1] + array[i] > array[i]:
        d[i] = d[i-1] + array[i]
    else:
        d[i] = array[i]

result = max(d)
print(result)
👉🏽 33 14 -1
```
---
### ⚡️ [ 문제 7 ] 코드업 3704 - 계단 오르기 2
<a href='https://codeup.kr/problem.php?id=3704'> 문제 </a>

피보나치 수열 변형 문제이다.
` d[i] = d[i-1] + d[i-2] + d[i-3]`
점화식이 3개까지 있기 때문에 초기값도 3개를 선언해줬다. 
`for`문 범위설정에 주의하자.

```python
'''
5
'''
n = int(input())

d = [0] * 100001

d[1] = 1
d[2] = 2
d[3] = 4

for i in range(4, n+1):
    d[i] = (d[i-1] + d[i-2] + d[i-3]) % 1000

print(d[n])
👉🏽 13
```

---
## 📍 코드업 4564 - 계단 오르기
<a href='https://codeup.kr/problem.php?id=4564'>코드업 4564 - 계단 오르기</a>

### ⚡️ 나의 풀이
전형적인 DP문제였는데, 나한테는 어려웠다. 코드보다 규칙을 찾는것이 어려웠다.
이전에 풀었던 <a href='https://codeup.kr/problem.php?id=3704'>계단 오르기2</a> 문제와 비슷하다고 생각했다.

처음에 계단에 올라갈 수 있는 경우의 수를 계산했는데, 예외가 발생해 점화식을 완성시키지 못했다.
일반적인 사고라면 앞에서부터 몇 칸씩 어떻게 올라갈지 고민했는데, 이 문제는 뒤에서부터 고민해야 문제를 풀 수 있었다.

먼저 n개의 계단마다 올라갈 수 있는 방법을 찾아보자. 그 전에 문제 조건을 잊지말자.
>1. 계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다. 즉, 한 계단을 밟으면 이어서 다음 계단이나, 다음 다음 계단으로 오를 수 있다.
>2. 연속된 세 개의 계단을 모두 밟아서는 안된다. 단, 시작점은 계단에 포함되지 않는다.
>3. 마지막 도착 계단은 반드시 밟아야 한다.

n개일때 올라갈 수 있는 방법은 다음과 같다.

그런데, 우리는 앞에서가 아닌 뒤에서부터 방법을 생각해야한다. 예를 들어 4개의 계단을 올라갈 때 생각해보자.
마지막 계단의 번호가 4라면 올라 갈 수 있는 방법이 2가지로 나뉜다.
>1. 3을 밟고 4를 밟을 때: f(4) = f(4) + f(3) + f(1)
>2. 3을 밟지 않고 4를 밟을 때: f(4) = f(4) + f(2) + ...

그렇다면 n개의 계단을 올라갈 땐 어떻게 될까?
>1. `n-1`을 밟을 때: f(n) = f(n) + f(n-1) + f(n-3) + ...
>2. `n-1`을 밟지 않을 때: f(n) = f(n) + f(n-2) + ...

이 때 `DP`를 사용해서 이전항까지 계산한 값을 가져올 수 있다.
`n-1`을 밟을 때 `n-3`항부터는 어떻게 올라왔는지 알 수 없으니까 `DP(n-3)`을 통해 최대값을 가져오자.
`n-1`을 밟지 않을 때 `n-2`항부터는 어떻게 올라왔는지 알 수 없으니까 `DP(n-2)`을 통해 최대값을 가져오자.

`DP`를 적용하면
>1. n-1을 밟을 때: f(n) = f(n) + f(n-1) + DP(n-3)
>2. n-1을 밟지 않을 때: f(n) = f(n) + DP(n-2)
이렇게 정리 할 수 있다.

처음에 score, stairs를 n+3까지 선언해준 이유는 1, 2, 3항의 값이 정해져 있기 때문이다.

```python
n = int(input())

score = [0] * (n+3)
stairs = [0] * (n+3)

for i in range(1, n+1):
    stairs[i] = int(input())

score[1] = stairs[1]
score[2] = stairs[1] + stairs[2]
score[3] = max(stairs[3] + stairs[1], stairs[2] + stairs[3])

for i in range(4, n+1):
    score[i] = max(stairs[i] + score[i-2], stairs[i] + stairs[i-1] + score[i-3])

print(score[n])
```

---
## 📍 이것이 코딩 테스트다 DP - 개미 전사
<a href='https://www.youtube.com/watch?v=5Lu34WIx2Us'>유튜브 - 동빈나(27:48)</a>

### ⚡️ 나의 풀이
3개월 전에 풀었던 문제이지만, 어떻게 풀었는지 기억이 잘 안나서 다시 풀어봤다.
문제를 풀어보면 알겠지만 <a href='https://www.acmicpc.net/problem/2579'>boj_2579 - 계단 오르기</a>와 비슷한 유형이다.

입력부분에서 맨 앞에 0을 주고 싶었는데 그렇게 되면 입력 받는부분이 까다로워질수 있어 처음부터 입력값을 주었다. 그러면 출력으로 `n-1`을 줘야된다는 점을 잊지말자!

풀이 영상을 보면서 동빈나가 DP를 써야하는 경우를 알려주셨는데 기억해야 하는 내용이다.
1. 최적부분: 특정 `i`번째까지 최적의 해를 구할 때 이전값을 사용한다.

여기에서 제일 중요한 포인트는 개미가 식량창고를 털 때 두가지의 케이스가 있다.
관점을 달리해서 뒤에서부터 살펴보자.

![](https://images.velog.io/images/abcd8637/post/1aa099ef-93ca-4db0-ac9c-274f2c5683d7/KakaoTalk_Photo_2021-04-23-12-26-11.jpeg)

1. 제일 마지막 i번째 식량창고를 턴다: d[i] = food[i] + d[i-2]
2. 제일 마지막 i번째 식량창고를 털지 않는다: d[i] = d[i-1]

2번에서 `d[i-3]`을 넣지 않은 이유는 이미 `table`에 값을 저장해놨기 때문이다. 

```python
'''
4
1 3 1 5
'''

n = int(input())
food = list(map(int, input().split()))
d = [0] * 101

d[0] = food[0]
d[1] = max(food[0], food[1])

for i in range(2, n):    
    d[i] = max(food[i] + d[i - 2], d[i - 1])

print(d[n - 1])
```

---
## 📌 백준 2167 - 2차원 배열의 합

[문제 설명](https://www.acmicpc.net/problem/2167)

---

## 💡 나의 풀이

시간 복잡도를 줄여주는 `구간 합(prefix_sum)`으로 구하면 쉽게 풀 수 있는 문제인데, 지금까지 [1차원 배열의 구간합](https://ywtechit.tistory.com/78?category=930709)만 해봤어서 2차원 배열 일 때 어떻게 사용해야 하는지 방법을 잘 몰랐었다.

1차원 배열에서 누적 합을 어떻게 구했었는지 한번 살펴보자. `누적 합` -> `구간 합` 순서로 살펴볼 것이다.

1.  누적 합 구하기  
    누적합을 구현하는 방법은 2가지가 있다. `append`방법과 `memoization`방법인데, 기억이 잘 안 난다면 다음 코드를 살펴보자. `arr = [10, 20, 30, 40, 50]`은 고정이다.

```python
arr = [10, 20, 30, 40, 50]

# append
value = 0
append_sum = [0]

for i in arr:
    value += i
    append_sum.append(value)

print(append_sum)
👉🏽 [0, 10, 30, 60, 100, 150]

# memoization
memo_sum = [0] * (len(arr)+1)

for i in range(1, len(arr)+1):
    memo_sum[i] = arr[i-1] + memo_sum[i-1]
    
print(memo_sum)
👉🏽 [0, 10, 30, 60, 100, 150]
```

두 방식의 차이점은 누적합 배열 전체를 0으로 선언했는지 안 했는지 차이고, 나머지는 기존 `arr`의 값에 내가 구하려고하는 값 이전까지 누적합을 더하는 방식인데 다음 사진을 보면 이해가 될 것이다.

![](https://images.velog.io/images/abcd8637/post/6dd69d08-b148-4fff-843e-b1c141d414c1/KakaoTalk_Photo_2021-05-10-11-32-50.jpeg)

이제 2차원 배열에서의 누적합을 구해보자. 1차원 배열에서는 방금 같은 과정으로 데이터를 선형적인 방향으로 저장할 수 있지만, 2차원 배열은 행과 열 모두 생각해야 한다. 그래서 `memoization` 방법을 사용했다. 

문제에서 제시된 2차원 배열 `3*4`형태인 `[[1, 2, 4], [8, 16, 32]]`를 기준으로 생각해보자. 1차원 배열 \[0\] 번째에 더미 데이터(dummy\_data) 0을 준 것처럼 2차원 배열에서도 첫 번째 행과 첫 번째 열에 더미 데이터인 0을 주자. 

예를 들어 memo\[1\]\[1\]을 구하려면 `arr[0][0] - memo[0][1] - memo[1][0] + memo[0][0]`을 해주면 되고, memo\[2\]\[2\]를 구하려면 `arr[1][1] - memo[1][2] - memo[2][1] + memo[1][1]`을 해주면 된다.

마지막에 `memo[1][1]`을 더해주는 이유는 앞에서 2번을 중복해서 뺐기 때문에 더해준 것이다. 

![](https://images.velog.io/images/abcd8637/post/a49146b1-85d9-45de-a2e1-de4fb41d7924/KakaoTalk_Photo_2021-05-10-11-32-58.jpeg)

2.  구간 합 구하기

1차원배열에서 구간 합은 현재 구하려고 하는 값 - 이전까지의 값 중 구하려는 값을 제외한 부분으로 나타낼 수 있다. 그럼 2차원 배열에서는 어떻게 구할까? 1번에서 누적 합을 구한 것처럼 행과 열 모두 생각해줘야 하는데 다음 사진처럼 나타 낼 수 있다. 중요한 것은 중복되는 부분을 더해주는 것이다.

![](https://images.velog.io/images/abcd8637/post/cc09f91d-b6b5-4074-a838-483c4ee266c2/KakaoTalk_Photo_2021-05-10-11-32-54.jpeg)

1번과 2번과정을 통틀어 헷갈리지 말아야 하는점은 누적합은 중복된 부분을 빼주고 구간 합은 중복된 부분을 더하는 것이다.

설명이 길었지만 코드는 단순하다.

```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
arr = [list(map(int, input().split())) for _ in range(n)]
memo = [[0] * (m+1) for _ in range(n+1)]

for i in range(1, n+1):
    for j in range(1, m+1):
        memo[i][j] = arr[i-1][j-1] + memo[i][j-1] + memo[i-1][j] - memo[i-1][j-1]

k = int(input())
for _ in range(k):
    i, j, x, y = map(int, input().split())
    print(memo[x][y] - memo[i-1][y] - memo[x][j-1] + memo[i-1][j-1])
```

---
## 📌 백준 9625 - BABBA

<a href='https://www.acmicpc.net/problem/9625'>백준 9625 - BABBA</a>

## 💡 나의 풀이
전형적인 `DP(Dynamic Programming)`문제였으나, 처음에 문제 그대로 `i`가 증가하면 바뀌는 문자열을 새로운 배열에 넣고 마지막에 총 몇 개인지 `count`를 사용하여 풀다가 시간초과 판정을 받았다.

그래서 어떤 규칙이 있는지 살펴보니까 전체 `A, B` 총 개수를 구할 필요는 없고 `A`, `B`의 개수를 따로따로 구하면 된다. `a[i] = a[i-1] + a[i-2]`인 전형적인 `피보나치(Fibonacci)`수열 형태를 보였다.

나는 `DP`를 사용할때 전체 `k`의 최대값를 선언했는데, 그럴 필요없이 `k+1`만큼만 줘서 그때그때 계산해도 된다. 또, 새롭게 배운점은 `a[0] = 1, a[1] = 0` 대신, 처음부터 `a=[1,0]`을 선언하고 `DP 반복문`에서 나온값을 `append`하는 방법을 사용해도 된다.

```python
# 나의 코드
k = int(input())
n = 46

a = [0] * 46
a[0] = 1
a[1] = 0

b = [0] * 46
b[0] = 0
b[1] = 1

for i in range(2, n):
    a[i] = a[i - 1] + a[i - 2]
    b[i] = b[i - 1] + b[i - 2]
print(a[k], b[k])
```

```python
# 다른사람의 코드
k = int(input())

a = [1, 0]
b = [0, 1]

for i in range(2, k+1):
    a_num = a[i-1] + a[i-2]
    a.append(a_num)
    b_num = b[i-1] + b[i-2]
    b.append(b_num)

print(a[k], b[k])
```



