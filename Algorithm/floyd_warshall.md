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
