## deque_function

1. deque(): `Queue`라이브러리는 일반적인 큐 자료구조를 구현하는 라이브러리는 아니다. 따라서, `deque()`를 이용해 큐를 구현해야 한다.

```python
from collection import deque

data = deque([2, 3, 4])

data.appendleft(1)
data.append(5)

print(data)
👉🏽 deque([1, 2, 3, 4, 5])

print(list(data))
👉🏽 [1, 2, 3, 4, 5]
```