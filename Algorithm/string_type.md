## string_type(문자 자료형)

### 📍 문자 개수세기(count)
```python
a = 'hobby'
a.count('b')
👉🏽 2
```

---

### 📍 위치 알려주기(find, index)
`find`함수는 문자열 처음 나온 위치를 반환한다.
만약, 값이 없으면 -1을 반환함

`index`함수는 find함수와 동일하지만
만약, 값이 없으면 오류를 발생시킨다.
```python
a = 'My Name is AYW'
a.find('Z')
a.index('Z')
👉🏽 -1 error
```
---

### 📍 문자열 삽입(join)
abcd문자열의 각각의 문자 사이에 변수 a의 값인 ','를 삽입한다.
```python
a = ','
a.join('abcd')
👉🏽 a,b,c,d
```
---

### 📍 공백지우기(strip)
>1. 왼쪽공백: lstrip()
>2. 오른쪽공백: rstrip()
>3. 양쪽공백: strip()

```python
a = ' hi '
a.lstrip()
a.rstrip()
a.strip()
```
---

### 📍 문자열 나누기(split)
괄호 안에 아무것도 넣지 않으면 공백을 기준으로 나눈다.
특정한 값이 있으면 구분자로 문자열을 나눈다.

```python
a = ' hey '
a.split()
```
---