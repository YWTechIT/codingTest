### 📌 백준 2468 - 안전 영역
<a href='https://www.acmicpc.net/problem/2468'>문제 설명</a>

### 💡 나의 풀이
문제를 이해하는데는 어렵지 않았는데, 나름대로 구현하는데 어려웠다. 아직 구현 실력이 뛰어나지 않아서 그런것 같다.

N의 최대범위가 `100 * 100`이어서 시간 복잡도가 `O(N^3)`이어도 시간초과가 나지 않을것이라고 판단했는데, 같은 지역에서 내리는 비의 양에 따른 모든경우를 조사해야하기때문에 이중반복문에서 삼중반복문으로 늘어났다.

모든 높이를 조사할때는 입력값 중 가장 작은 값부터 가장 큰 값을 범위로 잡았다. 여기서 `pythonic`코드를 배웠는데 2차원의 배열에서 `min, max`값을 찾을 때 `map`함수를 사용하면 간단하게 출력 할 수 있다. 가장 큰 값의 범위를 설정할때는 +1을 해주자. 아니면 오답판정난다.

그리고 BFS함수에서 변수를 `x, y`좌표 외에도 `value`를 하나 더 줬는데, 구해야하는 높이가 반복문마다 바뀌므로 변수로 같이 전달해줬다.

또, 핵심 포인트는 BFS를 통해 반복문을 한번 돌고나올때마다 `visited`와 `cnt`를 초기화해줘야 한다. 이걸 안해줘서 시간이 오래 걸렸던것 같다. 
첫 입력 좌표를 방문했다고 선언했어야하는데 `graph`를 방문했다고 설정하니까 출력이 제대로 안 나왔다. 이건 파이참이 고장난거야!라고 생각했지만 내 머리가 고장났었다.

![](https://images.velog.io/images/abcd8637/post/18005c45-6319-4421-8f85-57a25e2bfe46/More_details_be_omitted.jpeg)

높이가 4 이하인 지점이 모두 잠겼을 때의 안전한 영역을 구할때의 순서는 다음과 같다.
1. BFS 함수 구현(생략)
2. 모든 좌표에 대해 검사한다.(조건: 구하려고 하는 높이가 `graph[i][j]` 이상이고 `visited`에 방문한적이 없을 때)
3. BFS 함수를 실행한 횟수 누적
4. 안전한 영역의 최대값 갱신

코드 제출할 때 `python3`, `pypy` 각각 제출 했는데, 메모리와 시간이 다르게 계산됐다.

![](https://images.velog.io/images/abcd8637/post/0a5f7c3d-5313-4ae4-9af2-5bae421720a5/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-18%2015.28.45.png)

```python
from collections import deque
import sys
input = sys.stdin.readline

def bfs(x, y, safe_area):    # BFS
    queue = deque()
    queue.append((x, y))
    visited[x][y] = 1

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < N and 0 <= ny < N:
                if graph[nx][ny] >= safe_area and visited[nx][ny] == 0:
                    visited[nx][ny] = 1
                    queue.append((nx, ny))


N = int(input())
graph = [list(map(int, input().split())) for _ in range(N)]
graph_min = min(map(min, graph))
graph_max = max(map(max, graph))
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

max_safe_area = graph_min
for safe_area in range(graph_min, graph_max+1):
    visited = [[0] * N for _ in range(N)]
    temp = 0
    for i in range(N):
        for j in range(N):
            if graph[i][j] >= safe_area and visited[i][j] == 0:
                bfs(i, j, safe_area)
                temp += 1
    if temp > max_safe_area:
        max_safe_area = temp
print(max_safe_area)
```

