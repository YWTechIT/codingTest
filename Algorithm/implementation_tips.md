## 💡 implementation_tips

---
## 📍 list에서 첫번째, 마지막 값만 변수로 선언하기
```python
array = [10, 20, 30, 40, 50]

first_index, *rest, last_index = array

print(first_index)
👉🏽 10
print(*rest)
👉🏽 20 30 40
print(last_index)
👉🏽 50
```

---
## 📍 Swap
두 변수의 값을 바꾸는 기능
```python
# 기존
a = 'MyName'
b = 'AYW'

temp = a
a = b
b = temp
👉🏽 AYW MyName

# 향상
a = 1
b = 2

a, b = b, a
print(a, b)
👉🏽 2 1
```

---
## 📍 Packing
하나의 변수에 여러 값을 할당하는 방법
```python
a, b, c = [1, 2, 3]
d = a, b, c

print(d)
👉🏽 (1, 2, 3)
```

---
## 📍 Unpacking
for문을 사용하지 않고도 iterable한 결과를 출력하고 싶을 때
`tuple`, `set`형도 가능하다.

```python
array = [1, 2, 3, 4, 5]

for i in array:
    print(i, end=' ')
👉🏽 1 2 3 4 5

print(*array)
👉🏽 1 2 3 4 5
```

---
## 📍 zip
동일한 개수로 이루어진 자료형을 묶어주는 함수다
```python
fruits = ['alpha', 'bravo', 'charlie']
name = [1, 2, 3]

for f, n in zip(fruits, name):
    print(f, n)

👉🏽alpha 1
bravo 2
charlie 3

print(list(zip(fruits, name)))
👉🏽 [('alpha', 1), ('bravo', 2), ('charlie', 3)]

print(dict(zip(fruits, name)))
👉🏽 {'alpha': 1, 'bravo': 2, 'charlie': 3}
```

>reference: <a href='https://github.com/VSFe/Algorithm_Study/blob/main/Concept/00_Special/Pythonic_Code_For_Coding_Test.md'>VSfe_github</a>

---
## 📍 n번째 자리까지 무조건 출력하기

```python
# 소수점 넷째자리에서 반올림하여 무조건 소숫점 셋째 자리까지 출력 할 때.
a, b = map(float, input().split())
print('%.3f' %(a/b))
👉🏽 2.000
```
