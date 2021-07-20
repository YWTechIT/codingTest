## simulation
알고리즘을 각 한 단계씩 직접 수행하는 알고리즘. `Brute_force`와 함께 구현의 핵심 알고리즘이 되는 경우가 많다.
`N x N Matrix` 문제로 자주 출제 됨.

시뮬레이션에서 배열의 범위는 처음에 선언하지 않고 나중에 `if`문으로 배열을 벗어났을 때, 벗어나지 않았을 때를 설정해 줄 수 있다.
---

## 📍 [ 문제 ] 상하좌우

```python
n = int(input())
directions = input().split()
vector = ['L', 'R', 'U', 'D']

# 최초위치
x, y = 1, 1

# 좌우상하 방향벡터 선언
# 행 Index
dx = [0, 0, -1, 1]
# 열 Index
dy = [-1, 1, 0, 0]

for direction in directions:
    for i in range(len(vector))
        if direction == vector[i]:
            nx = n + dx[i]
            ny = n + dy[i]
    
    if nx < 1 or ny < 1 or nx > n or ny > n:
         continue
    x, y = nx, ny

print(nx, ny)
👉🏽 입력
5 
R R R U D

👉🏽 출력
3 4
```

---
## 📍 [ 문제 ] 왕실의 나이트
`cases`변수가 `dx`, `dy`기능을 대신하며, 이동할 방향을 기록할 수 있게 하였다.
첫번째 코드는 `cases`변수 선언하여 `dx, dy`의 코드를 넣고 `new_array`, `new_row`를 계산할 때 `dx = case[0]`, `dy = case[1]`과 같은 역할을 하게함.

```python
data = input()
column = int(chr(ord(data[0]) - 48))
row = int(data[1])
count = 0

cases = [(-2, -1), (-2, 1), (2, -1), (2, 1), (-1, -2), (1, -2), (-1, 2), (1, 2)]

for case in cases:
    new_column = column + case[0]
    new_row = row + case[1]
    if new_column > 0 and new_row > 0 and new_column <= 8 and new_row <= 8:
        count = count + 1
        print(new_row, new_column)
print(count)
👉🏽 입력: al
👉🏽 출력: 2
```

두번째 코드는 `dx, dy`변수 사용함.

```python
data = input()
column = int(chr(ord(data[0]) - 48))
row = int(data[1])
count = 0

move_types = [True for _ in range(8)]
dx = [-2, -2, 2, 2, -1, 1, -1, 1]
dy = [-1, 1, -1, 1, -2, -2, 2, 2]

for i in range(len(move_types)):
    nx = column + dx[i]
    ny = row + dy[i]
    if nx > 0 and ny > 0 and nx <= 8 and ny <= 8:
        count = count + 1
print(count)
👉🏽 입력: al
👉🏽 출력: 2
```

---
## 📍 백준 10804 - 카드 역배치

<a href='https://www.acmicpc.net/problem/10804'>백준 10804 - 카드 역배치</a>

## ⚡️ 나의 풀이

1. 카드를 0부터 20까지 선언한다 (`0`을 추가한 이유는 `index`를 편하게 계산하기 위해서)
2. 카드 뒤바꿀 범위를 입력 받는다.
3. 새로운 변수에 카드를 뒤바꿀 위치만 `[::-1]` 선언하고 뒤바꾸지 않는 범위는 그대로 붙인다. (slicing의 특징은 `end` 범위는 포함하지 않는 것이다.)
4. 새로운 변수를 이전 변수에 덮어씌운다.
5. 반복 ~
6. 마지막에는 맨 처음 값을 제외하고 나머지 값만 출력한다.

```python
arr = [i for i in range(0, 21)]

for _ in range(10):
    a, b = map(int, input().split())
    b += 1
    arr_ = arr[:a] + arr[a: b][::-1] + arr[b:]
    arr = arr_

print(' '.join(map(str, arr[1:])))
```

---

<a href='https://www.acmicpc.net/problem/10813'>백준 10813 - 공 바꾸기</a>

## ⚡️ 나의 풀이

입력으로 들어온 값을 `baskets`의 `index`를 바꿔주면 된다. 팁은 `lambda` 함수를 통해 입력으로 들어올 때 공통으로 원하는 값을 빼줄 수 있다. (<a href='https://ywtechit.tistory.com/215'>참고</a>)
 
```python
n, m = map(int, input().split())
baskets = [i for i in range(1, n+1)]

for _ in range(m):
    a, b = map(lambda x: int(x)-1, input().split())
    baskets[a], baskets[b] = baskets[b], baskets[a]

print(*baskets)
```