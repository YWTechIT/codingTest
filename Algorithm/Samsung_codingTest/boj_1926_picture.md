### 📌 백준 1926 - 그림
<a href='https://www.acmicpc.net/problem/1926'>문제 설명</a>

### 💡 나의 풀이
`BFS`를 이용해서 풀었는데, `queue`에 있는 원소를 `pop`할 때 마다 `cnt+=1`해주는것을 `while`문에 쓰지 않고 엉뚱한 곳에 썼다가 답이 안나와서 헤맸다.
또 중요한것은 함수가 실행될때마다 `each_cnt`를 1로 초기화 해주자. 아니면 값이 계속 누적된다.

그리고 최대값을 갱신해줄 때 굳이 파라미터로 넣지 않아도 `return each_cnt`을 해주고 나오는 값과 0부터 `max`로 비교해주면 나중에 제일 큰 값만 빼낼 수 있다.
가장 간단한 비교방법이니 외워두자.

1. 외부에서 모든 좌표를 하나씩 넣을 때 `BFS`를 사용하는 조건이 충족되면 `cnt+=1` 해준다.
2. `BFS` 함수 내부에서 원소를 `pop`할때 `each_cnt+=1`을 해준다.
3. `return each_cnt`와 최초 0으로 정의한 `max_each_count` 중 큰 값으로 갱신하면서 반복문이 끝나면 가장 높은 값을 출력한다.

```python
import sys
from collections import deque
input = sys.stdin.readline

def bfs(x, y):
    each_cnt = 1    # init each_cnt
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
                    each_cnt += 1    # update each_cnt
    return each_cnt    # end each_cnt

n, m = map(int, input().split())
visited = [[False] * m for _ in range(n)]
graph = [list(map(int, input().split())) for _ in range(n)]

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

cnt, max_each_count = 0, 0
for i in range(n):
    for j in range(m):
        if graph[i][j] == 1 and not visited[i][j]:
            cnt += 1    # dfs work condition
            max_each_count = max(max_each_count, bfs(i, j))    # update max_each_count

print(cnt)
print(max_each_count)
```