### dynamic_programming(다이나믹 프로그래밍)
다이나믹 프로그래밍은 메모리 공간을 약간 더 사용해 연산 속도를 비약적으로 증가시키는 방법으로, 동적 계획법이라고도 표현한다.

### 📍 예시 - 피보나치 수열
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