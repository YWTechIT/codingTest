## Stack
`선입후출(First In Last Out)` 구조 또는 `후입선출(Last In First Out)` 구조라고 한다. 

Box를 쌓는 모습을 연상하면된다.
먼저 들어온 수는 가장 나중에 나간다.
시간복잡도는 `O(1)`

```python
stack = []

stack.append(5)
stack.append(2)
stack.append(3)
stack.append(7)
stack.pop()
stack.append(1)
stack.append(4)
stack.pop()

print(stack)
👉🏽 [5, 2, 3, 1]

print(stack[::-1])
👉🏽 [1, 3, 2, 5]
```

