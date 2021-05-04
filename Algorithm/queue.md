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