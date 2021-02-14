## base_calculation(진법 변환)
ex) number = 10
> 1. 2진수: 0b1010
> 2. 8진수: 0o12
> 3. 16진수: 0xa

---
## 📍 python 내장함수

```python
number = 10

# 차례대로 2진법, 8진법, 10진법, 16진법
bin(number)
oct(number)
int(number)
hex(number)
```

---

## 📍 10진수 -> n진수 convert

```python
# n <= 10진수
n = 2
x = 11
y = ''

while x != 0:
    y = str(x % n) + y
    x = x // n
print(y)
```

```python
# n > 10진수
# char은 x만큼 바꿔줘야함
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