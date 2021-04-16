### 📌 백준 1260 - DFS와 BFS
<a href='https://www.acmicpc.net/problem/1260'>문제 설명</a>

### 💡 나의 풀이
`BFS`와 `DFS`를 둘 다 사용해야하는 문제인데 풀이방법은 다음과 같다.

문제에서 `정점 번호가 작은 것을 먼저 방문한다.`를 통해 입력값을 `인접리스트(adjacent list)`으로 넣을 때 `sort`를 붙여 작은 값부터 들어가게끔 설정했다.

`dfs`의 구현순서는 다음과 같다.
1. 처음 들어온 값 `index`의 `flag`를 `True`로 바꾼다.
2. 만약, 인접 노드를 방문하지 않았다면(`flag = False`), 해당 인접노드로 들어가서 방문하지 않은 인접노드가 없을 때까지 들어간다.(`recursive`)
3. 재귀문을 탈출하면서 해당값을 하나씩 출력한다.

`bfs`의 구현순서는 다음과 같다.
1. 처음 들어온 값을 `queue`에 넣는다.
2. 처음 들어온 값 `index`의 `flag`를 `True`로 바꾼다.
3. 먼저 들어온 값을 `queue`에서 먼저 꺼내면서 방문하지 않은 인접노드가 있는지 살펴보고, 있으면 해당 노드를 `queue`에 넣는다.
4. `queue`에 남은 값이 없을 때까지 반복한다.
5. `queue`에서 꺼낸 값을 하나씩 출력한다.

여담이지만, <a href ='https://ywtechit.tistory.com/57'>어제 풀었던 문제</a>와 같은 방식으로 풀었는데 결과는 다음과 같았다.
1. `sys.stdin.readline`을 사용하니까 시간이 2배가량 줄어들었다.
2. `flag(True)`방식이 `append`방식보다 <span style='color:blue'>실행시간을 약 4배가량 단축시켰다.</span>
왜냐하면, `if i not in visited`는 반복문안에 있는 원소들을 하나씩 검사해야하지만, `if not visited[i]`는 단순하게 `True`, `False`여부만 따지면 되기 때문이다.
즉, 노드 갯수 `n`이 커지게되면 그만큼 연산횟수가 늘어난다는 문제점이 있다.

![](https://images.velog.io/images/abcd8637/post/0e90af74-72e6-4165-b3b5-76ddac56dc0c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-16%2007.30.14.png)

```python
import sys
from collections import deque
input = sys.stdin.readline

def dfs(graph, v):  # implementation dfs function
    dfs_visited[v] = True
    print(v, end=' ')
    for i in graph[v]:
        if not dfs_visited[i]:
            dfs(graph, i)

def bfs(graph, start):   # implementation bfs function
    queue = deque([start])
    bfs_visited[start] = True
    while queue:
        v = queue.popleft()
        print(v, end=' ')
        for i in graph[v]:
            if not bfs_visited[i]:
                queue.append(i)
                bfs_visited[i] = True

N, M, V = map(int, input().split())
graph = [[] for _ in range(N+1)]
dfs_visited, bfs_visited = [False] * (N+1), [False] * (N+1) # flag init

for i in range(M):
    node1, node2 = map(int, input().split())
    graph[node1].append(node2)
    graph[node2].append(node1)

graph = [sorted(i) for i in graph] # sort by ascending order

dfs(graph, V)
print()
bfs(graph, V)
```