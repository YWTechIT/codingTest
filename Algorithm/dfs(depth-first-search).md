## DFS(Depth-First-Search)
깊이 우선탐색이라고 부르며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘
`DFS`는 `stack` 자료구조에 기초한다는 점에서 구현이 간단하다. 
탐색을 수행함에 있어서 데이터의 개수가 `N`개인 경우 `O(N)`의 시간이 소요된다.

실제로 스택을 쓰지 않고, 재귀 함수를 이용했을 때 매우 간결하게 구현할 수 있다.

>1. 인접행렬(Adjacency Matrix): 2차원 배열로 그래프의 연결관계를 표현하는 방식
>2. 인접리스트(Adjacency List): 리스트로 그래프의 연결 관계를 표현하는 방식
```python
# 인접 행렬 

# 무한 비용선언
INF = 999999999

graph = [
    [0, 7, 5],
    [7, 0, INF],
    [5, INF, 0]
]

print(graph)
👉🏽 [[0, 7, 5], [7, 0, 999999999], [5, 999999999, 0]]

# 인접 리스트

# 행(Row)이 3개인 2차원 리스트로 인접 리스트 표현
graph = [[] for _ in range(3)]

# 노드 0에 연결된 노드 정보 저장(노드, 거리)
graph[0].append((1, 7))
graph[0].append((2, 5))

# 노드 1에 연결된 노드 정보 저장(노드, 거리)
graph[1].append((0, 7))

# 노드 2에 연결된 노드 정보 저장(노드, 거리)
graph[2].append((0, 5))

print(graph)
👉🏽 [[(1, 7), (2, 5)], [(0, 7)], [(0, 5)]]
```

```python
dfs(graph, v, visited):
    visited[v] = True
    print(v, end=' ')
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

graph = [
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

visited[v] = [False] * 9

dfs(graph, 1, visited)
👉🏽 1 2 7 6 8 3 4 5 
```

---
### 📍 상, 하, 좌, 우 좌표 확인
```python
x, y = 0, 0
dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

for i in range(4):
    nx = x + dx[i]
    ny = y + dy[i]

👉🏽 1 0
0 1
-1 0
0 -1
```

---
### 📍 대각선 + 상, 하, 좌, 우 좌표 확인
```python
x, y = 0, 0
dx = [-1, -1, -1, 0, 0, 1, 1, 1]
dy = [-1, 0, 1, -1, 1, -1, 0, 1]

for i in range(8):
    nx = x + dx[i]
    ny = y + dy[i]

👉🏽 -1 -1
-1 0
-1 1
0 -1
0 1
1 -1
1 0
1 1
```

---