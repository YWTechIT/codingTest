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