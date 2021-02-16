## built_in_function

1. eval(): 해당 수식을 계산한 결과를 반환
```python
result = eval('(3+5) * 7')
👉🏽 56
```

2. sorted(): `iterable` 객체가 들어왔을 때, 정렬된 결과를 반환
   * `iterable`: [ List ], ( Tuple ), [ Dictionary ]
   * `key = lambda a: a[x]`, 원소기준으로 오름 / 내림 차순 정렬가능

3. sort(): `list iterable` 객체는 기본으로 `sort()` 함수 사용 가능
   * iterable: [ List ], ( Tuple ), [ Dictionary ]


```python
# sorted ()
data_list = [3, 1, 2, 5]
data_tuple = (3, 1, 2, 5)
data_dict = [('안영우', 26), ('동생1', 23), ('동생2', 13), ('동생3', 11)]
data_dict_key = sorted([('안영우', 26), ('동생1', 23), ('동생2', 13), ('동생3', 11)], key = lambda x: x[1], reverse=True)

print(sorted(data_list))
👉🏽 [1, 2, 3, 5]
print(sorted(data_list, reverse=True))
👉🏽 [5, 3, 2, 1]

print(sorted(data_tuple))
👉🏽 [1, 2, 3, 5]
print(sorted(data_tuple, reverse=True))
👉🏽 [5, 3, 2, 1]

print(sorted(data_tuple))
👉🏽 [('동생1', 23), ('동생2', 13), ('동생3', 11), ('안영우', 26)]
print(sorted(data_tuple), lambda a: a[1])
👉🏽 [('안영우', 26), ('동생1', 23), ('동생2', 13), ('동생3', 11)]

# sort(only list)
data_list = [3, 1, 2, 5]
data_list.sort()

print(data_list)
👉🏽 [1, 2, 3, 5]
```

---

### 📍 abs(절대값 반환)
```python
abs(3)
👉🏽 3
```

---
### 📍 abs(절대값 반환)
```python
abs(3)
👉🏽 3
```
---

### 📍 all
모두 참이면 True, 거짓이 하나라도 있으면 False
```python
all([1,2,3])
👉🏽 True
all([1,2,3,0])
👉🏽 False
```
---

### 📍 any
하나라도 참이 있으면 True, 모두 거짓이면 False
```python
any([1,2,3])
👉🏽 True
any([0,''])
👉🏽 False
```
---

### 📍 divmod(a,b)
a를 b로 나눈 몫과 나머지를 튜플형태로 리턴
```python
divmod(7,3)
👉🏽 (2, 1)
```
---

### 📍 enumerate
순서가 있는 자료형을 입력으로 받아 인덱스 값을 포함하는 enumerate 객체를 리턴한다.
```python
for idx, val in enumerate(['body', 'foo', 'bar'])
👉🏽 0 body
1 foo
2 bar
```
---

### 📍 lambda
함수를 한 줄 간격으로 만들 때 사용
```python
sum = lambda a, b: a+b
sum(3,4)
👉🏽 7
```
---

### 📍 zip
동일한 개수로 이루어진 자료형을 묶어주는 역할
```python
list(zip([1, 2, 3], [4, 5, 6]))
👉🏽 [(1, 4),(2, 5),(3, 6)]
list(zip([1, 2, 3], [4, 5, 6],[7, 8, 9]))
👉🏽 [(1, 4, 7),(2, 5, 8),(3, 6, 9)]
list(zip('abc','def'))
👉🏽 [('a','d'),('b','e'),('c','f')]
```
---