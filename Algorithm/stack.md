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