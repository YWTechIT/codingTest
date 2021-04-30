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
### 📍 1468 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-1
지그재그로는 어떻게 채워야할까?를 고민하다가 i가 홀수이거나 짝수일때로 나눠서 작성했다. 하지만, 그것보다 `flag`를 사용하면 더 편하게 채울 수 있었다.
`flag`는 전구를 `on/off` 스위치로 끄고 켤 수 있듯이 `flag`를 사용해서 방향이 바뀌면 `False`로 설정하고 반대일 경우에는 `True`로 설정해 원하는 방향으로 유도 할 수 있다.

평소에 `flag`를 잘 사용하지 않아서 몰랐는데 괜찮은 방법인것같다. 전체적인 흐름이 두 가지로 나눠졌을 때 사용해봐야겠다. 현재 코드에서는 `flag = True`일때는 순방향으로 `flag = False`일때는 역방향으로 설정했다.

나머지 문제들은 앞에서 풀었던 문제들과 동일했다.

```python
# flag 사용
n = int(input())
arr = [[0] * n for _ in range(n)]
flag = True

cnt = 0
for i in range(n):
    if flag:
        for j in range(n):
            cnt += 1
            arr[i][j] = cnt
        flag = False
    else:
        for j in range(n-1, -1, -1):
            cnt += 1
            arr[i][j] = cnt
        flag = True

for i in arr:
    for j in i:
        print(j, end=' ')
    print()

# 홀 짝 판별
n = int(input())
arr = [[0] * n for _ in range(n)]

cnt = 0
for i in range(n):
    if i % 2:
        for j in range(n-1, -1, -1):
            cnt += 1
            arr[i][j] = cnt
    else:
        for j in range(n):
            cnt += 1
            arr[i][j] = cnt

for i in arr:
    print(*i, ' ')

```

---
### 📍 1469 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-2

```python
n = int(input())
arr = [[0] * n for _ in range(n)]
flag = False

cnt = 0
for i in range(n):
    if not flag:
        for j in range(n-1, -1, -1):
            cnt += 1
            arr[i][j] = cnt
        flag = True
    else:
        for j in range(n):
            cnt += 1
            arr[i][j] = cnt
        flag = False

for i in arr:
    print(*i, ' ')

```

---
### 📍 1470 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-3

```python
n = int(input())
arr = [[0] * n for _ in range(n)]

flag = True
cnt = 0
for i in range(n):
    if flag:
        for j in range(n):
            cnt += 1
            arr[j][i] = cnt
        flag = False
    else:
        for j in range(n-1, -1, -1):
            cnt += 1
            arr[j][i] = cnt
        flag = True

for i in arr:
    print(*i, ' ')
```

---
### 📍 1471 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-4

```python
n = int(input())
arr = [[0] * n for _ in range(n)]

flag = True
cnt = 0
for i in range(n):
    if flag:
        for j in range(n-1, -1, -1):
            cnt += 1
            arr[j][i] = cnt
            flag = False
    else:
        for j in range(n):
            cnt += 1
            arr[j][i] = cnt
            flag = True

for i in arr:
    print(*i, ' ')

```

---
### 📍 1472 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-5
행렬의 크기가 `n*m`일때도 마찬가지로 가로로 값이 채워면 `n`을 먼저 반복문에 작성하고 `arr[i][j]`를 넣으면 된다. 반대의 경우는 `m`을 먼저 반복문에 작성하고 `arr[j][i]`을 넣어주면 된다.

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]
flag = True
cnt = 0

for i in range(n - 1, -1, -1):
    if flag:
        for j in range(m-1, -1, -1):
            cnt += 1
            arr[i][j] = cnt
        flag = False
    else:
        for j in range(m):
            cnt += 1
            arr[i][j] = cnt
        flag = True

for i in arr:
    print(*i, ' ')
```

---
### 📍 1473 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-6

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]
cnt = 0
flag = True

for i in range(n-1, -1, -1):
    if flag:
        for j in range(m):
            cnt += 1
            arr[i][j] = cnt
        flag = False
    else:
        for j in range(m-1, -1, -1):
            cnt += 1
            arr[i][j] = cnt
        flag = True

for i in arr:
    print(*i, ' ')
```

---
### 📍 1474 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-7

```python
n, m = map(int, input().split())

arr = [[0] * m for _ in range(n)]
flag = True

cnt = 0
for i in range(m - 1, -1, -1):
    if flag:
        for j in range(n - 1, -1, -1):
            cnt += 1
            arr[j][i] = cnt
        flag = False
    else:
        for j in range(n):
            cnt += 1
            arr[j][i] = cnt
        flag = True

for i in arr:
    print(*i, ' ')
```

---
### 📍 1475 : [ 기초 - 배열연습 ] 2차원 배열 지그재그 채우기 2-8

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]
cnt = 0
flag = True

for i in range(m-1, -1, -1):
    if flag:
        for j in range(n):
            cnt += 1
            arr[j][i] = cnt
        flag = False
    else:
        for j in range(n-1, -1, -1):
            cnt += 1
            arr[j][i] = cnt
        flag = True

for i in arr:
    print(*i, ' ')
```

---
### 📍 1476 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-1
빗금을 채우는경우는 2중 반복문이 아닌 3중 반복문으로 처리해야하는데, 처음에 규칙을 찾으려해도 도통 찾아지질 않았다.
그래서 관련영상(<a href='https://www.youtube.com/watch?v=m0TujkCIF9M&t=214s'>유튜브 - 황진경 코딩영재컴퓨터학원</a>)에서 푸는방법을 배웠다.

문제에 나와있는 `arr[i][j]`값의 좌표를 찍어보면 다음 사진과 같다. 
![](https://images.velog.io/images/abcd8637/post/e0ca45d4-ff28-4847-bdbb-fabc3c86eef3/KakaoTalk_Photo_2021-04-30-09-25-53.jpeg)

이전에 풀었던 <a href='https://ywtechit.tistory.com/88'>2차원배열 순서대로 채우기</a>는 2중 반복문을 이용해 i, j값이 증가 할때 순서대로 값을 출력했으나, 이번문제는 조건을 만들어야한다. `i+j = sum`인 조건이 같을 때만 좌표를 입력하기때문에 `i, j`가 나올 수 있는 모든 경우의 수에 조건을 대입해야한다. 따라서, 3중 반복문을 사용해 `K(sum)`값과 일치하는지 여부를 파악해야한다. 이때 `K`값은 빗금이 6번만에 끝나기때문에 범위를 `for k in range(m+n)`까지 선언해준다.

그리고 값은 `세로`부터 채워지기때문에 반복문에는 `세로(m)`를 먼저 선언하고 나중에 `가로(n)`를 넣어준다.

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m):
    for i in range(m):
        for j in range(n):
            if i + j == k:
                cnt += 1
                arr[j][i] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1477 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-2
1476문제와 동일하지만 값이 채워지는 순서가 반대인 문제다. 값은 가로부터 채워지기때문에 반복문에는 `가로(n)`를 먼저 선언하고 나중에 `세로(m)`를 넣어준다.
```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m):
    for i in range(n):
        for j in range(m):
            if i+j == k:
                cnt += 1
                arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1478 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-3
이번에는 우측상단부터 채워지는 문제이다. 순서대로 배열을 채웠던 문제는 단순하게 `n` 혹은 `m`의 범위를 뒤에서부터 잡으면 되지만, 삼중 반복문의 경우에는 k의 값도 신경써줘야 한다.
그래서 1476번처럼 `i, j`의 좌표를 적어놓고 더했더니 또 규칙을 찾을 수 없었다. 이럴 때 `n` 혹은 `m`을 이용하자. `i-j+m`의 조건일때를 생각하면 규칙이 찾을 수 있다.

![](https://images.velog.io/images/abcd8637/post/0fb29109-aa39-4019-8aed-8da0b0b1ce97/KakaoTalk_Photo_2021-04-30-09-36-33.jpeg)

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m):
    for i in range(n):
        for j in range(m-1, -1, -1):
            if i-j+m == k:
                cnt += 1
                arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1479 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-4

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m):
    for i in range(n-1, -1, -1):
        for j in range(m):
            if i - j + m == k:
                cnt += 1
                arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1480 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-5
이번에는 1이 우측 하단에 있는 문제다. 이때는 `k`의 범위를 거꾸로 선언해주면 된다.

```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m-1, -1, -1):
    for i in range(n):
        for j in range(m):
            if i+j == k:
                cnt += 1
                arr[i][j] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1481 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-6
```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m-1, -1, -1):
    for i in range(m):
        for j in range(n):
            if i+j == k:
                cnt += 1
                arr[j][i] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1482 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-7
```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m):
    for i in range(m-1, -1, -1):
        for j in range(n):
            if i-j+n == k:
                cnt += 1
                arr[j][i] = cnt

for i in arr:
    print(*i, ' ')
```

---
### 📍 1483 : [ 기초 - 배열연습 ] 2차원 배열 빗금 채우기 3-8
```python
n, m = map(int, input().split())
arr = [[0] * m for _ in range(n)]

cnt = 0
for k in range(n+m):
    for i in range(m):
        for j in range(n):
            if i-j+n == k:
                cnt += 1
                arr[j][i] = cnt

for i in arr:
    print(*i, ' ')
```

## ⚡️ 결론
