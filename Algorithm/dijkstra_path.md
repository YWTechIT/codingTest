## dijkstra_path
다익스트라를 구현하는 방법 
>1. 구현하기 쉽지만 느리게 동작하는 코드 `(O(V^2))`
>2. 구현하기 조금 까다롭지만 빠르게 동작하는 코드 `O(ElogV)`


### dijkstra_path(linear_search)
>1. 각 노드에 대한 최단 거리를 담는 1차원 리스트 선언
>2. 방문하지 않은 노드 중 최단 거리가 가장 짧은 노드를 선택하기 위해 매 단계마다 1차원 리스트의 모든 원소를 순차 탐색

```python
'''
6 11
1
1 2 2
1 3 5
1 4 1
2 3 3
2 4 2
3 2 3
3 6 5
4 3 3
4 5 1
5 3 1
5 6 2
'''

import sys

n, m = int, input().split()
input = sys.stdin.readline
start = int(input())
INF = int(1e9)
graph = [[] for _ in range(n+1)]
visited = [False] * (n+1)
distance = INF * (n+1)

for i in range(m):
    a, b, c = map(int, input().split())
    graph[a].append((b,c))
    
def get_small_node():
    min_value = INF
    index = 0
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index

def dijkstra(start):
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
        
    for i in range(n-1):
        now = get_small_node()
        visited[now] = True
        for j in graph[now]:
            cost = distance[now] + j[1]
            if cost < distance[j[0]]:
                distance[j[0]] = cost
                
dijkstra(start)

for i in range(1, n+1):
    if distance[i] == INF:
        print('INFINITY')
    else:
        print(distance[i])
👉🏽 0 2 3 1 2 4
```
