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

### ⚡️ [ 문제 1 ] - 1로 만들기
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