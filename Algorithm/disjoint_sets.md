## 서로소 집합(disjoint_sets)
수학에서 `서로소 집합`이란 공통 원소가 없는 두 집합을 의미한다.
예를 들면, 집합 `{1, 2}`와 `{3, 4}`는 서로소 관계이다. 
반면에, 집합 `{1, 2}`와 `{2, 3}`은 `2`라는 원소가 두 집합에 공통적으로 포함되어 있기 때문에 서로소 관계가 아니다.

서로소 집합 자료구조는 `union-find(합치기 - 찾기)` 자료구조라고도 불린다. 
또한, 자료구조를 구현할때는 트리 자료구조를 이용하여 집합을 표현하는데, 알고리즘은 다음과 같다.

>1. `union(합집합)` 연산을 확인하여, 서로 연결된 두 노드 A, B를 확인한다.
   * A와 B의 루트노드 A', B'를 각각 찾는다.
   * A'를 B'의 부모 노드로 설정한다(B'가 A'를 가리키도록 한다.)
>2. 모든 `union(합집합)` 연산을 처리할 때까지 1번 과정을 반복한다.

기존 시간복잡도는 `O(V)`였으나, 개선된 알고리즘을 사용하면 시간복잡도는 `O(V+M(1+logV))`정도로 줄어든다.

```python
'''
6 4
1 4
2 3
2 4
5 6
'''

def find_parent(parent, x):
    if parent[x] != x:
        return find_parent(parent, parent[x])
    else:
        return parent[x]

def union_parent(parent, a, b):
    a = find_parent(a)
    b = find_parent(b)

    if a < b:
        parent[b] = a
    else:
        parent[a] = b

v, e = map(int, input().split())
parent = [0] * (v+1)

for i in range(1, v+1):
    parent[i] = i

for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)

print('각 원소가 속한 집합 출력', end='')
for i in range(1, v+1):
    print(find_parents(parent, i), end=' ')

print()

for i in range(1, v+1):
    print(parent[i], end=' ')

👉🏽 각 원소가 속한 집합: 1 1 1 1 5 5 
부모원소의 집합: 1 1 2 1 5 5 
```
---

### 경로 압축기법 코드
```python
# 기존 코드는 else return 값이 x였음.
def find_parent(parent, x):
    if parent[x] != x:
        return find_parent(parent, parent[x])
    else:
        return parent[x]
```

---

### 서로소 집합을 이용한 사이클 판별
서로소 집합은 무방향 그래프 내에서의 사이클을 판별할 때 사용할수 있다는 특징이 있다.
참고로 방향 그래프에서의 사이클 여부는 `DFS`통해 판별할 수 있으며, 개인적으로 공부하도록 하자.

사이클 알고리즘은 다음과 같다.
>1. 각 간선을 확인하며 두 노드의 루트 노드를 확인한다
  * 루트 노드가 서로 다르다면 두 노드에 대하여 `union` 연산을 수행한다.
  * 루트 노드가 서로 같다면 사이클(cycle)이 발생한 것이다.
>2. 그래프에 포함되어 있는 모든 간선에 대하여 1번과정을 반복한다.

```python
'''
3 3
1 2
1 3
2 3
'''

def find_parent(parent, x):
    if parent[x] != x:
        return find_parent(parent, parent[x])
    else:
        return parent[x]

def union_parent(parent, a, b):
    a = find_parent(a)
    b = find_parent(b)

    if a < b:
        parent[b] = a
    else:
        parent[a] = b

v, e = map(int, input().split())
parent = [0] * (v+1)

for i in range(1, v+1):
    parent[i] = i

cycle = False

for i in range(e):
    a, b = map(int, input().split())
    if find_parent(parent, a) == find_parent(parent, b):
        cycle = True
        break
    else:
        union_parent(parent, a, b)

if cycle:
    print('cycle이 발생했습니다.!')
else:
    print('cycle이 발생하지 않았습니다.!')

👉🏽 cycle이 발생하지 않았습니다.!
```

---
