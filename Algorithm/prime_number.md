# 소수판별 알고리즘 1

```python
import math

n = 100

def is_prime_number(x):
    for i in range(2, int(math.sqrt(x))+1):
        if i % x == 0:
            print('not prime')
        else:
            print('prime')
```

# 소수판별 알고리즘 2(에라토스테네스의 체)
```python
import math

n = int(input())

array = [ True for in range(n+1) ]

for i in range(2, int(math.sqrt(n))+1):
    if array[i] == True:
        j = 2
        while i * j <= n:
            array[i*j] = False
            j = j + 1

for i in range(2, n+1):
    if array[i]:
        print(i, end = ' ')
```

# 소수판별 알고리즘 2(에라토스테네스의 체 응용: 구간 별 소수찾기) 
```python
import math

n, m = map(int, input().split())

array = [True for i in range(m + 1)]

for i in range(2, int(math.sqrt(m)) + 1):
    if array[i] == True:
        j = 2
        while i * j <= m:
            array[i * j] = False
            j = j + 1

for i in range(n, m + 1):
    if array[i]:
        print(i, end=' ')
```

# 소수판별 알고리즘 3(<a href='https://www.acmicpc.net/problem/2153'>백준 - 2153</a>) 
알고리즘 문제푸는게 익숙치 않아 오래걸렸는데, 순전히 나의 힘으로 문제를 풀었다.
그만큼 내가 집중해서 해결했다는 얘기다.
엄청 고민했는데 다시보니까 코드가 길지 않아서 놀랬다 😮 😮

처음부터 `String`을 `input`으로 받고나서 해결하려니까 잘 안됐다.
`A` -> `Apple` -> `input`로 설정하면서 점차적으로 답안의 범위를 넓혀갔다. 

처음 답안을 제출했을 때, 맞았다고 생각했으나
문제에서 소문자 `a`는 1로, 대문자 `A`는 27로 바꿔야하는데 뒤집어서 풀었다.

`Ascii`코드표를 보니까 소문자 `a`는 97로, 대문자 `A`는 65로 설정되어있었다.
그래서 `소문자 - 96`을 통해 1 로만들고, `대문자 - 38`을 통해 27로 설정했다.

처음으로 `ord()`, `isupper()` 함수를 사용했는데 이런 함수가 있었는지 몰랐다.

나머지 소수판별 함수는 코딩테스트에서 공부했던대로 작성했다.
`에라토스테네스의 체`를 사용하진 않고 제곱근까지만 구해서 나머지 문제를 풀었다.

<span style='color:blue'>결론적으로 알고리즘문제를 푸는데 오래걸렸지만 `맞혔습니다`란 글자를 보면 뿌듯한 느낌이 너무 좋았다. 🤩 🤩</span>

```python
import math
import sys

data = sys.stdin.readline().rstrip()
n = list(data)
result = 0

for i in n:
    if i.isupper() == True:
        result = result + (ord(i) - 38)
    else:
        result = result + (ord(i) - 96)

def is_prime_sqrt(result):
    for i in range(2, int(math.sqrt(result)) + 1):
        if result % i == 0:
            return 'It is not a prime word.'
    else:
        return 'It is a prime word.'


print(is_prime_sqrt(result))

```
