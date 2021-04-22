## 📌 백준 4179 - 불!

[문제 설명](https://www.acmicpc.net/problem/4179)

---

## 💡 나의 풀이

나에겐 끔찍한 문제였다.. 이 문제에 오전, 오후를 완전히 쏟아버렸다. 😇 😇 수 없이 코드를 제출했다. 하지만, 돌아오는 대답은 `인덱스 에러` 혹은 `틀렸습니다.`

채점 중간에 71%에서 자꾸 오답 판정을 받았다.

![](https://images.velog.io/images/abcd8637/post/7cfa3b77-1f1d-4fe3-9b90-7094f241d0ea/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-04-22%2018.53.08.png)

틀린 이유를 단계별로 작성하면

1.  인덱스 에러(Index Error): 변수 정의 단계에서 행과 열을 반대로 입력했다.
2.  잘못된 변수 입력: 네이밍을 비슷하게 해서 그런지 중간에 다른 변수를 작성해서 제출했다.
3.  잘못된 코드: 여기서 시간이 제일많이 걸렸는데 마지막 단계인 `f_visited > j_visited` 조건을 잘못 추가했다. 처음에는 `f_visited[nx][ny] > j_visited[nx][ny]`로 생각했는데 아니었다. 왜 그런가 하면 우리가 `fire BFS단계`에서 선언했던 `f_visited[nx][ny] = f_visited[x][y] + 1`를 떠올려보자.

문제를 풀면서 도저히 감이 잡히지 않는다면 핵심 파트를 살펴보자.

1.  불(fire)과 지훈이의 `queue`를 2개 선언하고 방문 기록도 마찬가지로 2개 선언한다.(f\_queue, j\_queue / f\_visited, j\_visited)
2.  지훈이와 불은 매 분마다 상, 하, 좌, 우로 퍼진다.
3.  지훈이가 불에 갇히지 않고 안전하게 탈출하려면 불이 퍼진 시간보다 지훈이가 이동한 시간이 더 빨라야 한다.
4.  다시 말해, 한 좌표의 값을 기준으로 불보다 지훈이의 값이 더 크다면 그쪽으로 움직일 수 없다.
5.  지훈이는 미로의 가장자리에 접한 곳에서 탈출한다고 나와있는데, 이는 `(nx, ny)` 좌표가 미로의 범위를 벗어날 때 탈출이 가능하다.
6.  `BFS` 내부에서 `queue`는 거리순으로 누적된다는 점을 기억하자.
7.  지훈이가 미로를 빠져나오지 못한 경우는 `while`문이 종료될 때까지도 출력이 없는 경우니까 그때는 `IMPOSSIBLE`을 출력하자.

![](https://images.velog.io/images/abcd8637/post/739c32de-7015-4b9f-b538-a3c1b6af7050/KakaoTalk_Photo_2021-04-22-19-10-52.jpeg)

또, 다른 사람의 풀이를 찾아보니까 다들 범위에 들어오지 않는 경우로만 구해서 적잖이 당황했었다.  
나는 대체로 `BFS` 문제는 범위에 들어오는 경우로만 계산했기 때문에 아닌 경우를 찾는 코드는 손에 익지 않았다.

내가 수십 번의 코드를 다시 제출했던 이유는 `28번` 코드인데 단순하게 `nx, ny` 좌표에서 불이 방문한 경로와 지훈이가 방문했던 경로만 비교하면 될 줄 알았더니 그게 아니었다.

피나는 구글링 끝에 얻은 반례 테스트 케이스를 가져왔다. 왜 대소만 비교하면 안 되는지 같이 살펴보자.

```
'''
3 4
###F
.J#.
###.
'''
```

현재 테스트 케이스에서 `f_visited`와 `j_visited`의 결과는 다음과 같다.

1.  f\_visited = \[\[0, 0, 0, 1\], \[0, 0, 0, 2\], \[0, 0, 0, 3\]\]
2.  j\_visited = \[\[0, 0, 0, 0\], \[0, 1, 0, 0\], \[0, 0, 0, 0\]\]

이상하다. 분명 불이 번지지 않았고 벽도 아닌데 왜 `j_visited[1][0]` 자리는 2로 바뀌지 않은 거지?!

  
그 이유는 불이 방문하지 않은경우(`not f_visited[nx][ny] or`)에는 정상적으로 `BFS`처리를 해줘야 하기 때문이다. 저 코드를 빼면 단순히 불이 방문한 경로와 지훈이가 방문한 경로의 좌표만 비교해서 더 큰 값만 출력하기 때문에 불이 방문하지 않은 경로는 `BFS` 처리하지 않는다.

골드 문제에 익숙하지 않아서 그런지 모르겠지만 `반례의 케이스`의 중요성을 이 문제를 통해서 잘 알게 됐다. 백준 질문검색에서 3개의 [테스트 케이스를](https://www.acmicpc.net/board/view/31494) 더 가져왔다. 혹시나 풀리지 않는다면 다음을 시도해보자.

```
'''
5 5
....F
...J#
....#
....#
...#.

출력: 4

---

3 3
F.F
.J.
F.F

출력: IMPOSSIBLE

---

5 5
#####
#...#
#.J.#
#...#
#####

출력: IMPOSSIBLE
'''
```

하단의 코드는 2개를 가져왔는데 범위를 안쪽으로 설정한 코드, 범위를 벗어나게 설정한 코드를 가져왔다. 둘 중 이해가 잘되는 코드로 사용하자. 나는 첫 번째 코드가 이해가 더 잘됐다.

아직 [실버 1밖에](https://www.acmicpc.net/user/abcd8637) 되지 않았지만 골드 문제 첫 신고식을 잘(?) 치른 것 같다.  
이제 다른 골드 문제를 풀면서 역경에 또 부딪혀보자!

```
# in range case

import sys
from collections import deque
input = sys.stdin.readline

def bfs():
    while f_queue:    # fire BFS
        x, y = f_queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < R and 0 <= ny < C:
                if not f_visited[nx][ny] and graph[nx][ny] != '#':
                    f_visited[nx][ny] = f_visited[x][y] + 1
                    f_queue.append((nx, ny))

    while j_queue:    # jihoon BFS
        x, y = j_queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 <= nx < R and 0 <= ny < C:
                if not j_visited[nx][ny] and graph[nx][ny] != '#':
                    if not f_visited[nx][ny] or f_visited[nx][ny] > j_visited[x][y] + 1:    # important code
                        j_visited[nx][ny] = j_visited[x][y] + 1
                        j_queue.append((nx, ny))
            else:
                return j_visited[x][y] + 1    # escape map

    return 'IMPOSSIBLE'    # not escape map

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

R, C = map(int, input().split())
graph = [list(input().strip()) for _ in range(R)]
f_queue, j_queue = deque(), deque()    # declare fire, jihoon queue
f_visited, j_visited = [[0] * C for _ in range(R)], [[0] * C for _ in range(R)]    # declare fire, jihoon visited

for i in range(R):
    for j in range(C):
        if graph[i][j] == 'F':
            f_queue.append((i, j))
        elif graph[i][j] == 'J':
            j_queue.append((i, j))
print(bfs())
```

```
# out range case(continue)

import sys
from collections import deque
input = sys.stdin.readline

def bfs():
    while f_queue:    # fire BFS
        x, y = f_queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if nx < 0 or ny < 0 or nx >= R or ny >= C:
                continue

            if f_visited[nx][ny] != 0 or graph[nx][ny] == '#':
                continue

            f_visited[nx][ny] = f_visited[x][y] + 1
            f_queue.append((nx, ny))

    while j_queue:    # jihoon BFS
        x, y = j_queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if nx < 0 or ny < 0 or nx >= R or ny >= C:
                return j_visited[x][y] + 1    # escape map

            if j_visited[nx][ny] != 0 or graph[nx][ny] == '#' or (f_visited[nx][ny] != 0 and f_visited[nx][ny] <= j_visited[x][y]+1):    # important code
                continue

            j_visited[nx][ny] = j_visited[x][y] + 1
            j_queue.append((nx, ny))

    return 'IMPOSSIBLE'    # not escape map

dx = [1, 0, -1, 0]
dy = [0, 1, 0, -1]

R, C = map(int, input().split())
graph = [list(input().strip()) for _ in range(R)]
f_queue, j_queue = deque(), deque()    # declare fire, jihoon queue
f_visited, j_visited = [[0] * C for _ in range(R)], [[0] * C for _ in range(R)]    # declare fire, jihoon visited

for i in range(R):
    for j in range(C):
        if graph[i][j] == 'F':
            f_queue.append((i, j))
        elif graph[i][j] == 'J':
            j_queue.append((i, j))
print(bfs())
```