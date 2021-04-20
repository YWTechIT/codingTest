### 📌 백준 4963 - 섬의 개수
<a href='https://www.acmicpc.net/problem/4963'>문제 설명</a>

### 💡 나의 풀이
`BFS` 혹은 `DFS`만 잘 구현 할 수 있다면 어려운 문제는 아니다. 다만, 기존 문제에서는 상, 하, 좌, 우 패턴이 등장했다면 이번에는 대각선 패턴이 등장했다. 

이왕 등장했으니 다음 세가지 패턴을 알아보자.
>1. 상, 하, 좌, 우 패턴
```python
dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]
```

>2. 대각선 + 상, 하, 좌, 우 패턴
```python
dx = [-1, -1, -1, 0, 0, 1, 1, 1]
dy = [-1, 0, 1, -1, 1, -1, 0, 1]
```

>3. 대각선 패턴
```python
dx = [-1, -1, 1, 1]
dy = [-1, 1, -1, 1]
```

2번을 사용하면 쉽게 해결 할 수 있다. 그리고 `while`문 종료조건은 입력이 `0, 0`이어야 하는데, 이는 `if not w and not h`조건을 주면 쉽게 해결 할 수 있다.

```python
from collections import deque

def bfs(x, y):
    queue = deque()
    queue.append((x, y))
    visited[x][y] = True

    while queue:
        x, y = queue.popleft()

        for i in range(8):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < h and 0 <= ny < w:
                if graph[nx][ny] == 1 and not visited[nx][ny]:
                    visited[nx][ny] = True
                    queue.append((nx, ny))

dx = [-1, -1, -1, 0, 0, 1, 1, 1]
dy = [-1, 0, 1, -1, 1, -1, 0, 1]

while True:
    w, h = map(int, input().split())
    if not w and not h:
        break
    graph = [list(map(int, input().split())) for _ in range(h)]
    visited = [[False] * w for _ in range(h)]
    cnt = 0

    for i in range(h):
        for j in range(w):
            if graph[i][j] == 1 and not visited[i][j]:
                bfs(i, j)
                cnt += 1
    print(cnt)
```