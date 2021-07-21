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
## 📍 백준 10813 - 공 바꾸기

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

---
## 📍 백준 10709 - 기상캐스터

<a href='https://www.acmicpc.net/problem/10709'>백준 10709 - 기상캐스터</a>

## ⚡️ 나의 풀이
시뮬레이션 문제였는데, 구름이 움직일때의 로직을 어떻게 짜는냐가 중요한 문제였다. 내가 작성한 코드는 다른 코드에 비해 길이도 많았고, 실행시간도 `100m/s`정도 차이가 났다. 다시보니까 반복문을 많이 사용해서 그런것 같다.

나의 풀이방법은 다음과 같다.
1. 입력에 구름이 있는지 없는지를 판단하여 `boolean`값을 리턴한다.
2. 구름이 한개라도 존재하는 경우 현재 `sky`좌표가 `c`이고 다음 칸을 방문하지 않았다면 `cnt`를 하나씩 증가시킨다. (종료조건: `cnt`가 `W`보다 커질 때)

다른사람의 풀이순서는 입력의 각 `row`를 기준으로 풀었는데, 생각해보면 문제에서 `열`끼리는 고려하지 않고 `행`을 기준으로만 풀기때문에 여기서 코드를 간단하게 사용 할 수 있는것 같다.

1. 각 `row`를 기준으로 `cnt`와 `cloud`를 초기화 시킨다.
2. 현재 좌표가 `.`인데 `not cloud`면 `-1`을 넣는다. (이전까지 구름이 없으므로)
3. 현재 좌표가 `c`면 `0`을 넣는다. (구름이 현재 떠있는 상태이므로)
4. 현재 좌표가 `.`인데 `cloud`면 이전까지 누적한 `cnt`를 넣는다. (구름이 `cnt`분 뒤에 오기 때문에)

주의 할 점은 다음 사진처럼 이전에 다른 구름이 있더라도 현재 좌표기준으로 제일 가까운 구름만 신경써야한다. 왜냐하면 제일 처음으로 하늘에 구름이 도착하는 시간을 구해야 하기 때문이다.(문제 참고) 따라서 두번째 코드 `15`번 라인에서 `cnt`를 다시 `1`로 초기화 시켜야한다. (이 부분에서 조금 막혔다.)

![](https://images.velog.io/images/abcd8637/post/0142228f-f667-49cd-85af-4fcf0b1e8029/KakaoTalk_Photo_2021-07-21-11-34-56.jpeg)

```python
# 나의 코드
H, W = map(int, input().split())
sky = [input() for _ in range(H)]
result_sky = [[-1] * W for _ in range(H)]
visited = [[False] * W for _ in range(H)]
cnt = 1

def check_cloud():    # 구름이 있는지 없는지 판단하는 함수
    for i in sky:
        if 'c' in i:
            return True
    return False

def print_arr(arr):    # arr을 출력하는 함수
    for i in arr:
        print(*i, end=' ')
        print()

def visited_cloud():    # 구름의 초기값을 visited하는 함수
    for i in range(H):
        for j in range(W):
            if sky[i][j] == 'c':
                visited[i][j] = True
                result_sky[i][j] = 0

if not check_cloud():    # 구름이 하나도 없는 경우
    print_arr(result_sky)    

else:    # 구름이 하나라도 있는 경우
    visited_cloud()

    while cnt < W:    # 구름이 움직이는 최대 횟수는 W
        temp_arr = [[-1] * W for _ in range(H)]

        for i in range(H):
            for j in range(W-1):
                if sky[i][j] == 'c' and not visited[i][j+1]:
                    temp_arr[i][j+1] = 'c'
                    result_sky[i][j+1] = cnt

        sky = temp_arr
        cnt += 1
    print_arr(result_sky)
```

```python
# 다른 사람의 코드
H, W = map(int, input().split())
sky = [input() for _ in range(H)]
answer = [[0] * W for _ in range(H)]

for i in range(H):
    cnt = 1
    cloud = False
    for j in range(W):
        if not cloud and sky[i][j] == '.':
            answer[i][j] = -1
        elif sky[i][j] == 'c':
            cloud = True
            answer[i][j] = 0
            cnt = 1
        elif cloud and sky[i][j] == '.':
            answer[i][j] = cnt
            cnt += 1

for i in answer:
    print(*i, end=' ')
    print()

```
