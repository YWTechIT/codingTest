### 📌 백준 10451 - 순열사이클
<a href='https://www.acmicpc.net/problem/10451'>문제 설명</a>

### 💡 나의 풀이

```python
# DFS
import sys
input = sys.stdin.readline

def dfs(graph, v, visited):
    visited[v] = True
    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

result = []
T = int(input())
for i in range(T):

    N = int(input())
    sequence = list(map(int, input().split()))
    graph = [[] for _ in range(N + 1)]
    visited = [False] * (N + 1)

    for i in range(1, N + 1):
        graph[i].append(i)
        graph[i].append(sequence[i - 1])

    cnt = 0
    for j in range(1, N + 1):
        if not visited[j]:
            dfs(graph, j, visited)
            cnt += 1
    print(cnt)
```