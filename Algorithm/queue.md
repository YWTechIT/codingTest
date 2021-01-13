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