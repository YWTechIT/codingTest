### 📌 백준 1303 - 전쟁 - 전투
<a href='https://www.acmicpc.net/problem/1303'>문제 설명</a>

### 💡 나의 풀이
2차원 배열에서 각 색깔에 맞는 거리를 구하는 전형적인 `BFS`문제이지만, 헷갈린 부분들이 많았다.

한쪽 `BFS`만 구하는것이 아니고 양쪽 `BFS`를 모두 구현해야하다보니까 함수를 어떻게 선언하는지 굉장히 고민을 많이 했다.
결론적으로 `BFS` 함수에 `color`라는 파라미터를 작성해서 넘겨줬고 함수내에서 각 칸의 거리를 구하는 방법은 각 색깔별로 `w_cnt`, `b_cnt`를 따로따로 선언하지 않고 `cnt` 변수 하나만 선언해서 조건문으로 색깔이 다를때 해당 색을 기준으로 `cnt`를 세고 `return`하는 방법으로 진행했다. 이 방법까지 캐치하는데 상당히 오랜시간이 걸렸다. 어제 첫 알고리즘 문제로 선정했으나, 당시에는 풀지 못했고 이후 완벽하게 구현방법을 머릿속에 넣고 싶어 오늘 21시까지 미뤄뒀다가 다시 풀었다.

`BFS`의 구현방법을 알더라도 문제의 유형에 따라서 입력값을 다르게 줘야하는 경우가 생기는데 지금까지 내가 풀었던 유형은 다음과 같다.
1. 정석적인 BFS 구현: <a href='https://www.acmicpc.net/problem/1260'>boj_1260 - DFS와 BFS</a>
2. 각각의 기준점 별 거리계산: <a href='https://www.acmicpc.net/problem/2667'>boj_2667 - 단지번호붙이기</a>, <a href='https://www.acmicpc.net/problem/1303'>boj_1303 - 전쟁 - 전투</a>
3. 시작지점이 2곳 이상인 좌표를 동시에 BFS 구현: <a href='https://www.acmicpc.net/problem/7576'>boj_7576 - 토마토</a>
4. 한 기준점이 다른 기준점에 영향을 미치는 BFS: <a href='https://www.acmicpc.net/problem/4179'>boj_4179 - 불!</a>
5. 범위별 최대 BFS 구하기: <a href='https://www.acmicpc.net/problem/2468'>boj_2468 - 안전 영역</a>
6. 등등...

많이 풀지는 못했지만 어떤 문제는 풀었던 문제같고 반대로 어떤 비슷한 문제는 방법을 완전히 다르게 해야하는 경우도 많았다. 흐름을 아는것이 중요한것 같다. 그리고 `BFS` 관련된 문제가 엄청많았다. 척보면 이런 유형이구나를 알때까지 풀어야겠다는 생각이 들었다. 

풀이방법을 살펴보자.
1. 방문기록이 없고 현재값이 `W`인 값 혹은 방문기록이 없고 현재값이 `B`인 값을 함수로 넣어준다.
2. `color`별로 `cnt`를 증가시킨다.
3. `return cnt+1` 한 값에 제곱해주고 색깔별로 누적시킨다.

```python
import sys
from collections import deque
input = sys.stdin.readline

def bfs(x, y, color):
    cnt = 0
    queue = deque()
    queue.append((x, y))
    visited[x][y] = True

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < m and 0 <= ny < n:
                if graph[nx][ny] == color and not visited[nx][ny]:    # each color check
                    visited[nx][ny] = True
                    queue.append((nx, ny))
                    cnt += 1    # each color count

    return cnt + 1

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]
n, m = map(int, input().split())
graph = [list(input()) for _ in range(m)]
visited = [[False] * n for i in range(m)]

white, blue = 0, 0
for i in range(m):
    for j in range(n):
        if graph[i][j] == 'W' and not visited[i][j]:
            white += bfs(i, j, 'W') ** 2    # count accumulate
        elif graph[i][j] == 'B' and not visited[i][j] :
            blue += bfs(i, j, 'B') ** 2    # count accumulate

print(white, blue)
```