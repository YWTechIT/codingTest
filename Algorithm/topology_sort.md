## topology_sort(위상정렬)
위상 정렬은 순서가 정해져 있는 일련의 작업을 차례대로 수행해야 할 때 사용할 수 있는 알고리즘이다. 즉, 방향 그래프의 모든 노드를 `방향성에 거스르지 않도록 순서대로 나열하는 것`이다.

위상정렬의 알고리즘은 다음과 같다.
>1. 진입차수가 0인 노드를 큐에 넣는다.
>2. 큐가 빌 때까지 다음의 과정을 반복한다.
  * 큐에서 원소를 꺼내 해당 노드에서 출발하는 간선을 그래프에서 제거한다.
  * 새롭게 진입차수가 0이 된 노드를 큐에 넣는다.

이때, 모든 원소를 방문하기 전에 큐가 빈다면 사이클이 존재한다고 판단할 수 있다. 다시말해, 큐에서 원소가 `V`번 추출되기 전에 큐가 비어버리면 사이클이 발생한 것이다.

위상 정렬의 시간복잡도는 `O(V + E)`이다. 
차례대로 모든 노드를 확인하면서, 해당 노드에서 출발하는 간선을 차례대로 제거해야한다. 결과적으로 노드와 간선을 모두 확인하는 측면에서 `O(V + E)`의 시간이 소요되는 것이다.

```python
'''
7 8
1 2
1 5
2 3
2 6
3 4
4 7
5 6
6 4
'''

from collections import deque

v, e = map(int, input().split())
graph = [[] for _ in range(v+1)]
indegree = [0] * (v+1)

for i in range(e):
    a, b = map(int, input().split())
    graph[a].append(b)
    indegree[b] = indegree[b] + 1

def topology_sort():
    q = deque()
    result = []

    for i in range(1, v+1):
        if indegree[i] == 0:
            q.append(i)

    while q:
        now = q.popleft()
        result.append(now)

        for i in graph[now]:
            indegree[i] = indegree[i] - 1
            if indegree[i] == 0:
                q.append(i)
    for i in result:
        print(i, end=' ')

topology_sort()

👉🏽 1 2 5 3 6 4 7 
```