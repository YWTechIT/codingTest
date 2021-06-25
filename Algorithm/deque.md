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

---
## 📌 백준 1406 - 에디터
<a href='https://www.acmicpc.net/problem/1406'>문제 설명</a>

## 💡 나의 풀이
어제 응시했던 2021 카카오 인턴십 온라인코딩테스트에서도 비슷한 문제가 나왔다. 다만 거기서는 `ctl + z`기능도 포함되어있어서 조금 더 어려웠던것 같다. 어떻게 풀어야할지 정말 많이 고민했는데, 결과적으로 `stack` 혹은 `deque`를 사용하면 쉽게 풀 수 있는 문제였다. 그리고 문제에서 시간 제한이 0.3초로 주어져있어서 O(N^2)으로는 풀 수 없다.

처음에 `len(s)`만큼 `cursor`를 선언해서 풀었지만 `B` 명령어의 예외처리를 어떻게 해줘야할지 모르겠다. 그리고 `cursor`를 사용해서 `insert`와 `remove`를 사용했는데 각각 시간복잡도가 `O(N)`이고 입력인 명령어를 받기위해 처음에 반복문을 한번 선언했기 때문에 이중 반복문이 되는 형태였다.

처음에 `deque`로 풀고, 두번째는 `stack`으로 풀었다. 두 방식 모두 시간복잡도가 O(N)이기 때문에 실행시간은 각각 `364ms`, `352ms`로 차이가 많지 않았다.

1. 빈 `deque(stack)`을 선언한다.
2. `L`: 커서를 왼쪽으로 한 칸 옮기는 명령어인 `L`이 들어오면 `L`보다 오른쪽에 있는 값들 모두 `deque_R`로 옮긴다. 옮길때는 `append`가 아닌 `appendleft()`로 해주는것을 잊지 말자.
3. `D`: 반대로 커서가 오른쪽으로 한 칸 옮기는 명령어인 `D`가 들어오면 `D`보다 왼쪽에 있는 값들 모두 `deque_L`로 옮긴다. 옮길때는 `append`가 아닌 `appendleft()`로 해주는것을 잊지 말자.
4. `B`: 삭제하는 기능은 `pop`으로 해결한다.
5. `P`: 추가하는 기능은 `append`로 해결한다.

명령어 `L`, `D`, `B` 공통적으로 커서가 문장의 맨 앞 / 맨 뒤면 무시하라는 조건이 있는데, 이는 `deque`의 길이보다 작으면 무시하는 조건을 넣어주면 된다.
`deque`의 출력은 리스트를 서로 더해주고 `join`을 해주면 되는데, `stack`같은 경우는 거꾸로 뒤집어줘야(reversed) 정상적인 출력이 나온다. 

```python
# deque
import sys
from collections import deque
input = sys.stdin.readline

deque_L, deque_R = list(input().strip()), deque([])
m = int(input())

for i in range(m):
    command = input().split()
    if 'L' in command:
        if not deque_L:
            continue
        deque_R.appendleft(deque_L.pop())

    elif 'D' in command:
        if not deque_R:
            continue
        deque_L.append(deque_R.popleft())

    elif 'B' in command:
        if not deque_L:
            continue
        deque_L.pop()

    else:
        deque_L.append(command[1])

print(''.join(deque_L + list(deque_R)))
```


```python
# stack
import sys
input = sys.stdin.readline

stack_L, stack_R = list(input().strip()), []
m = int(input())

for i in range(m):
    command = input().split()
    if 'L' in command:
        if not stack_L:
            continue
        stack_R.append(stack_L.pop())

    elif 'D' in command:
        if not stack_R:
            continue
        stack_L.append(stack_R.pop())

    elif 'B' in command:
        if not stack_L:
            continue
        stack_L.pop()

    else:
        stack_L.append(command[1])

print(''.join(stack_L + list(reversed(stack_R))))
```

---
## 📌 백준 1021 - 회전하는 큐
<a href='https://www.acmicpc.net/problem/1021'>백준 1021 - 회전하는 큐</a>

## 💡 나의 풀이
처음에는 한번에 2번연산 혹은 3번연산을 따로따로 진행하고 둘 중 작은 값을 출력하는건 줄 알았는데, `arr`을 보고 더 가까운 쪽에 2번연산, 3번연산을 판단해서 풀어야하는 문제였다.

머리로는 이해했는데 막상 구현하려니까 잘 떠오르지 않았다. 함수를 선언하여 풀었지만 왠지 코드가 많아 보였다. 

1. 현재 `arr`을 보고 `target`값이 몇번째 인덱스에 있는지 앞 / 뒤에서 판단하고 `return`한다.`(compare_min_length)`
2. 앞쪽이 더 가까우면 `2번 연산`을 진행한다.`(front_rotate)`
3. 뒤쪽이 더 가까우면 `3번 연산`을 진행한다.`(back_rotate)`

다른 사람의 코드를 보니까 `2, 3번 연산`은 기능을 구현하지 않아도 `python - deque`라이브러리에는 `rotate` <a href='https://docs.python.org/3/library/collections.html?highlight=deque#collections.deque'>내장 함수</a>가 구현되어있었다. 다음번에 꼭 써먹으리라..

그리고 다른사람은 `for`문 안에 `while`문을 넣어 작성했는데 코드도 짧고 가독성이 좋아보였다. 새로 배운점은 `arr`의 길이를 기준으로 `target_index`가 앞쪽에서 가까운지 뒤쪽에서 더 가까운지 판단하는 15번 코드인데 간결해보였다. 또, `rotate(-1)`은 2번 연산이고 `rotate(1)`은 3번 연산이다.

```python
# 나의 코드
from collections import deque
n, m = map(int, input().split())
target_indexes = list(map(int, input().split()))
cnt = 0
arr = deque([i for i in range(1, n+1)])

def compare_min_length(target):
    global arr
    for i in range(len(arr)):
        if arr[i] == target:
            return i, len(arr)-i-1

def front_rotate(target, cnt):    # 왼쪽으로 이동
    global arr
    while True:
        if arr[0] == target:
            arr.popleft()
            return cnt
        arr.append(arr.popleft())
        cnt += 1

def back_rotate(target, cnt):    # 오른쪽으로 이동
    global arr
    while True:
        if arr[0] == target:
            arr.popleft()
            return cnt
        arr.appendleft(arr.pop())
        cnt += 1

for target in target_indexes:
    front, back = compare_min_length(target)
    if front <= back:
        temp_cnt = front_rotate(target, cnt)
    else:
        temp_cnt = back_rotate(target, cnt)
    cnt = temp_cnt
print(cnt)
```

```python
# 다른사람의 코드
from collections import deque

n, m = map(int, input().split())
target_indexes = list(map(int, input().split()))
cnt = 0
arr = deque([i for i in range(1, n+1)])

for target in target_indexes:
    while True:
        if arr[0] == target:
            arr.popleft()
            break
        else:
            if arr.index(target) <= len(arr) // 2:
                arr.rotate(-1)
            else:
                arr.rotate(1)
            cnt += 1
print(cnt)
```

