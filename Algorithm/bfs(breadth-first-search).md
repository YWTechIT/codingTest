## BFS(Breadth-First-Search)
BFS 알고리즘은 `너비 우선탐색`이라는 의미를 가진다. 쉽게말해, 가까운 노드부터 탐색하는 알고리즘이다. 

>1. `DFS`: 최대한 멀리있는 노드를 우선으로 탐색하는 방식
>2. `BFS`: 최대한 가까이있는 노드를 우선으로 탐색하는 방식

BFS는 `선입선출`방식인 `큐(Queue)` 자료구조를 이용하는것이 정석이다. 

알고리즘의 동작방식은 다음과 같다.
>1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
>2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
>3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.

```python
from collections import deque

def bfs(graph, start, visited):
    queue = deque([start])
    visited[start] = True
    
    while queue:
        v = queue.popleft()
        print(v, end=' ')
        for i in graph[v]:
            if not visited[i]:
                queue.append(i)
                visited[i] = True

graph =[
    [],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

visited = [False] * 9
bfs(graph, 1, visited)
👉🏽  2 3 8 7 4 5 6  
```

### 📍 [ 예제 1 ] 미로탈출 & 백준 2178 미로탐색
>1. 함수를 선언하는 방식
>2. 함수를 선언하지 않는 방식

총 두가지 버전으로 문제를 풀어보았다.
나는 `함수를 선언하지 않고 푸는 방식`이 조금 더 잘 맞았다.
함수를 선언하지 않은 방식은 `deque`를 쓰지 않아도 풀 수 있는데,
요약하자면 다음과 같다.

>1. `matrix:` 입력값
>2. `visited:` 입력값과 비교할 데이터 ([0]으로 이루어진 `N x M` 리스트)
   * `visited[0][0]:` 처음 방문한 곳 = 1
>3. `dx`, `dy:` 상하좌우 데이터
>4. `queue:` 가장 첫 시작점

`while문` `queue`의 가장 첫번째 원소대입
이후 `for문`을 통해 상하좌우 계산을 해준다.
i가 0부터 시작하므로 dy = 1인 `상`을 먼저 본다.
범위 설정을 통해 입력받은 값을 벗어나지 않게한다.
입력받은 값 중 `0`은 벽이므로 건너뛴다.
`matrix[nx][ny] == 1`: 갈 수 있는 곳
`visited[nx][ny] == 0`: 방문하지 않은 곳을 동시에(and) 만족하면
`visited[nx][ny] = visited[x][y] + 1` (초기값은 1로 설정함)
`print(visited[n-1][m-1])`: 0, 0부터 시작하므로 `-1 범위` 까지 설정

```python
# 함수를 선언한 방식
from collections import deque

n, m = map(int, input().split())

matrix = []

for i in range(n):
    matrix.append(list(map(int, input())))

dx = [0, 0, -1, 1]
dy = [1, -1, 0, 0]

def bfs(x,y):
    queue = deque()
    queue.append((x,y))

    while queue:
        x, y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if nx < 0 or ny < 0 or nx >= n or ny >= m:
                continue
            if matrix[nx][ny] == 0:
                continue

            if matrix[nx][ny] == 1:
                matrix[nx][ny] = matrix[x][y] + 1
                queue.append((nx, ny))
    return matrix[n-1][m-1]

print(bfs(0, 0))


# 함수를 선언하지 않은 방식
n, m = map(int, input().split())
# 입력받은 배열넣기
matrix = []
for i in range(n):
    matrix.append(list(map(int, input())))

# 방문하지 않은 배열
visited = [[0] * m for _ in range(n)]

# 상하좌우선언
dx = [0, 0, -1, 1]
dy = [1, -1, 0, 0]

queue = []
queue.append((0,0))
visited[0][0] = 1

while queue:
    x, y = queue.pop(0)
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if nx < 0 or ny < 0 or nx >= n or ny >= m:
            continue
        if matrix[nx][ny] == 1 and visited[nx][ny] == 0:
            visited[nx][ny] = visited[x][y] + 1
            queue.append([nx, ny])

print(visited[n-1][m-1])
```