## recursive_function
자기 자신을 다시 호출하는 함수이다.

가장 간단한 식
```python
def recursive_function():
    print('재귀함수를 호출합니다.)
    recursive_function

print(recursive_function())
👉🏽 RecursionError: maximum recursion depth exceeded while calling a Python object
```

이 오류메시지는 재귀의 최대 깊이를 초과했다는 내용이다. 
보통 파이썬 인터프리터는 호출 횟수 제한이 있는데 이 한계를 벗어났기 때문이다. 따라서 무한대로 재귀 호출을 진행 할 수는 없다.

다음과 같이 종료조건을 준다.
```python
def recursive_function(i):
    if i == 3:
        return
    print(f'{i}번째에서 {i+1}번째 재귀 함수를 호출합니다.')
    recursive_function(i+1)
    print(f'{i}번째에서 함수를 종료합니다.')

recursive_function(1)
👉🏽1번째에서 2번째 재귀 함수를 호출합니다.
2번째에서 3번째 재귀 함수를 호출합니다.
3번째에서 4번째 재귀 함수를 호출합니다.
4번째에서 5번째 재귀 함수를 호출합니다.
4번째에서 함수를 종료합니다.
3번째에서 함수를 종료합니다.
2번째에서 함수를 종료합니다.
1번째에서 함수를 종료합니다.
```

재귀 함수의 수행은 스택 자료구조를 이용한다.
함수를 계속 호출했을 때 가장 마지막에 호출한 함수가 먼저 수행을 끝내야 그 앞의 함수 호출이 종료되기 때문이다.
(스택구조는 선입후출 방식이다.)
결론적으로 재귀함수는 내부적으로 스택 자료구조와 동일하다는 것만 기억하자.

재귀함수를 이용하는 문제는 대표적으로 `팩토리얼(factorial)` 문제가 있다. 팩토리얼문제는 `반복문`, `재귀함수`방식으로 풀 수 있다.

```python
# 반복문
def for_factorial(n):
    result = 1
    for i in range(1, n+1):
        result = result * i
    return result

print(for_factorial(5))
👉🏽 120

# 재귀함수
def recursive_factorial(n):
    if n <= 1:
        return 1
    
    return result * for_factorial(n-1)

print(recursive_factorial(5))
👉🏽 120

```

---
## 📍 코드업 1901 - 1부터 n까지 출력하기

<a href='https://codeup.kr/problem.php?id=1901'>코드업 1901 - 1부터 n까지 출력하기</a>

### ⚡️ 나의 풀이
재귀함수 문제 중 같은 문제라도 1부터 n까지 구하는 문제가 있는 반면, n부터 1까지 역순으로 구하는 문제도 있다.

재귀함수에서 알아두어야 할 자료구조는 `스택(stack)`이다. stack의 특성 상 재귀함수는 나중에 들어온 값이 제일 먼저 나가게 되는 `후입선출(LIFO)`구조인데, 여기서도 제일 마지막에 호출한 함수를 제일 먼저 호출하는 과정을 거친다.

이 문제는 1부터 n까지 구하는 문제인데, 함수의 호출 순서를 알고 싶어 print(f(n))을 설정했다.
또 마지막에 `return`을 적지 않아도 되지만, 어떠한 흐름으로 진행되는지 알고싶어 명시적으로 적었다.

전체적인 흐름은 다음과 같다.

입력값에 5가 들어오게 되면 5는 1과 같지않으므로 `bottom_up(4)`를 호출하게된다. `bottom_up(4)`는 1과 같지않으므로 `bottom_up(3)`를 호출하게 되고 마지막으로 n이 1일 때는 print(n)을 거치고 `return`을 하게된다. `return`을 할 때는 스택에 호출됐던 함수들을 다시 찾아간다(밑에서부터) `bottom_up(1)`을 호출한 `n=2`는 print(n)을 하게되고 또 다시 올라가게된다. 결과적으로 print는 1에서부터 n까지 출력하게 된다.

| n | stack | print | 
| :----: | :----: | :----: | 
| 5 | bottom_up(4) | 5 |
| 4 | bottom_up(3) | 4 |
| 3 | bottom_up(2) | 3 |
| 2 | bottom_up(1) | 2 |
| 1 | 1 | 1 |

하단에 사진은 재귀함수 호출의 흐름을 화살표로 그려봤다.

![](https://images.velog.io/images/abcd8637/post/3ce0bdc9-83fe-44ad-8c93-3b70ed42a018/KakaoTalk_Photo_2021-03-17-14-56-55.jpeg)


```python
def bottom_up(n):
    print(f'f({n})', end=' ')
    if n != 1:
        bottom_up(n-1)
    
    print(f'f({n})', n)
    return

bottom_up(5)

👉🏽 
f(5) 
f(4) 
f(3) 
f(2) 
f(1) f(1) 1
f(2) 2
f(3) 3
f(4) 4
f(5) 5
```

---
## 📍 코드업 1902 - 1부터 n까지 역순으로 출력하기


<a href='https://codeup.kr/problem.php?id=1902'>코드업 1902 - 1부터 n까지 역순으로 출력하기</a>

### ⚡️ 나의 풀이
이번엔 반대로 n부터 1까지 출력하는 문제이다.

1901문제랑 다른점은 `print(n)`의 위치인데 여기에서는 다른 함수를 호출하기 전 `print(n)`을 작성해주었다. 

현재 들어온 n값을 먼저 출력하고 다른 함수를 호출하기 때문에 n부터 1까지 순서대로 값이 출력된다. 그리고 호출 한 지점에서부터 다음 코드는 어떤 행위(?)를 하는 코드가 없기때문에 호출만 될 뿐 값은 출력하지 않는다.

이번에도 `return` 되는 지점을 알고 싶어 명시적으로 작성했다. `return`을 적지 않아도 본래 함수 맨 마지막에는 `return`이 들어가있다.

![](https://images.velog.io/images/abcd8637/post/102ad1ee-00a9-4f30-8516-74ac61086a32/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-17%2015.13.35.png)

```python
def top_down(n):
    print(f'f({n})', end=' ')
    print(n)
    if n != 1:
        top_down(n-1)
    print(f'f({n})')

top_down(5)
👉🏽
f(5) 5
f(4) 4
f(3) 3
f(2) 2
f(1) 1
f(1)
f(2)
f(3)
f(4)
f(5)
```

## 📍 코드업 1904 - 두 수 사이의 홀수 출력하기

<a href='https://codeup.kr/problem.php?id=1904'>코드업 1904 - 두 수 사이의 홀수 출력하기</a>

### ⚡️ 나의 풀이
범위내의 값을 출력할때는 어떻게 할까 고민을 했다.
딱히 떠오르지 않아 먼저, 홀수만 출력하는 코드를 짜보자!라는 생각이 들어 샤프를 끄적거리며 홀수만 출력할때 재귀함수의 종료조건을 작성하다가 1 대신에 다른 변수가 들어가면 범위내의 값을 출력할 수 있겠네?!라는 생각을 했다.

그리고 앞선문제와 달리 변수를 2개 받기 때문에 재귀함수 호출 조건에서도 인자를 2개 넣어줘야 했다. 그럼 지금보다 -1 작은값을 넣어줄때마다 a보다 작으면 더 이상 호출을 안하게 설정하면 되겠다. 라는 생각을 했다.

코드를 그대로 구현했더니 정답판정을 받았다.

```python
a, b = map(int, input().split())

def func_odd(a, b):
    if b > a:
        func_odd(a, b-1)

    if b % 2 == 1:
        print(b, end=' ')
    else:
        return

func_odd(a, b)
```

---
## 📍 코드업 1905 - 1부터 n까지의 합 구하기

<a href='https://codeup.kr/problem.php?id=1905'>코드업 1905 - 1부터 n까지의 합 구하기</a>

### ⚡️ 나의 풀이
쉽게 풀 수 있었는데도 불구하고 어렵게 빙빙 돌아가서 푼 문제였다. `sum`값에 현재 값을 더한 값을 빈 리스트에 추가한 다음 `print()`했는데, 그러지 않고도 쉽게 문제를 풀 수 있었다.

1보다 작거나 같은 값은 1로 반환시켜주고 그렇지 않은 값들은 n에 재귀적으로 값을 더해주면 됐다.

너무 어렵게 생각하면 안되겠다는것을 느꼈다.

```python
import sys
sys.setrecursionlimit(1000000)

# 1번(어렵게 푼 문제)
sum = 0
def sum_number(n):
    global sum
    if n != 1:
        sum_number(n-1)
    sum+=n
sum_number(int(input()))

print(sum)

# 2번(쉬운 방법)
def plus(n):
    if n <= 1:
        return 1
    return plus(n-1) + n

print(plus(int(input())))
```

---
## 📍 코드업 1920 - 2진수 변환

<a href='https://codeup.kr/problem.php?id=1920'>코드업 1920 - 2진수 변환</a>

### ⚡️ 나의 풀이
2진수를 구현하는 법을 알고 있었는데 막상 재귀함수로 풀어보려고하니까 잘 생각이 떠오르지 않았다. 핵심 코드는 이렇다.

>1. 나머지를 2로 나눈다.
>2. 출력한다.
>3. 몫을 2로 나눈다.
>4. 언제까지? n이 1보다 작아질때까지

1905번처럼 빈 리스트에 추가해서 `join`함수를 사용했는데, 그럴필요가 없었다. 비록 정답판정을 받았지만 30분동안 삽질하고 다른코드를 보니까 허무(?)했다.

너무 어렵게 생각하지 말자!

```python
# 1번 어렵게 푼 문제
x = 7
result = []

while x != 0:
    result.append(x % 2)
    x //= 2
print(result)

result = []
def binary(n):
    if n == 0:
        return print(0)
    global result
    if n > 1:
        binary(n // 2)
    result.append(n % 2)
binary(int(input()))
print(''.join(map(str,result)))

# 2번 쉽게 푼 문제
def binary(n):
    if n > 1:
        binary(n // 2)
    return print(n % 2, end='')

binary(10)
```