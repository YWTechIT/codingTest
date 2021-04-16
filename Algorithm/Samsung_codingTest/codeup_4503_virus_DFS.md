
### 📌 코드업 4503 - 바이러스(DFS)
<a href='https://codeup.kr/problem.php?id=4503'>문제 설명</a>

### 💡 나의 풀이
이 문제의 다양한 풀이가 있겠지만, 우선 DFS로 풀어봤다. 내일은 BFS로 풀어 볼 예정이다.

비 선형자료구조인 그래프에서의 가장 중요한 부분은 선형자료구조와 다르게 입력을 받을때 양방향으로 받아야 한다는 점이다.
이번 문제에서 입력값을 어떻게 받아야하는지 조금 헷갈렸는데, 양방향으로 받으면 정상적으로 정답판정을 받을 수 있다.

네트워크에 연결되어있는 컴퓨터만 바이러스에 걸린다고 했으므로 DFS를 통해 나온값들의 `len`을 구하면 된다.

또, DFS를 푸는 방법에는 2가지가 있는데 다음과 같다.
>1. 이코테에서 배운방법: `Flag: if not visited[i]`
`visited`를 모두 `[False]`로 초기화해두고 현재 방문하려는값이 `False`이면, 해당 값을 방문했다는 표시인 `True`로 변경하고 방문하지 않은 인접노드를 방문한다.

>2. 단순 확인방법: `check: if i not in visited`
`visited`안에 현재 값과 똑같은 값이 없으면 방문처리한다. 단순 확인방법은 제일 첫번째 값도 포함되므로 문제에서는 기준이 되는값을 제외하고 출력해야하므로 `len(result)-1`을 해줘야한다.

```python
# 1. Flag 방법
def dfs(graph, v, visited):
    visited[v] = True
    for i in graph[v]:
        if not visited[i]:
            result.append(i)
            dfs(graph, i, visited)

computer = int(input())
network = int(input())
graph = [[] for _ in range(computer+1)]
result = []
visited = [False] * (computer+1)

for i in range(network): # 그래프는 양방향이니까 거꾸로도 추가시켜야한다.
    node, node2 = map(int, input().split())
    graph[node].append(node2)
    graph[node2].append(node)

dfs(graph, 1, visited)
print(len(result))

# 2. 단순 확인(check) 방법
def dfs(graph, v, visited):
    for i in graph[v]:
        if i not in visited:
            visited.append(i)
            dfs(graph, i, visited)

computer = int(input())
network = int(input())
graph = [[] for _ in range(computer+1)]
visited = []

for i in range(network): # 그래프는 양방향이니까 거꾸로도 추가시켜야한다.
    node, node2 = map(int, input().split())
    graph[node].append(node2)
    graph[node2].append(node)

dfs(graph, 1, visited)
print(len(visited)-1)
```