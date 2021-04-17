### 📌 백준 2331 - 반복수열
<a href='https://www.acmicpc.net/problem/2331'>문제 설명</a>

### 💡 나의 풀이
지금까지 2차원 그래프나 리스트를 이용한 문제만 풀었었는데, 1차원의 수 반복을 이용하는 계산은 새로운 접근이 필요했다.

그래서 어떤 탐색을 사용할까 고민하다 `BFS`를 사용했는데, 감이 잘 잡히지 않았다.
찾아보니까 `DFS`를 이용하고, 어떤 코드는 아예 `DFS`를 사용하지도 않았다.

또, DFS를 이용할 때 Flag 방식을 사용하려고 했는데, 오답판정을 받았다. 현재 값을 가지고 재귀함수로 들어가는게 아니라서 그런건지.. 이유를 도통 모르겠다.

제일 하단의 코드를 보고 왜 안되는지 아시는 고수님들 댓글 부탁드립니다. ㅠㅠ 😂 😂

>1. DFS
반복수열을 진행하며 현재 값을 기준으로 다음 원소를 탐색하고, 이전에 나왔던 원소(중복원소)가 나올 때까지 다음 값을 계속 탐색한다. 이때, 이전 원소를 방문했는지 확인하는 `visited`의 전체범위를 `250000`으로 정했는데, 원소가 최대로 나올 수 있는 값이 `236196`이기 때문이다. (A의 값이 9999까지이고, P의 최대 제곱이 5기 때문 `9**5+9**5+9**5+9**5 = 236196`)

마지막에 중복되는 원소가 나오면 `return`하여 호출됐던 지점까지 올라간다.
호출순서는 다음의 사진을 참고하자.

![](https://images.velog.io/images/abcd8637/post/e660ecf4-dfb6-48a7-93cc-800fc0ccda30/1.jpeg)

>2. while
중복되는 원소가 나오기전까지 계속해서 `result`에 추가하는 방법이다. 이때 중요한점은 처음값(57)을 추가한 상태에서 진행하자. 또, 반복문 마지막에 현재 값을 `D[n]`으로 변경해주는것도 잊지말자.

출력은 `index`를 사용해서 몇 번째 위치에 있는지 확인하면된다. `index`는 0부터 세기때문에 `-1`처리를 해줄 필요가 없다.

![](https://images.velog.io/images/abcd8637/post/ba3f5ab5-2688-4013-b1e3-d240de27c177/2.jpeg)


```python
# DFS
def number_square(number, square):    # square P each number
    return sum([int(i) ** square for i in str(number)])

def dfs(A, P, visited, count):    # DFS implementation
    if visited[A]:    # if occur repeated number
        return visited[A] - 1
    visited[A] = count
    temp = number_square(A, P)
    count += 1
    return dfs(temp, P, visited, count)

A, P = map(int, input().split())
visited = [0] * 250000    # maximum case(236196 is approximately 250000)
count = 1
print(dfs(A, P, visited, count))
```

```python
# use while
A, P = map(int, input().split())
result = [A]

while True:
    temp = sum([int(i) ** P for i in str(A)])    # square P each number
    if temp in result:    # if occur repeated number
        break
    result.append(temp)
    A = temp

print(result.index(temp))
```

```python
# incorrect code
def number_square(number, square):  # square P each number
    return sum([int(i) ** square for i in str(number)])

def dfs(A, P, visited):  # DFS implementation
    if visited[A]:  # occur repeated number
        return visited.index(visited[A])
    visited[A] = True
    temp = number_square(A, P)
    return dfs(temp, P, visited)

A, P = map(int, input().split())
visited = [False] * 250000  # maximum case
print(dfs(A, P, visited))

```