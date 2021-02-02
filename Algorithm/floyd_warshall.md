### floyd_warshall_algorithm
>1. `dijkstra`: 한 지점에서 다른 특정 지점까지의 최단 경로를 구하는 경우
>2. `floyd_warshall`: 모든 지점에서 모든 지점까지의 최단 경로를 모두 구하는 경우

---

ex) 2번 노드의 점화식을 구할 때, `대각선 0`, `2행 2열의 값은 구하지 않아도 된다.`
즉, [1, 2, 3, 4]의 노드 중 2를 제외한 나머지 [1, 3, 4]노드 중 2개의 노드를 뽑는 경우
`[1, 3] [1, 4] [3, 1] [3, 4] [4, 1] [4, 3]`의 경우의 수만 구하면 된다.

나머지 노드의 경우의 수를 구할때도 동일하다.

```python
import itertools

data = [1, 3, 4]

for i in itertools.permutations(data, 2):
    print(list(i), end=' ')
👉🏽 [1, 3] [1, 4] [3, 1] [3, 4] [4, 1] [4, 3]
```

| 출발 / 도착 | 1 | 2 | 3 | 4 |
| :----: | :----: | :----: | :----: | :----: | 
| 1 | 0 | 0 | * | * |
| 2 | 0 | 0 | 0 | 0 |
| 3 | * | 0 | 0 | * |
| 4 | * | 0 | * | 0 |

---

매번 <span style='color:blue'>방문하지 않은 노드 중 최단 거리를 갖는 노드를 찾을 필요가 없다.</span>

노드의 개수가 `N`개일 때, 알고리즘상으로 `N`번의 단계를 수행하며, 단계마다 `O(N^2)`의 연산을 통해 `현재 거쳐가는` 모든경로를 고려한다. 따라서, 플로이드 워셜 알고리즘의 총 시간 복잡도는 `O(N^3)`이다.

점화식에 맞게 2차원 리스트를 갱신하기 때문에 `dynamic_programming`이라고도 부른다.

> D(ab) = min(D(ab), D(ak) + D(kb))

```python
'''
4
7
1 2 4
1 4 6
2 1 3
2 3 7
3 1 5
3 4 4
4 3 2
'''

INF = int(1e9)

# 노드, 간선 입력받기
n, m = int(input())

# 2차원 리스트를 만들고 graph의 모든 값은 무한으로 초기화
graph = [[INF] * (n+1) for _ i in range(n+1)]

# 자기 자신으로 가는 값은 0으로 초기화
for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0

# 간선에 대한 입력 정보 저장
for _ in range(m):
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식 입력
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 결과 출력
for a in range(1, n+1):
    for b in range(1, n+1):
        if graph[a][b] == INF:
            print('INFINITY', end= ' ')
        else:
            print(graph[a][b], end=' ')

👉🏽
0 4 8 6 
3 0 7 9 
5 9 0 4 
7 11 2 0
```

---

### [ 문제 1 ] 미래도시
방문 판매원 A는 현재 1번회사에 위치해 있으며, X번 회사에 방문해 물건을 판매하고자 한다.

>1. 나중에 입력받을 수는 따로 선언해주자.
>2. 1번노드에서 X를 거쳐 K로 가는 최단거리 계산법: 1번에서 X까지의 최단거리 + X부터 K까지의 최단거리
`distance = graph[1][k] + graph[k][x]`

```python
'''
5 7
1 2
1 3
1 4
2 4
3 4
3 5
4 5
4 5

4 2
1 3
2 4
3 4
'''

INF = int(1e9)

n, m = map(int, input().split())

graph = [[INF] * (n+1) for _ in range(n+1)]

for a in range(1, n+1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

for i in range(m):
    a, b = map(int, input().split())
    graph[a][b] = 1
    graph[b][a] = 1


x, k = map(int, input().split())

for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])


distance = graph[1][k] + graph[k][x]

if distance >= INF:
    print(-1)
else:
    print(distance)

👉🏽 3
👉🏽 -1
```
---

### [ 문제 2 ] 전보
어느 날 C라는 도시에서 위급 상황이 발생했다.
그래서 최대한 많은 도시로 메시지를 보내고자 한다. 메시지는 도시 C에서 출발하여 각 도시 사이에 설치된 통로를 거쳐, 최대한 많이 퍼져나갈것이다. 각 도시의 번호와 통로가 설치되어 있는 정보가 주어졌을 때, 도시 C에서 보낸 메세지를 받게 되는 도시의 개수는 총 몇 개 이며, 도시들이 모두 메시지를 받는 데까지 걸리는 시간은 얼마인지 계산하는 프로그램을 작성하시오.

>1. `입력조건`: 첫째 줄에 도시의 개수 N, 통로의 개수 M, 메세지를 보내고자 하는 도시 C가 주어진다.
>2. 둘째 줄부터 `M+1`번째 줄에 걸쳐서 통로에 대한 정보 `X`, `Y`, `Z`가 주어진다. 이는 특정 도시 `X`에서 다른 특정 도시 `Y`로 이어지는 통로가 있으며, 메시지가 전달되는 시간이 `Z`라는 의미다.
>3. `출력조건`: 첫째 줄에 도시 C에서 보낸 메시지를 받는 도시의 총 개수와 총 걸리는 시간을 공백으로 구분하여 출력한다.

`N`과 `M`의 범위가 `5,000`보다 크기때문에 `floyd_warshall` 알고리즘을 사용하긴 힘들고, `linear_path` 알고리즘 역시 `3,000`보다 크기때문에 
사용하기 힘들다.

따라서, 한 도시에서 다른 도시까지의 최단거리 문제로 치환할 수 있으므로 다익스트라 알고리즘을 이용하자.

그림을 그려보니까 메세지를 보내는데 드는 비용은 `max: 4`가 소요된다. 따라서, `distance[i]`에서 `max`값만 따로 추출하면 된다. 

그리고 출력 중 메세지를 받는 도시의 수는 `distance`가 나올때마다 `count += 1`을 넣어주면된다. 그러나, 자기자신은 제외해야하기 때문에 `count - 1`도 넣어주자.

```python
'''
3 2 1
1 2 4
1 3 2
'''

import heapq

INF = int(1e9)
n, m, start = map(int, input().split())
graph = [[] for _ in range(n+1)]
distance = [INF] * (n+1)

for i in range(m):
    x, y, z = map(int, input().split())
    graph[x].append((y,z))

def dijkstra(start):
    q = []
    heapq.heappush(q, (0, start))
    distance[start] = 0

    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue

        for i in graph[now]:
            cost = dist + i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

dijkstra(start)

max_distance = 0
count = 0

for i in distance:
    if i != INF:
        count = count + 1
        max_distance = max(max_distance, i)

print(count - 1, max_distance)
👉🏽 2 4
```