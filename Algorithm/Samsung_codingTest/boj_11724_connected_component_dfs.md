### 📌 백준 11724 - 연결 요소의 개수
<a href='https://www.acmicpc.net/problem/11724'>문제 설명</a>

### 💡 나의 풀이
이번 문제는 <a href='https://ywtechit.tistory.com/67'>bfs</a>와 dfs 모두 이용해서 풀었는데 시간차이가 많이 나지 않았다.(근소하게 `dfs`가 `48m/s`정도 빨랐다.)
방향 그래프가 없을 때는 간단하게 입력값을 반대로 바꿔서 넣어주면 된다.

`예제 입력1`을 그림으로 표현하면 다음과 같다.
이후에 몇번노드끼리 이어졌는지를 `graph`에 입력하면 되는데 무 방향 그래프기때문에 순서가 바뀌어도 된다.

문제를 쉽게 그림으로 표현했다. `graph`의 `index`가 노드이다.

DFS로 풀 때는 최대 재귀 값을 더 열어줘야 풀린다.

![](https://images.velog.io/images/abcd8637/post/1fcf2359-88ee-4bb3-85e8-46fe46ae0092/KakaoTalk_Photo_2021-04-19-14-20-29.jpeg)

```python
import sys
sys.setrecursionlimit(1000000)
input = sys.stdin.readline

def dfs(graph, v, visited):    # dfs implementation
    visited[v] = True

    for i in graph[v]:
        if not visited[i]:
            dfs(graph, i, visited)

N, M = map(int, input().split())
graph = [[] for _ in range(N + 1)]
visited = [False] * (N + 1)

for i in range(M):
    node1, node2 = map(int, input().split())
    graph[node1].append(node2)
    graph[node2].append(node1)

cnt = 0
for i in range(1, N+1):    # check each node
    if not visited[i]:
        dfs(graph, i, visited)
        cnt += 1
print(cnt)
```

