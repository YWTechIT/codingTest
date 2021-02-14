## base_calculation(진수 변환)
ex) number = 10
> 1. 2진수: 0b1010
> 2. 8진수: 0o12
> 3. 16진수: 0xa

---
## 📍 python 내장함수(bin, oct, int, hex)
int함수는 기본적으로 `int(x, base = 10)`이 되어있다.

```python
number = 10

# 차례대로 2진법, 8진법, 10진법, 16진법
bin(number)
oct(number)
int(number)
hex(number)
```

---

## 📍 python import string(2진수 -> 16진수)
```python
import string

notation = string.digits + string.ascii_uppercase

n, base = map(int, input().split())
y = ''

while n != 0:
    y = str(notation[n % base]) + y
    n = n // base
print(y)
```

---

## 📍 2 <= n <= 16 base_convert

```python
# 2 <= n <= 16진수
x, base = map(int, input().split())
char = '0123456789ABCDEF'
y = ''

while x != 0:
    y = str(char[x % base]) + y
    x = x // base
print(y)
```

---

## 📍 n진수 to 10진수
```python
number = 0x11
print(int(number))
```

```python
# base: 현재 진수
base = int(input())
number = '1011' 
decimal = 0

for idx, val in enumerate(x[::-1]):
    decimal = decimal + (base ** idx) * int(val)
print(decimal)
```

---

## 📍 n진수 to n진수
기본적으로 n진수 to n진수를 하려면 다음의 순서를 거쳐야 한다.
>1. n진수 -> 10진수
>2. 10진수 -> n진수

풀이 순서는 다음과 같다.
>1. int()안에 '문자열'과 변환진법를 입력하면 해당 진법의 수를 입력 받는다.
   * 예를들어 int(314, 8)이면 8진법의 314를 10진법으로 변환함.
>2. 변환하고 싶은 함수(진수)를 쓰고 안에 값을 입력한다.
   * bin(204)
>3. 값만 출력하고 싶으면 인덱싱을 이용해서 출력.
   * print(bin(204) [2:])

```python
# bin(2진수), oct(8진수), hex(16진수)
print(bin(int(input(), 8)) [2:])
```

---

### 📍 백준 14915 - 진수 변환기
<a href='https://www.acmicpc.net/problem/14915'>백준 14915 - 진수 변환기</a>

채점 중 90% 이상까지 올라갔을때, 조건을 다시 확인 할것
`x == 0`일 조건을 생각안해서 오답판정이났다.
그리고, `x == 0`일 조건은 `while`문 밖에서 선언해야함.

```python
x, base = map(int, input().split())
r = ''
char = '0123456789ABCDEF'

if x == 0:
    print(0)

while x != 0:
    r = str(char[x % base]) + r
    x = x // base
print(r)
```

---

### 📍 백준 1212 - 8진수 2진수
<a href='https://www.acmicpc.net/problem/1212'>백준 14915 - 진수 변환기</a>

놀라울정도로 코드가 짧아서 놀랐다.

```python
print(bin(int(input(), 8)) [2:])
```

---