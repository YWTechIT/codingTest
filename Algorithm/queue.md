## Queue
`선입선출(First In First Out)` 구조라고 한다.
먼저 들어온 수가 제일 먼저 나간다.

터널을 지나가는 모습에 비유할 수 있다.
파이썬으로 `queue`를 구현할때는 `collection`에서 제공하는 `deque` 자료구조를 활용하자. `deque`는 스택과 큐의 장점을 모두 채택한 것인데, 데이터를 넣고 빼는 속도가 리스트 자료형에 비해 효율적이며 queue 라이브러리를 이용하는 것보다 더 간단하다.
`deque` 객체를 리스트 자료형으로 변경할때는 마지막에 `list()`를 붙여주자.

```python
from collections import deque

queue = deque()

queue.append(5)
queue.append(2)
queue.append(3)
queue.append(7)
queue.popleft()
queue.append(1)
queue.append(4)
queue.popleft()

print(queue)
👉🏽 deque([3, 7, 1, 4])
print(list(queue))
👉🏽 [3, 7, 1, 4]

queue.reverse()
print(queue)
👉🏽 deque([4, 1, 7, 3])
print(list(queue))
👉🏽 [4, 1, 7, 3]
```

---
## 📌 백준 2164 - card2
<a href='https://www.acmicpc.net/problem/2164'>문제 설명</a>

## 💡 나의 풀이
단순하게 문제에 나와있는대로 구현하면 되는데, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮기는 과정은 `deque`의 `popleft()`를 사용했다. `deque`를 사용하지 않고 `pop(0)`을 사용 할수도 있지만, 범위가 `500,000`정도기 때문에 시간초과 판정이난다. 따라서 `deque`를 적극 사용하도록 하자.

`while`문의 범위를 `card`로만 작성하면 더 이상 뺼 원소가 없기때문에 오류가난다. `len(cards)`의 길이가 1이하로 줄어들때로 설정하자.

```python
import sys
from collections import deque
input = sys.stdin.readline

n = int(input())
cards = deque(range(1, n+1))

while len(cards) > 1:
    cards.popleft()
    cards.append(cards.popleft())

print(''.join(map(str, cards)))
```

---
## 📌 백준 1158 - 요세푸스 문제
<a href='https://www.acmicpc.net/problem/1158'>문제 설명</a>

## 💡 나의 풀이
요세푸스 문제는 `연결리스트(linkedList)`로 풀 수 있는 전형적인 문제이지만 `큐(queue)`를 사용해서도 풀 수 있다. 

1. k번째의 사람들이 계속해서 제거되어야하므로 cnt를 0으로 초기화한다.
2. `len(arr)`이 0이될때까지 제일 앞에있는 수가 제일 뒤로 이동하면서 순환한다.
3. 한번 순환 할때마다 `cnt`가 1씩 누적된다.
4. 만약, `cnt`가 `k-1`와 같다면 다음 사람이 제거되야하므로 해당 수를 `stack`에 추가한다.(인덱스는 0부터세므로 `k-1`로 선언했다.)
5. `stack`으로 빠졌다면 다시 0부터 카운트한다.

그럴싸한 로직이다. 하지만, 이대로 제출하면 실행시간이 비약적으로 높게나온다.

그래서 다음 제거할 사람의 인덱스를 찾을 때 `(k-1) mod N번` 포인터를 누적하는 방법을 사용했다. 이 방법을 사용하면 실행시간이 단축된다.

```python
# 나의 코드(cnt)
import sys
from collections import deque
input = sys.stdin.readline

n, k = map(int, input().split())
arr = deque(range(1, n + 1))
stack = []
cnt = 0

while arr:
    if cnt == k-1:
        stack.append(arr.popleft())
        cnt = 0
    else:
        arr.append(arr.popleft())
        cnt += 1

print(f"<{', '.join(map(str, stack))}>")
```

```python
# 다른사람의 코드(k-1 mod N)
import sys
input = sys.stdin.readline

n, k = map(int, input().split())
arr = list(range(1, n + 1))
stack = []
cnt = 0

while arr:
    cnt = (cnt+(k-1)) % len(arr)
    stack.append(arr.pop(cnt))

print(f"<{', '.join(map(str, stack))}>")
```

---
## 📌 백준 10773 - 제로
<a href='https://www.acmicpc.net/problem/10773'>문제 설명</a>

## 💡 나의 풀이
1. 빈 리스트를 선언한다.
2. 입력이 0이면 `pop`, 아니면 리스트에 추가한다.
3. 남은 값들을 모두 더한다.

```python
import sys
input = sys.stdin.readline

n = int(input())
stack = []

for _ in range(n):
    recent = int(input())
    if not recent:
        stack.pop()
    else:
        stack.append(recent)
print(sum(stack))
```

---
## 📌 백준 18258 - 큐
<a href='https://www.acmicpc.net/problem/18258'>문제 설명</a>

## 💡 나의 풀이
<a href='https://ywtechit.tistory.com/96'> 백준 10773 - 제로 </a> 

와 비슷한 문제지만 `front`, `back`의 경우 그리고 `pop`에서 제일 앞에있는 정수를 빼는경우만 생각하면 된다. 제일 앞에있는 값을 빼낼때에는 `deque`를 사용하는것을 잊지말자.

```python
from collections import deque
import sys
input = sys.stdin.readline

n = int(input())
stack = deque([])

def push(x):
    stack.append(x)

def pop():
    if not stack:
        return -1
    return stack.popleft()

def size():
    return len(stack)

def empty():
    if not stack:
        return 1
    return 0

def front():
    if not stack:
        return -1
    return stack[0]

def back():
    if not stack:
        return -1
    return stack[-1]

for _ in range(n):
    command = input().split()
    if 'push' in command:
        push(command[1])
    elif 'front' in command:
        print(front())
    elif 'back' in command:
        print(back())
    elif 'size' in command:
        print(size())
    elif 'empty' in command:
        print(empty())
    else:
        print(pop())
```

---
## 📍 백준 1966 - 프린터 큐

<a href='https://www.acmicpc.net/problem/1966'>백준 1966 - 프린터 큐</a>

## ⚡️ 나의 풀이
문제가 잘 이해가 되지 않아 4 ~ 5번정도 다시 봤다. 결론적으로 현재 `index`와 동일한 `우선순위`값이 제일 클 때 `cnt+=1`을 해주면 된다. 다른 테스트케이스는 괜찮았는데 중복된 우선순위가 있는 문서를 처리 할 때 고민을 많이 했다. `예제 입력 1 - 테스트케이스` 중 제일 마지막 `1, 1, 9, 1, 1, 1`을 예로 들어보자. ~~(글씨 양해 부탁드립읍니다.)~~

![](https://images.velog.io/images/abcd8637/post/4a78b8ed-0acd-4fc5-bfc7-2f905052079f/KakaoTalk_Photo_2021-06-24-09-21-43.jpeg)

1. 자신보다 높은 우선순위가 없을 때까지 회전한다.(이때는 `cnt`가 올라가지 않는다. why? 인쇄를 하지 않았기 때문)
2. `pop` 할 위치(가장 첫번째 index)에 위치 했을 때 해당 값의 우선순위가 제일 높다면 `pop`처리하고 `cnt+=1` 해준다.
3. 2번과정에서 만약, `pop` 값이 내가 찾고 있는 `target`이면, 해당 `cnt`를 출력하고 반복문을 종료(`break`)한다.

여담으로 `python - import PriorityQueue` 방법으로 접근했는데 풀지 못했는데 이유는 다음과 같다.

1. `PriorityQueue` 라이브러리는 가장 낮은 값부터 출력한다. (이는 `우선순위 * -1`으로 해결했다.)
2. `PriorityQueue` 라이브러리는 우선순위가 동일할 때 삽입순서에 따라 요소가 반환된다.(이 부분을 해결하지 못했는데, 프린터 큐 문제는 `index`가 동일할 때 `삽입순서`가 아닌 현재 `queue` 에 들어있는 값 그대로 출력을 해야한다. 여기서 더 좋은 접근법이 있다면 댓글로 알려주시면 감사하겠습니다. 😀 😀)

```python
T = int(input())

for _ in range(T):
    n, m = map(int, input().split())
    priority = list(map(int, input().split()))
    index = [i for i in range(n)]
    index[m] = 'target'    # 내가 찾고 싶은 index
    cnt = 0

    while priority:
        if priority[0] == max(priority):    # 나머지 문서들보다 중요도가 더 높은 문서가 없다면
            cnt += 1
            if index[0] == 'target':
                print(cnt)
                break
            priority.pop(0)
            index.pop(0)
        else:
            priority.append(priority.pop(0))
            index.append(index.pop(0))
```