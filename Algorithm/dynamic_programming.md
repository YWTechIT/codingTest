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
