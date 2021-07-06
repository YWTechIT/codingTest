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

---
### 📍 [ 문제 1 ] 백준 9012 - 괄호
문제: <a href='https://www.acmicpc.net/problem/9012'>백준 9012 - 괄호</a>

### 💡 나의 풀이
스택에 대해 공부를 하던 중 관련된 문제를 풀고 싶어 백준을 기웃거리다 찾은 문제였다.

`Parenthesis String` 관련된 문제 중 괄호가 `(`,`)`로 고정되어있어 그나마 쉽다고 생각했는데 정답판정까지의 시간이 상.당.히. 오래걸렸다. ~~(조건문에 열린괄호를 닫힌괄호라고 쓰고 1시간동안 헤맨건 비밀 🤣 🤣)~~

먼저, `PS`는 열린괄호와 닫힌괄호가 정상적으로 맞아떨어지면 `YES`라고 출력한다.
그런데, 정상적으로 떨어지지 않는경우를 따져봐야하는데 나는 이렇게 생각했다.

우선, 예제 입력의 값 중 `NO`라고 출력되는 값들만 쭉 적어봤다.
예제 입력 1-1의 경우 마지막 `)`가 나왔을 때 이미 열린 괄호는 맞아 떨어지고 없기 때문에 `NO`라고 출력되었다.
예제 입력 1-2의 경우 마지막에 열린괄호만 남았기 때문에 `NO`라고 출력되었다.
예제 입력 1-4의 경우 마찬가지로 열린괄호만 남았기 때문에 `NO`라고 출력되었다.
예제 입력 1-6의 경우 마찬가지로 열린괄호만 남았기 때문에 `NO`라고 출력되었다.

예제 입력 2-1의 경우 열린괄호만 남았기 때문에 `NO`라고 출력되었다.
예제 입력 2-2의 경우 닫힌괄호가 나왔는데, 같이 없어질 열린괄호가 없기 때문에 `NO`라고 출력되었다.
예제 입력 2-3의 경우 마찬가지로 닫힌괄호가 나왔는데, 같이 없어질 열린괄호가 없기 때문에 `NO`라고 출력되었다.

이를 토대로 `NO`를 출력하는 경우는 다음과 같다.
>1. 조건에 닫힌 괄호가 나왔는데 같이 맞아 떨어지는 열린 괄호가 없을 때
>2. 모든 조건을 수행하고나서 리스트를 검사했을 때 값이 남은 경우

손으로 적으면서 반례의 경우를 생각하니까 코드를 구현하는건 어렵지 않았다.(시간이 오래걸릴 뿐)

중간에 `if len(result) == 0`이라고 작성했는데, result값이 비었을 때를 뜻하는 코드이고 `if not result:`로도 사용가능하다.

그리고 중간 조건문에 `return`값을 넣어주지않으면 하단 조건문에서 `YES`를 출력하므로 출력값이 달라진다. 참고하자.

```python
def check_VPS(data):
    result = []
    for i in data:
        if i == '(':
            result.append(i)
        else:
            if len(result) == 0:
                print('NO')
                return
            else:
                result.pop()
    
    if not result:
        print('YES')
    else:
        print('NO')

n = int(input())
for i in range(n):
    parenthesis = input()
    check_VPS(parenthesis)
```

---
## 📍 백준 10828 - 스택
문제: <a href='https://www.acmicpc.net/problem/10828'>백준 10828 - 스택</a>

## 💡 나의 풀이
3개월 전 이 문제를 봤을 때는 못 풀었는데 지금은 풀게 된 문제다. 그때는 왜 기능별로 함수를 만드는지 몰랐었는데... ~~(추억 돋음)~~

문제풀이는 다음과 같다.
1. 각 기능별로 함수를 만든다.
2. n만큼 입력을 받는데, 입력이 함수의 이름에 포함이되면 해당 함수를 실행시킨다.

참고로 함수안에 `if, else`문을 사용해도 되는데 `else`를 빼고 `return`문을 집어넣었다. `if`문 지나 조건을 통과하지못한 기능만 남아 자연스럽게 `return`을 만나기 때문이다. 또, `push` 값은 `split()`으로 나눠 `[1]`번째를 사용하면 된다.

```python
import sys
input = sys.stdin.readline

n = int(input())

stack = []
def push(x):
    stack.append(x)

def pop():
    if not stack:
        return -1
    return stack.pop()

def size():
    return len(stack)

def empty():
    if not stack:
        return 1
    return 0

def top():
    if not stack:
        return -1
    return stack[-1]

for _ in range(n):
    command = input().split()
    if 'push' in command:
        push(command[1])
    elif 'top' in command:
        print(top())
    elif 'size' in command:
        print(size())
    elif 'empty' in command:
        print(empty())
    else:
        print(pop())
```

---
## 📍 백준 17608 - 막대기
문제: <a href='https://www.acmicpc.net/problem/17608'>백준 17608 - 막대기</a>

## 💡 나의 풀이
일렬로 세워진 막대기를 `오른쪽`에서 봐야하기 때문에 막대기의 입력을 모두 받아 리스트로 만들고 문제를 풀었다. 처음에는 오답판정을 받았는데 최대 높이의 막대기를 갱신해주지 않아서 그랬다.

첫번째 방법은 반복문을 작성해 `sticks`를 거꾸로 보면서 최대의 막대기를 갱신한 방법이고 두번째 방법은 `sticks`를 `pop()`으로 하나씩 뽑아 최대값을 갱신하는 방법을 사용했다. `pop()`을 사용한 방법의 실행시간이 약 `30m/s`정도 빨랐다.

![](https://images.velog.io/images/abcd8637/post/e032db29-0b28-4f90-bba5-b0339767cfb3/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-28%2011.44.27.png)

(사진에서 첫번째 방법은 하단, 두번째 방법은 상단)

```python
# 나의 코드
import sys
input = sys.stdin.readline

n = int(input())
sticks = [int(input()) for _ in range(n)]
max_height = sticks[-1]
cnt = 1

for i in range(n):
    if max_height < sticks[n-i-1]:
        cnt += 1
        max_height = sticks[n-i-1]
print(cnt)
```

```python
# 나의 다른 코드
import sys
input = sys.stdin.readline

n = int(input())
sticks = [int(input()) for _ in range(n)]
max_height = sticks[-1]
cnt = 1

for i in range(n):
    temp = sticks.pop()
    if max_height < temp:
        cnt += 1
        max_height = temp
print(cnt)
```

---
## 📍 백준 1874 - 스택 수열
문제: <a href='https://www.acmicpc.net/problem/1874'>백준 1874 - 스택 수열</a>

## 💡 나의 풀이
나에겐 난이도가 있던 문제였다. 문제의 길이는 짧았지만서도 이해하기까지 시간이 오래 걸렸다. 

중요한 포인트는 `스택에 push하는 순서는 반드시 오름차순을 유지한다.`라는 문장인데, 이를 다시말하면 `push 순서`는 현재 만들어야 할 수열보다 작아 질 수 없고 오직 `current = target` 혹은 `current > target` 할때만 성립한다는 의미다. 이를 이해하기까지는 꽤 오랜시간이 걸렸다. 그럼 `current`는 어떻게 구현해야하지를 고민했는데 `1~n`까지 선언한 다음 여기서 뽑지 않은 값 중 가장 작은 값들을 가져와야하는 건가? 생각했는데 결론적으로 `current += 1씩` 증가하면서 값을 넣으면 된다. 

1. `current`가 `target`보다 작거나 같을 때 까지 `current`를 `stack`에 넣어준다. (push 연산)
2. 만약, `stack[-1]`이 `target`과 같다면 `pop` 연산을 수행한다.
3. 연산이 끝났을 때 `stack`에 아무것도 남아있지 않다면 `push, pop` 연산을 출력한다.
4. 연산이 끝났는데도 `stack`이 남아있거나 `current > target`이면 `NO`를 출력한다.

![](https://images.velog.io/images/abcd8637/post/c55e5dc9-d451-4fc7-9f7f-6816f123b017/KakaoTalk_Photo_2021-06-30-10-17-19.jpeg)

```python
# 나의 풀이
import sys
input = sys.stdin.readline

n = int(input())
targets = [int(input()) for _ in range(n)]

flag = True
stack, answer, current = [], [], 0

for target in targets:
    while True:
        if stack and stack[-1] == target:    # stack: 을 작성한 이유는 맨 처음 stack은 아무것도 없기 때문
            answer.append('-')
            stack.pop()
            break

        elif current > target:
            flag = False

        else:
            current += 1
            stack.append(current)
            answer.append('+')

        if not flag:
            print('NO')
            exit()

if flag:
    print('\n'.join(answer))
```

```python
# 다른 사람의 풀이
import sys
input = sys.stdin.readline

n = int(input())
targets = [int(input()) for _ in range(n)]
current = 1
stack, answer = [], []

for target in targets:
    while current <= target:
        stack.append(current)
        answer.append('+')
        current += 1

    if stack[-1] == target:
        answer.append('-')
        stack.pop()

if not stack:
    print('\n'.join(answer))
else:
    print('No')
```

---
## 📍 백준 10799 - 쇠 막대기
문제: <a href='https://www.acmicpc.net/problem/10799'>백준 10799 - 쇠 막대기</a>

## 💡 나의 풀이

`stack`으로 해결 할 수있는 문제이나, 나에게는 어려웠던 문제다. 이 문제를 풀 때 예제는 `올바른(짝이 맞는) 괄호`만 주어진다는 점을 알고 풀면 접근하기 쉬울 것이다. 깨알 팁은 입력범위가 `100,000`이라서 `import sys`를 써야 `시간초과`가 나지 않는다.

1. 여는 괄호(`(`)는 `stack`에 집어넣는다 
2. 닫는 괄호(`)`)가 나올 때 `쇠 막대기`인지 `레이저`인지 구분해야하는데, 우선 레이저는 인접한 쌍(즉, `현재 index가 )` 이면 무조건 `이전 index는 (`)이다. 그럼 나머지의 경우는 모두 쇠 막대기로 판단 할 수 있다.
3. 레이저의 경우는 현재까지 들어있는 `len(stack)`을 구하면 된다.(참고로 `stack`에 여는 괄호만 들어있다.)
4. 레이저가 아닌 경우(쇠 막대기인 경우)은 누적 `cnt` 값에 +1을 더해주면 된다.

이 문제의 관건은 `pop()`의 시점인데, 레이저의 경우 `stack[-1]`값을 `pop`해주고 `len(stack)`을 해주고, 쇠 막대기의 경우 `cnt += 1` 이후 `pop`을 해주는것이 전체 흐름을 파악하기에 적절하다.(물론 19, 20번째 코드를 뒤바꿔 제출해도 정답이다.)

```python
import sys
input = sys.stdin.readline

s = input().rstrip()
stack = []
cnt = 0

for i in range(len(s)):
    if s[i] == '(':
        stack.append('(')

    else:    # ')'
        if s[i-1] == '(':    # Razor
            stack.pop()
            cnt = cnt + len(stack)

        else:    # ')', ironBar
            cnt += 1
            stack.pop()
print(cnt)
```

---
## 📍 백준 4949 - 균형잡힌 세상
문제: <a href='https://www.acmicpc.net/problem/4949'>백준 4949 - 균형잡힌 세상</a>

## 💡 나의 풀이
문제의 조건을 잘 따져야 하는데 마지막 조건(`짝을 이루는 두 괄호가 있을 때, 그 사이에 있는 문자열도 균형이 잡혀야 한다.`)은 문자열 공백을 똑같이 줘야하는건가?라는 생각이 들면서 조금 헷갈렸다. 하지만 그건 문제에 주어져있지 않기때문에 고려하지 않아도 된다.

`올바른괄호`를 찾는 문제는 여러가지 `T.C`를 넣어가면서 에러가 걸리지 않게 로직을 짜는것이 중요한것 같다. 그리고 `while True`와 `while 1`의 차이를 물어보는 질문들이 꽤 있었는데, 결론부터 말하자면 두 개의 코드의 시간차이는 없다. 정확히 말하면 `python 2`에서는 `while 1`이 더 약 `3 ~ 4초` 가량 더 빠른데 왜 그러냐면 `python 2`에서는 `True` 키워드가 정의되어있지 않기 때문이다. 하지만 `python 3`에서는 `True` 키워드가 정의되어있기 때문에 인터프리터가 빠르게 읽어올 수 있고 `while 1`, `while True`의 실행시간은 동일하다. (<a href='https://stackoverflow.com/questions/3815359/while-1-vs-whiletrue-why-is-there-a-difference-in-python-2-bytecode'>stack_over_flow</a>)

1. 여는 괄호(`(`, `[`)는 `stack`에 넣는다.
2. `stack`이 있으면서 닫힌 괄호가 나올 때 `stack[-1]`과 짝이 맞는 괄호면 `pop`을 시키고 그렇지 않으면 flag를 `False`로 바꾼다.
3. `stack`이 없으면서 닫힌괄호가 나오면 정상적으로 짝이 맞지 않으므로 마찬가지로 flag를 `False`로 바꾼다.
4. `flag == True`이면서(정상적인 괄호) `not stack`이면 올바른 괄호열이고 반대의 경우는 올바르지 않은 괄호열이다.

```python
# 나의 코드

import sys
input = sys.stdin.readline

while True:
    s = input().rstrip()
    if s == '.':    # 종료 조건
        break

    stack = []
    flag = True    # 짝을 이루지 않는 경우

    for i in range(len(s)):
        if s[i] == '(' or s[i] == '[':
            stack.append(s[i])

        elif stack and (s[i] == ')' or s[i] == ']'):  # stack은 있지만 닫힌 괄호가 나오는 경우
            if s[i] == ')' and stack[-1] == '(':
                stack.pop()
            elif s[i] == ']' and stack[-1] == '[':
                stack.pop()
            else:    # (])
                flag = False

        elif not stack and (s[i] == ')' or s[i] == ']'):  # stack이 없으면서 닫힌 괄호가 나오는 경우, )(
            flag = False

    if flag and not stack:
        print('yes')
    else:
        print('no')
```

```python
# 다른 사람의 코드

import sys
input = sys.stdin.readline

while 1:
    string = input().rstrip()
    stack = []
    true_flag = 1
    
    for cha in string:
        if cha == '(' or cha == '[':
            stack.append(cha)
        elif cha == ')':
            if stack and stack[-1] == '(':
                stack.pop()
            else:
                true_flag = 0
                break
        elif cha == ']':
            if stack and stack[-1] == '[':
                stack.pop()
            else:
                true_flag = 0
                break

    if string == '.':
        break

    print("yes" if true_flag and not stack else "no")
```

---
## 📍 백준 3986 - 좋은 단어
문제: <a href='https://www.acmicpc.net/problem/3986'>백준 3986 - 좋은 단어</a>

## 💡 나의 풀이
어떤 방식으로 풀어야할지 고민하다 `stack`으로 풀었는데 정답판정을 받았다.

문제에서 아치형 곡선으로 만나야 한다고 나와있는데 `괄호 쌍`맞추는 문제처럼 `stack`으로 들어오는 현재 값과 이전에 있던 `stack[-1]`과 비교해서 같으면 `pop()` 다르면 새로운 값 추가 하는 방식으로 풀면 된다.

처음에 `stack`이 없을 때 값을 어떻게 넣지??라고 생각하다 `stack`에 값이 있을 때, 없을 때로 나눠서 조건을 작성했다. 여기서 나의코드와 다른사람 코드의 차이점은 `13 ~ 19번` 인데, `stack` 조건을 `and`로 합치고 아닌경우에는 `append`를 줘도 같은 결과가 나왔길래 가져왔다.

다음 사진은 예제 입력1을 손으로 그리면서 푼 사진이다.(~~글씨 주의~~)

![](https://images.velog.io/images/abcd8637/post/4bf0c724-700e-48cd-aa51-b3eadcb8c781/KakaoTalk_Photo_2021-07-06-11-32-30.jpeg)

```python
# 나의 코드
import sys
input = sys.stdin.readline

n = int(input())
cnt = 0

for _ in range(n):
    s = input().rstrip()
    stack = []

    for i in range(len(s)):
        if stack:
            if s[i] == stack[-1]:
                stack.pop()
            else:
                stack.append(s[i])
        else:
            stack.append(s[i])

    if not stack:
        cnt += 1
print(cnt)
```

```python
# 다른 사람 코드
import sys
input = sys.stdin.readline

n = int(input())
cnt = 0

for _ in range(n):
    s = input().rstrip()
    stack = []

    for i in range(len(s)):
        if stack and s[i] == stack[-1]:
            stack.pop()
        else:
            stack.append(s[i])

    if not stack:
        cnt += 1
print(cnt)
```
