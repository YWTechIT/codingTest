### 📌 백준 1743 - 음식물 피하기
<a href='https://www.acmicpc.net/problem/1743'>문제 설명</a>

### 💡 나의 풀이
전형적인 `BFS` 혹은 `DFS` 문제이고, 입력에 음식물의 좌표를 입력받아 `BFS`, `DFS`를 돌려 단순 개수를 파악하고 기존 개수와 현재 개수를 비교하여 더 큰 값으로 갱신해주면 되는 방향으로 문제를 풀면 된다.

여기서 약간 까다로운 부분은 좌표를 직접 입력받는 부분일텐데, 우리가 사용하는 `graph`는 `0`부터 시작하므로 입력을 받을 때 `-1`처리를 해주면 오류없이 그래프에 입력할 수 있다.

풀이 흐름을 직접 그려봤다.

![](https://images.velog.io/images/abcd8637/post/da71f064-b807-4b81-a199-f036cbbb4b33/KakaoTalk_Photo_2021-04-22-06-48-35.jpeg)

```python
import sys
from collections import deque
input = sys.stdin.readline

def bfs(x, y):
    cnt = 0
    queue = deque()
    queue.append((x, y))
    visited[x][y] = True

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < n and 0 <= ny < m:
                if graph[nx][ny] == 1 and not visited[nx][ny]:
                    visited[nx][ny] = True
                    queue.append((nx, ny))
                    cnt += 1    # count food
    return cnt + 1

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

n, m, k = map(int, input().split())
graph = [[0] * m for _ in range(n)]
visited = [[False] * m for _ in range(n)]
for i in range(k):
    r, c = map(int, input().split())
    graph[r-1][c-1] = 1

max_food = 0
for i in range(n):
    for j in range(m):
        if graph[i][j] == 1 and not visited[i][j]:
            max_food = max(max_food, bfs(i, j))    # update max count food
print(max_food)
```