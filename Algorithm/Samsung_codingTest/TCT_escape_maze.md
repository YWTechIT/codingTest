### 📌 이것이 코딩테스트다 - 미로 탈출
<a href='https://www.youtube.com/watch?v=7C9RgOcvkvo&t=2497s'>영상 링크(51:30)</a>

### 💡 나의 풀이
`BFS`를 이용하는 흐름을 알아야 풀 수 있었는데, 그 흐름을 잘 몰라서 못 풀었다.
이전까지는 `그래프`를 이용해서 풀었는데, 이중 리스트를 이용하니까 머리가 잘 안돌아갔다.

이 문제를 풀어보니까 값이 어떻게 변하는지 흐름을 잡는것이 중요하다고 느꼈다.

```python
from collections import deque

n, m = map(int, input().split())
graph = [list(map(int, input())) for _ in range(n)]

# 상하좌우 선언
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

def bfs(x, y):
    queue = deque()
    queue.append((x, y))

    while queue:
        x, y = queue.popleft()

        # 상하좌우로 이동
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            # 새로운 그래프의 좌표가 전체 범위를 벗어나는 경우
            if nx < 0 or ny < 0 or nx >= n or ny >= m:
                continue

            # 새로운 그래프의 좌표가 괴물이 있는 부분으로 가는 경우
            if graph[nx][ny] == 0:
                continue

            # 새로운 그래프의 좌표가 괴물이 없는 부분으로 가는 경우, 이전 값에 +1을 해줘서 최단 경로를 계산한다.
            if graph[nx][ny] == 1:
                graph[nx][ny] = graph[x][y] + 1
                queue.append((nx, ny))

    # index는 0부터 세므로 출구(N, M)의 좌표는?
    return graph[n-1][m-1]

print(bfs(0, 0))
```

