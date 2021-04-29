## 📍 코드업 1460 ~ 1467 2차원 배열 순서대로 채우기 1-1 ~ 1-8

<a href='https://codeup.kr/problemset.php?search=2%EC%B0%A8%EC%9B%90+%EB%B0%B0%EC%97%B4'>코드업 [ 기초 - 배열연습] </a>

## ⚡️ 서론
2차원 배열의 기초적인 개념을 다졌던 문제이다.
저번주 `DFS, BFS` 관련 문제 풀 때 2차원 배열을 많이 사용했는데, 그때마다 `가로 x 세로` 혹은 `세로 x 가로`로 입력이 주어지면 올바른 방식으로 접근하는지 긴가민가했었는데, 이번기회에 개념을 다시 잡을 수 있어 좋았다.

코드업에 `2차원 배열`이라고 검색했을 때 나오는 문제들은 전부 풀어봐야겠다.

---
## ⚡️ 본론

### 📍 1460 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-1
`n*n`크기의 2차원배열을 채우는 문제다. 

```python
n = int(input())

cnt = 1
for i in range(n):
    for j in range(n):
        print(cnt, end=' ')
        cnt += 1
    print()
```

---
### 📍 1461 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-2
`n*n`크기의 2차원 배열을 채우는 건 동일하지만, 범위를 거꾸로 선언하는 방법을 알아야 한다. `range(n)-1, -1, -1`을 작성하면 거꾸로 채울 수 있다.

또, `DFS, BFS`문제를 풀다보니까 자연스럽게 `arr`을 먼저 2차원 배열 0으로 선언해놓고 `fill`을 해당 칸에 넣어주는 방법을 사용했다.

```python
n = int(input())
arr = [[0] * n for _ in range(n)]

fill = 1
for i in range(len(arr)):
    for j in range(len(arr[i]) - 1, -1, -1):
        arr[i][j] = fill
        fill += 1
        
for i in arr:
    print(*i, ' ')
```

---
### 📍 1462 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-3
이번엔 가로가 아닌 세로부터 채우는 문제다. 이때는 `arr[j][i]`로 선언해주면 세로부터 채울 수 있다. 풀다보니까 범위 설정을 `len(arr)`로 했는데, 이렇게 하는것보다 입력값 n으로 작성하는것이 더 가독성이 뛰어난것같다.

또, 이 문제는 `zip`을 사용해서 풀 수도 있는데 다음과 같은 행렬을 만들고 나서 `zip`함수로 묶어줘도 값이 동일하게 나온다.
```
1 2 3
4 5 6
7 8 9
```

```python
# 공통 코드
n = int(input())
arr = [[0] * n for _ in range(n)]

# 반복문 사용
cnt = 0
for i in range(n):
    for j in range(n):
        cnt +=1
        arr[j][i] = cnt

for i in arr:
    print(*i, ' ')

# zip함수 사용
cnt = 0
for i in range(n):
    for j in range(n):
        cnt +=1
        arr[i][j] = cnt

arr = list(map(list, zip(*arr)))

for i in arr:
    print(*i, ' ')
```

---
### 📍 1463 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-4
이 문제부터는 `n*m` 즉, 직사각형 모양의 2차원 배열을 채우는 문제다. 나는 `세로 x 가로`형태로 바꿔서 사용하는데 입력은 `가로 x 세로`형태로 주어졌다. 2차원 행렬을 선언할 때 헷갈리지 말자.

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for i in range(n-1, -1, -1):
    for j in range(m-1, -1, -1):
        cnt += 1
        arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1464 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-5

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for i in range(n-1, -1, -1):
    for j in range(m-1, -1, -1):
        cnt += 1
        arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1465 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-6

```python
n, m = map(int, input().split())

arr = [[0] * m for _ in range(n)]

cnt = 0
for i in range(n - 1, -1, -1):
    for j in range(m):
        cnt += 1
        arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1466 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-7
문제를 풀다보니까 2차원 배열을 채울 때 공통점이 있었는데, 

다음 행렬과 같이 가로부터 채워지는 행렬은 이중반복문을 가로(n)부터 선언하고 `arr[i][j]`를 작성하면 된다.
```
1 2 3
4 5 6
```

반대로 다음 행렬과 같이 세로부터 채워지는 행렬은 이중반복문을 세로(m)부터 선언하고 `arr[j][i]`를 작성하면 된다.
```
1 3 5
2 4 6
```

```python
n, m = map(int, input().split())

arr = [[0] * m for _ in range(n)]

cnt = 0
for i in range(m - 1, -1, -1):
    for j in range(n - 1, -1, -1):
        cnt += 1
        arr[j][i] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1467 : [ 기초 - 배열연습 ] 2차원 배열 순서대로 채우기 1-8
세로부터 값이 채워지니까 `m`을 먼저 반복문에 작성하고 `arr[j][i]`를 구하면 된다. 순서가 뒤에부터 쌓이면 범위를 뒤에서부터 설정해주면 된다.

```python
n, m = map(int, input().split())

arr = [[0] * m for _ in range(n)]

cnt = 0
for i in range(m-1, -1, -1):
    for j in range(n):
        cnt += 1
        arr[j][i] = cnt

for i in arr:
    for j in i:
        print(j, end=' ')
    print()

```

---
## ⚡️ 결론
기초적인 2차원배열 채우는법을 알았고, 다음에는 지그재그로 채우는 방법을 공부해보자.