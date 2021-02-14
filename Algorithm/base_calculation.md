## base_calculation(진수 변환)
ex) number = 10
> 1. 2진수: 0b1010
> 2. 8진수: 0o12
> 3. 16진수: 0xa

---
## 📍 python 내장함수(bin, oct, int, hex)

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