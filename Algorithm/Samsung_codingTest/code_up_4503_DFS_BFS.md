### 📌 코드업 4503 - 바이러스(BFS)
<a href='https://codeup.kr/problem.php?id=4503'>문제 설명</a>

### 💡 나의 풀이
<a href='https://ywtechit.tistory.com/56'>어제 풀었던 문제</a>를 BFS로 풀어봤다.

DFS는 한 노드에서 인접노드가 더 없을때까지 끝까지 파고 들어가는데, BFS는 한 노드에서 인접노드가 없으면 주변 인접노드를 찾는다.
BFS는 `Queue`를 이용해서 풀면 되는데, 어제처럼 `flag`, `check`형식으로 풀어보자.

BFS방식의 전체적인 흐름은 다음과 같다.(Queue는 선입선출임을 기억하자.)
>1. 시작하는 값을 Queue에 넣고 방문처리를 한다.
>2. Queue안에 현재 들어있는 값(노드)을 뺀다.
>3. 해당 노드의 인접한 노드 중에서 아직 방문하지 않은 노드를 모두 큐에 넣는다.
>4. 2~3번의 과정을 더 이상 할 수 없을 때까지 반복한다.

이런 흐름을 따라서 문제를 풀어보자.
`Flag`, `Check`방식을 이용하는데 방법은 다음과 같다.

1. `Flag`
`C`와 동일한 범위 전체를 `False`로 선언해놓고, 현재 `Queue`에 들어가있는 값을 꺼냈을 때 해당 노드를 방문한적이 없다면(해당 값이 `False`이면) `True`로 만든다.
`while`문이므로 방문처리한 값은 `pop`시키고 `Queue`에 남아있는 값을 차례대로 확인한다.(Queue가 없어질 때까지)


2. `Check`
빈 리스트를 선언하고 현재 `Queue`에 들어가있는 값을 꺼냈을 때 해당 노드를 방문한 적이 없다면(빈 리스트에 해당 값이 없으면) 빈 리스트에 현재 값을 추가한다. 빈 리스트에 `append`한 값은 방문했다는 의미가 된다.
`while`문이므로 방문처리한 값은 `pop`시키고 `Queue`에 남아있는 값을 차례대로 확인한다.(Queue가 없어질 때까지)

이후에 bfs순으로 나온 값을 `len`으로 돌려 출력하면 문제에서 요구하는 1번 컴퓨터를 통해 웜 바이러스에 걸리게 되는 컴퓨터의 수를 출력하게 된다. 이때 자신의 값은 제외해야하므로 `len-1`처리를 해주자.


```python
# 1. Flag 방식
from collections import deque

def bfs(graph, start):  # bfs 구현
    queue = deque([start])
    visited[start] = True

    while queue:
        v = queue.popleft()
        result.append(v)  # 시작 값 추가
        for i in graph[v]:
            if not visited[i]:
                queue.append(i) # 방문하지 않은 노드 추가
                visited[i] = True

C = int(input())
NC = int(input())
graph = [[] for _ in range(C+1)]
result = []
visited = [False] * (C+1)

for i in range(NC):  # 입력값 노드 변환
    node1, node2 = map(int, input().split())
    graph[node1].append(node2)
    graph[node2].append(node1)

bfs(graph, 1)
print(len(result)-1)

# 2. 단순 확인(check) 방식
from collections import deque

def bfs(graph, start):  # bfs 구현
    queue = deque([start])
    visited.append(start)  # 시작 값 추가

    while queue:
        v = queue.popleft()
        for i in graph[v]:
            if i not in visited:
                visited.append(i) 
                queue.append(i)  # 방문하지 않은 노드 추가

C = int(input())
NC = int(input())
graph = [[] for _ in range(C+1)]
visited = []

for i in range(NC):
    node1, node2 = map(int, input().split())
    graph[node1].append(node2)
    graph[node2].append(node1)

bfs(graph, 1)
print(len(visited)-1)
```

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


