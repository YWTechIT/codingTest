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

