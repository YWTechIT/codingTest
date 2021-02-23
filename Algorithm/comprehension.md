## 📍 comprehension(컴프리헨션)
iterable한 오브젝트를 생성하기 위한 방법 중 하나로 파이썬에서 사용 할 수 있는 유용한 기능이다.
즉, 반복되거나 특정 조건을 만족하는 자료형으로 쉽게 만들어 내기 위한 방법이다.

python에는 총 4개의 comprehension이 있다.
>1. list comprehension(LC)
>2. set comprehension(SC)
>3. dict comprehension(DC)
>4. generator comprehension(GC)

### ⚡️ List Comprehension
반복되거나 특정 조건을 리스트형으로 구현하고 싶을 때 주로 사용한다.

```python
# 1. 1부터 100까지 생성하기
array = [_ for _ in range(1, 101)]

# 2. 1부터 10까지 짝수만 생성하기
array = [i for i in range(1, 11) if i % 2 == 0]

# 3. 1부터 10까지 홀수만 생성하기
array = [i for i in range(1, 11) if i % 2 == 1]

# 4. '정'을 제외한 나머지 값들을 새로운 리스트에 담기
array = ['갑', '정', '병', '기']
result = [i for i in array if i != '정']
👉🏽 ['갑', '병', '기']

# 5. 대문자만 새로운 리스트에 담기
alpha = ['A', 'b', 'c', 'D', 'e', 'F', 'G', 'h']
result = [i for i in alpha if i == i.upper()]
👉🏽 ['A', 'D', 'F', 'G']

# 6. 모음만 제거하기
word = 'mathematics'
not_vowel = ' '.join([i for i in word if i not in ['a', 'e', 'i', 'o', 'u']])
👉🏽 m t h m t c s

# 7. 문자열 두개를 더하기
a = '12345'
b = 'abc'
result = ' '.join([i+j for i in a for j in b])
👉🏽 1a 1b 1c 2a 2b 2c 3a 3b 3c 4a 4b 4c 5a 5b 5c
```
---

### ⚡️ Set Comprehension
list와 사용법은 동일하고 결과값에 중복과 순서가 없는것이 특징이다.
```python
word = 'mathematics'
not_vowel = ' '.join({i for i in word if i not in ['a', 'e', 'i', 'o', 'u']})
👉🏽 c h s t m
```
---

### ⚡️ Dictionary Comprehension
> {key:value for 요소 in 입력시퀀스}

요소를 입력시퀀스에서 꺼낸 변수로 선언하고 `key:value`형태로 출력한다.

```python
info = {'name': 'AYW', 'age':27, 'height': 170}
result = {key: value for key, value in info.items()}
👉🏽 {'name': 'AYW', 'age': 27, 'height': 170}
```

---

### ⚡️ Generator Comprehension
```python
gen = (x**2 for x in range(10))
# <generator object <genexpr> at 0x105bde5c8>
print(next(gen)) # call 1
# 0
print(next(gen)) # call 2
# 1
# 'next' 함수 호출을 10번 반복
for i in range(20):
   print(next(gen))
"""
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
"""

# Yes, it is an just generator. You can sum the yielding values.
# GE로 생성한 Generator도 yield를 가진 함수로 생성한 것과 동일한 Generator이기 때문에, 똑같이 sum을 사용할 수 있다. (iterable 객체)
gen = (x**2 for x in range(10))
sum_of_squares = sum(gen)
👉🏽 285
```