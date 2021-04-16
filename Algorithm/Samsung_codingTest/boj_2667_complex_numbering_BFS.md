### 📌 백준 2667 - 단지번호붙이기
<a href='https://www.acmicpc.net/problem/2667'>문제 설명</a>

### 💡 나의 풀이
아침부터 저녁까지 이 문제만 잡고 늘어졌는데 드디어 풀었다. 😇 😇
특히, <span style='color:blue'>처음에 방문한 좌표를 1로 선언한 이유와, 새로운 좌표를 1로 선언한 이유를 잘 몰라서 엄청 헤맸다.</span>

`BFS, DFS` 파트에 약한 나에게 많은 도움을 준 문제다.
이 문제도 `BFS`와 `DFS`로 풀 수 있는데 지금은 `BFS`버전이고 내일은 `DFS`로 풀어봐야겠다.

또, `append`와 `flag`방식 두개로 나눠서 풀었는데 `flag` 실행시간이 `append` 보다 `4ms`정도 더 빨랐다.( 4ms면 별 의미 없는 시간차이긴 하지만, `True, False`가 근소하게 더 빠르다는것을 참고적으로 알아두자!)

![](https://images.velog.io/images/abcd8637/post/2a80933a-b3cc-4a1b-b491-b86a8e9d2bc5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-16%2019.07.09.png)

개별 단지수를 구하는 코드는 고민을 많이 했는데, 결론적으로 `{}`를 이용해서 풀었다.

이 문제에서 구현해야하는 기능은 총 2가지로 나뉘는데 다음과 같다.
>1. 총 단지수(bfs함수를 실행하는 조건이 충족된 횟수, 3번)
>2. 개별 단지수(bfs함수를 실행하는 횟수, 7, 8, 9)

풀이방법은 다음과 같다.
1. `N * N`의 좌표를 모두 확인해야하므로 이중반복문을 사용한다.
2. 그렇다고, 모든 좌표를 함수에 대입하는것이 아닌 조건에 맞는 좌표를 확인하자.(현재 값이 1이고, 아직 방문하지않은 노드 일때)
3. 필터링된 값을 `bfs`함수로 집어넣는다.
4. `deque()`안에 초기 `x, y`좌표를 집어 넣는다.(이때, 괄호를 하나 더 추가해서 튜플형태로 넣자.)
5. 초기좌표는 방문했으므로 1로 바꾼다.
6. `queue`의 값이 없어질때까지 `popleft()`를 하는데 현재 좌표 기준으로 상, 하, 좌, 우의 좌표를 확인하고 1이 발견되면 해당 좌표를 큐에 집어넣는다.
7. 새로운 좌표를 방문했으므로 1로 선언하자.

![](https://images.velog.io/images/abcd8637/post/52b5556e-cbb3-40f1-bbc8-77bd9a294cf0/1.jpeg)

![](https://images.velog.io/images/abcd8637/post/e65d4f77-4d90-4731-9822-d6fd8c8f0922/2.jpeg)

```python
# number 확인

from collections import deque

def bfs(x, y, cnt):
    queue = deque()
    queue.append((x, y))
    visited[x][y] = 1

    while queue:
        x, y = queue.popleft()

        for i in range(4):  # Search Up, Down, Left, Right
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < N and 0 <= ny < N:  # private out of bound
                if graph[nx][ny] == 1 and visited[nx][ny] == 0:  # check current value is house and not visited house
                    queue.append((nx, ny))
                    visited[nx][ny] = 1
                    cnt_dict[cnt] += 1

dx = [-1, 1, 0, 0]  # init Up and Down
dy = [0, 0, -1, 1]  # init Left and Right

N = int(input())  # map_size
graph = [list(map(int, input())) for _ in range(N)]  # input init
visited = [[0] * N for _ in range(N)]  # visited init
cnt = 0  # count all complex number
cnt_dict = {}  # count each complex number

for i in range(N):
    for j in range(N):
        if graph[i][j] == 1 and visited[i][j] == 0:
            cnt+=1
            cnt_dict[cnt] = 1
            bfs(i, j, cnt)
print(cnt)
print(visited)
print('\n'.join(map(str, sorted(cnt_dict.values()))))
```

```python
# True, False 방법

from collections import deque

def bfs(x, y, cnt):
    queue = deque()
    queue.append((x, y))
    visited[x][y] = True

    while queue:
        x, y = queue.popleft()

        for i in range(4):  # Search Up, Down, Left, Right
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < N and 0 <= ny < N:  # private out of bound
                if graph[nx][ny] == 1 and visited[nx][ny] == False:  # check current value is house and not visited house
                    queue.append((nx, ny))
                    visited[nx][ny] = True
                    cnt_dict[cnt] += 1

dx = [-1, 1, 0, 0]  # init Up and Down
dy = [0, 0, -1, 1]  # init Left and Right

N = int(input())  # map_size
graph = [list(map(int, input())) for _ in range(N)]  # input init
visited = [[False] * N for _ in range(N)]  # visited init
cnt = 0  # count all complex number
cnt_dict = {}  # count each complex number

for i in range(N):
    for j in range(N):
        if graph[i][j] == 1 and visited[i][j] == False:
            cnt+=1
            cnt_dict[cnt] = 1
            bfs(i, j, cnt)
print(cnt)
print('\n'.join(map(str, sorted(cnt_dict.values()))))
```

