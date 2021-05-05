## Deque

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

---
## 📌 백준 10866 - 덱
<a href='https://www.acmicpc.net/problem/10866'>문제 설명</a>

## 💡 나의 풀이
<a href='https://ywtechit.tistory.com/96'>백준 10828 - 스택</a>과 <a href='https://ywtechit.tistory.com/97'>백준 18258 - 큐</a>와 같은 유형이면서 다른 자료구조인 덱 문제다. 

이번에는 이전에 공부했던 내용인 <a href='https://ywtechit.tistory.com/26'>단락평가</a>를 이용해서 문제를 풀어봤는데 코드가 조금 간결해진것 같다. 단락평가를 이용하여 코드를 짧게 구현해보는 방법도 익혀두자.

```python
import sys
from collections import deque
input = sys.stdin.readline

def push_front(x):
    stack.appendleft(x)

def push_back(x):
    stack.append(x)

def pop_front():
    return stack and stack.popleft() or -1

def pop_back():
    return stack and stack.pop() or -1

def size():
    return len(stack)

def empty():
    return not stack and 1 or 0

def front():
    return stack and stack[0] or -1

def back():
    return stack and stack[-1] or -1

n = int(input())
stack = deque([])

for _ in range(n):
    command = input().split()
    if 'push_front' in command:
        push_front(command[1])
    elif 'push_back' in command:
        push_back(command[1])
    elif 'pop_front' in command:
        print(pop_front())
    elif 'pop_back' in command:
        print(pop_back())
    elif 'size' in command:
        print(size())
    elif 'empty' in command:
        print(empty())
    elif 'front' in command:
        print(front())
    else:
        print(back())
```