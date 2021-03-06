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
## 📍 Packing
하나의 변수에 여러 값을 할당하는 방법
```python
a, b, c = [1, 2, 3]
d = a, b, c

print(d)
👉🏽 (1, 2, 3)
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