### 📌 백준 7576 - 토마토
<a href='https://www.acmicpc.net/problem/7576'>문제 설명</a>

### 💡 나의 풀이
나의 수준에서는 어려웠다... 익은토마토가 1개일 경우에는 잘 구할 수 있었는데, 2개 이상인경우는 도저히 생각이 나지 않았다.

그래서 다른사람의 코드를 조금 참고했는데 `BFS`를 동시에 2개를 돌리는 방법은 아예 생각도 못했고 그러다보니까 함수의 코드도 이전에 풀던 방법과는 조금 달라서 고민하며 문제를 푸느라 반나절을 쏟아버렸다.

처음에 익은 토마토가 2개 이상 있을 때 케이스를 하나씩 더해서 두 개를 더해주면 될 줄 알았다. 컴퓨팅적으로 생각하지 않고 내키는대로 생각해버려서 안되는 방법으로 구현하려니까 머리가 터지는 줄 알았다.

![](https://images.velog.io/images/abcd8637/post/499d9c9b-4628-4b92-b9d1-1356d90bf004/48084048_1979360242133382_4370583502370897920_n.jpeg)

그리고 문제 마지막 모든 토마토가 익어있는 상태를 0으로 출력해야하는데, 이 경우는 제외하고 코드를 작성해도 됐었다. 그래서 경우의 수는 다음과 같이 2가지만 고려했다.

1. 토마토를 모두 익히지 못했을 경우(bfs를 돌리고 나온 값에 0이 포함되어 있는 경우)
2. 모든 토마토가 익은경우 or 토마토가 모두 익을 때까지의 최소 날짜

풀이방법은 다음과 같다.
1. queue를 함수 밖에 선언한다.
2. 모든 좌표를 검색하여 익은토마토(1)의 좌표만 `queue`에다 집어 넣는다.
3. `BFS` 함수를 구현한다. (이전과 동일: 상, 하, 좌, 우 선언 -> 현재 들르지 않은 좌표들르기 -> 이전 좌표에 +1씩 누적시키기)
4. `BFS` 실행
5. 실행하고 나온 2차원 배열 중 `0`이 포함되어 있으면 `-1` 출력 아니면 2차원 배열의 최댓값에서 -1 해주기(-1을 하는 이유는 BFS가 날짜는 `1(하루)`부터 시작되어야하는데 `2(이틀)`부터 시작했기 때문이다.)

익은 토마토가 2개이상 들어있는 `예제입력 3`을 `BFS`로 구현하면 다음과 같은 결과가 나온다.

![](https://images.velog.io/images/abcd8637/post/a8faf821-d163-44f2-acfb-4c303e62ddd6/KakaoTalk_Photo_2021-04-20-14-56-40.jpeg)

좌표값이 1을 동시에 `BFS` 돌리는것이므로 처음 `queue`에는 `(0, 0), (3, 5)`가 들어가있고 이후 하나씩 `popleft()`하면서 다음 좌표가 `0(익지 않은 토마토)`이면 이전 값에 `+1`이 누적된다.

코드를 간결하게 작성하려고 자꾸 헷갈리는 문장이 있는데, `if graph[i][j] == 1:`와 `if graph[i][j]:`는 다른코드이고, `if not graph[i][j]:`와 `if graph[i][j] == 0:`는 같은코드이다. 까먹지 말자.

```python
import sys
from collections import deque
input = sys.stdin.readline

def bfs():
    while queue:
        x, y = queue.popleft()
        print(x, y)
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < n and 0 <= ny < m:
                if not graph[nx][ny]:
                    graph[nx][ny] = graph[x][y] + 1
                    queue.append((nx, ny))
    return graph

queue = deque()
m, n = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(n)]
dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

for i in range(n):
    for j in range(m):
        if graph[i][j] == 1:
            queue.append((i, j))    # extract ripen tomatoes(value = 1)

result = bfs()    # execute bfs ripen tomatoes at the same time
print(result)
if True in map(lambda x: 0 in x, result):    # not all ripen tomatoes
    print(-1)
else:    # all ripen tomatoes or minimum days of ripen tomatoes
    print(max(map(max, result))-1)
```