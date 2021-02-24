## 📍 조건문

### ⚡️ 참 거짓 종류
```python
# 참 
True: '내용', [내용], (내용), {내용}, 1, True

# 거짓
False: '', [], (), {}, 0, False
```
> 1. 관계, 논리연산자
> 우선순위: 산술(사칙연산) > 관계(부호) > 논리(and, not, or)

```python
# >, >=, <, <=, ==, !=
a = 100
b = 50
c = 0

print(a > b and b < c)
👉🏽 False
print(a > b or b < c)
👉🏽 True
print(not False)
👉🏽 True
print(not True)
👉🏽 False
print(not a > b)
👉🏽 False

# 우선순위: 산술 > 관계 > 논리
print( 10+5 > 0 and not 7+3 == 10)
👉🏽 False
```

> 2. 다중조건문
```python
score = 90
if score >= 90:
    print('A', score)
elif score >= 80:
    print('B', score)
elif score >= 70:
    print('C', score) 
else:
    print('불합격', score)

```

> 3. 중첩조건문
```python
age = 27
height = 170

if age >= 20:
    if height >= 180:
        print('A지망')
    elif height >= 170:
        print('B지망')
    else:
        print('지원 불가')
else:
    print('나이자격 미달로 인한 불가')
```

---
## 📍 반복문

1. for
```python
# 홀수만 출력
for i in range(1, 10, 2):
    print(i)
 👉🏽 1 3 5 7 9

# 1부터 100까지의 합을 구하시오.
result = 0
for i in range(1, 101):
    result += i
print(result)
```
`print(sum(range(1, 100)))`으로 작성해도 된다.

2. while
```python
# 1부터 100까지의 합을 구하시오.
sum1 = 0
cnt = 1
while cnt <= 100:
    sum1 +=1 cnt
    cnt +=1
print(sum1)
```


3. 시퀀스 타입반복

> 반복가능한 자료형: str, list, tuple, dict, set
> iterable 리턴 함수: range, reversed, enumerate, filter, map, zip...

`print(list(reversed(name)))`

```python
# string 반복
names = 'names'
for i in names:
    print(i, end=' ')
👉🏽 n a m e s

# list 반복
names = ['An', 'Jung', 'Lee']
for i in names:
    print(i, end=' ')
👉🏽 An Jung Lee

# tuple 반복
names = ('An', 'Jung', 'Lee')
for i in names:
    print(i, end=' ')
👉🏽 An Jung Lee

# dictionary 반복, for문의 기본 값은 key이다. 
info = {
    'name': 'AYW',
    'age': 27,
    'sex': 'male'
}

# key
for i in info:
    print(i, end=' ')
👉🏽 name age sex

for i in info.keys():
    print(i, end=' ')
👉🏽 name age sex

# value
for i in info.value():
    print(i, end=' ')
👉🏽 AYW 27 male

# items
for i in info.items():
    print(i, end=' ')
👉🏽 ('name', 'AYW') ('age', 27) ('sex', 'male') 

# key, value
for key, value in info.items():
    print(key, end=' ')
    print(value)
👉🏽
name AYW
age 27
sex male

# enumerate
for key, value in enumerate(info):
    print(key, end=' ')
    print(value)
👉🏽
0 name
1 age
2 sex
```

```python
# 예제, 문자열 중 소문자는 대문자로, 대문자는 소문자로 만드는 코드를 작성하라.
name = 'reBanDoFSKy'

for i in name:
    if i == i.upper():
        print(i.lower())
    else:
        print(i.upper())
```

>4. break, continue
break: 중간에 조건이 맞으면 반복문을 탈출함, break를 넣어주지 않으면 반복문을 끝까지 실행한다.

```python
# 예제 1
number = [1, 10, 9, 11, 88, 35]
for i in number:
    if i == 88:
        print(i)
        break
    else:
        print('not found')
```

continue: 키워드를 만나면 문장을 실행하지않고 조건(위)으로 다시 올라감

```python
# 조건에 맞는 값 이외의 값을 보여주고 싶을 때, 다음 순회 할 값으로 이동한다. 조건이 맞으면 하위부분으로 내려가지 않음
lt = [True, 1, (3,), 4.1, [1,2,3]]

for i in lt:
    if type(i) is float:
        continue
    print(type(i))
👉🏽
<class 'str'>
<class 'int'>
<class 'int'>
<class 'bool'>
<class 'complex'>
        
```

>5. for - else 구문(반복문이 정상적으로 수행 된 경우 else 수행)
```python
numbers = [14, 3, 4, 7, 10, 24, 17, 2, 33, 15, 34, 36, 38]

for num in numbers:
    if num == 331:
        print('숫자를 찾앗다.')
        break
    else:
        print(num)
else:
    print("Not fond 33...")
```

