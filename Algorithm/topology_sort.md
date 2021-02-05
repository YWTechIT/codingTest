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

---

### ⚡️ [ 문제 1 ] 커리큘럼
N개의 강의 정보가 주어졌을 때, N개의 강의에 대해여 수강하기까지 걸리는 최소시간을 각각 출력하는 프로그램을 작성하시오.

문제를 잘 읽어보니 단방향그래프를 가지고 있는 특징 때문에 `서로소 집합`, `크루스칼` 알고리즘을 사용 할 수는 없고, N의 입력이 `500`이하인걸로 보았을 때, `위상 정렬(topology_sort)`을 사용하면 되는것을 깨달았다.

입,출력 값을 천천히 살펴봤는데 어떤의미로 작성된건지 깨닫는데만해도 30분이 걸렸다. 😂 😂

입력값은 다음과 같았는데 

```python
'''
5
10 -1
10 1 -1
4 1 -1
4 3 1 -1
3 3 -1
'''
```

맨 앞의 값은 `입력조건`에서 `강의 시간`이라고 주어져있으니까, `time` 변수로 따로 빼야겠구나 라는 생각을 했다.

그리고 제일 마지막 값이 `-1`로 동일하게 작성되있는걸 보니까 `-1`은 값은 제거해줘야겠구나라는 생각이 들었다.

하지만 `N+1` 다음부터 중간에 있는 값이 무엇인지 헷갈렸다.
`입력조건`: 각 강의의 강의 시간과 <span style='color:blue'>그 강의를 듣기 위해 먼저 들어야 하는 강의들의 번호가 자연수로 주어지며</span>
이때, 강의 시간은 100,000 이하의 자연수이다. 라고 적혀있었다.

고심끝에 직접 그림으로 그려보니까 이해가 됐다. N번째 강의를 듣기위해 먼저 들어야 하는 강의를 나타낸 수였다. 여기서 또 막히는 구간이 있었는데, 그럼 N+4번째 `4 3 1 -1`는 3번을 듣고 1번을 들어야하는 순서인가?라는 생각이 들었다. 문제를 다시보니 `또한, 동시에 여러개의 강의를 들을 수 있다고 가정한다`라는 말이 적혀있었다. 그림으로 나타내면 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/8e30a55c-c605-46c8-95f2-a9c0d172f0fa/KakaoTalk_Photo_2021-02-05-10-21-34.jpeg)

코드에 `graph[x].append(i)`가 있는데 이를 출력하면
`[[], [2, 3, 4], [], [4, 5], [], []]`인데,

해석하면 1번노드가 `2, 3, 4`번 노드로 갈 수 있고 3번노드가 `4, 5`번 노드로 갈 수 있다는 의미다.

이 외에도 중간에 `deepcopy()` 함수를 사용하여 `time` 값을 복사하는 코드가 있는데 이는 리스트의 경우 단순히 대입 연산을 하면 값이 변경 될때 문제가 발생할 수 있다는 말이 언급되어있다. 

`react` 만질때 `...state`를 써봤는데 `python`에도 `deepcopy()`를 쓰는걸 처음봤다. 자주 써먹어야겠다.

```python
from collections import deque
import copy
'''
5
10 -1
10 1 -1
4 1 -1
4 3 1 -1
3 3 -1
'''
v = int(input())
indegree = [0] * (v+1)
graph = [[] for _ in range(v+1)]
time = [0] * (v+1)

for i in range(1, v+1):
    array = list(map(int, input().split()))
    time[i] = array[0]
    for x in array[1:-1]:
        indegree[i] += 1
        graph[x].append(i)

q = deque()
result = copy.deepcopy(time)

for i in range(1, v+1):
    if indegree[i] == 0:
        q.append(i)

while q:
    now = q.popleft()

    for i in graph[now]:
        result[i] = max(result[i], result[now] + time[i])
        indegree[i] -= 1
        if indegree[i] == 0:
            q.append(i)

for i in range(1, v+1):
    print(result[i], end=' ')
👉🏽 10 20 14 18 17
```



