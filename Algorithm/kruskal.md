## kruskal_algorithm

크루스칼 알고리즘은 다양한 문제 상황에서 가능한 한 최소한의 비용으로 신장 트리를 찾아야 할 때가 있다.

예를 들어, `N`개의 도시에서 두 도시 사이에 도로를 놓아 전체 도시가 서로 연결될 수 있게 도로를 설치하는 경우에서, 2개의 도시 `A`, `B`를 선택했을 때, 도시 `A`에서 `B`로 이동하는 경로가 반드시 존재해야한다.

이때, 모든 도시를 연결할 때 최소한의 비용으로 연결하려면 어떤 알고리즘을 사용해야 할까? 와 같은 문제에서 `크루스칼`을 이용하면 효율적으로 답을 구할 수 있다.

알고리즘의 핵심 원리는 다음과 같다.
>1. 간선 데이터를 비용에 따라 오름차순으로 정렬한다.
>2. 간선을 하나씩 확인하며 현재의 간선이 사이클을 발생시키는지 확인한다.
 * 사이클이 발생하지 않는 경우 최소 신장 트리에 포함시킨다.
 * 사이클이 발생하는 경우 최소 신장 트리에 포함시키지 않는다.
>3. 모든 간선에 대하여 2번의 과정을 반복한다.

시간복잡도는 다음과 같다.
> 간선의 개수가 `E`개 일때, `O(ElogE)`
>   * 간선을 정렬하는 작업의 시간복잡도가 `O(ElogE)`이기 때문이다.
>   * 서로소 집합 알고리즘 시간 복잡도 < 정렬 시간복잡도

---

```python
'''
7 9
1 2 29
1 5 75
2 3 35
2 6 34
3 4 7
4 6 23
4 7 13
5 6 53
6 7 25
'''

def find_parent(parent, x):
    if parent[x] != x:
        return find_parent(parent, parent[x])
    else:
        return parent[x]

def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

v, e = map(int, input().split())
parent = [0] * (v+1)
edges = []
result = 0

for i in range(1, v+1):
    parent[i] = i

for i in range(e):
    a, b, cost = map(int, input().split())
    edges.append((cost, a, b))

edges.sort()

for edge in edges:
    cost, a, b = edge
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result = result + cost
print(result)
👉🏽 159
```