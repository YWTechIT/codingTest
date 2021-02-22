## 📍 print
>1. sep
```python
print('abcd8637', 'naver.com', sep='@')
print('2021', '2', '21', sep='.')
👉🏽 abcd8637@naver.com
2021.2.21
```
---

>2. end
```python
print('%s' %('My name is'), end=' ')
print('%s' %('Yeongwoo An'), end=' ')
print('%s' %("What's your name?"))
print('%s' %("What's your name?"))
👉🏽 My name is Yeongwoo An What's your name?
```
---

>3. format
```python
print('영우의 성적 - test1: %5d, test2:  %5.2f' %(100, 100.00000))
print('영우의 성적 - test1: {0: 5d}, test2: {1: 5.2f}'.format(100, 100.00000))
print('영우의 성적 - test1: {a: 5d}, test2: {b: 5.2f}'.format(a=100, b=100.00000))

print('영우의 축구 - number: %d, name: %s' %(7, 'AYW'))
print('영우의 축구 - number: {0}, name: {1}'.format(7, 'AYW'))
print('영우의 축구 - number: {a}, name: {b}'.format(a=7, b='AYW'))
👉🏽 
영우의 성적 - test1:   100, test2:  100.00
영우의 성적 - test1:   100, test2:  100.00
영우의 성적 - test1:   100, test2:  100.00

영우의 축구 - number: 7, name: AYW
영우의 축구 - number: 7, name: AYW
영우의 축구 - number: 7, name: AYW
```
---

>4. escape
```python
print('yw\'s favorite color is orange')
print("''her say\"s favorite number is 7")
print('''
hello
my name is
ayw''')
print('\'\\t\' == 스페이스 4. ')
print('\t 이런식으로 사용합니다.')
print('     지금은 스페이스 4번을 쳤지여.')
👉🏽
yw's favorite color is orange
she say"s favorite number is 7
hello
my name is
ayw
```

### 💡 Escape_code
'\' 뒤에 문자는 그대로 보여준다.
/n: 개행
/t: 탭
\\: 문자
\': 문자
\": 문자
\r: 캐리지 리턴
\f: 폼 피드
\a: 벨 소리
\b: 백 스페이스
\000: 널 문자

---

## 📍 data_type
data_type은 다음과 같이 선언 할 수 있다.

>1. Boolean: True = 1, False = 0
>2. Numbers: 숫자형
>3. String: 문자형
>4. byte(바이너리 데이터를 처리할 때 사용): bytes(10), bytes([10, 20, 30, 40])
>5. List: [1, 2, 3, 4]
>6. Tuples: (1, 2, 3)
>7. Sets(집합): {1, 2, 3}
>8. Dictionary: {"name": "AYW", "age": 27}

### 💡 숫자형(Number)
숫자들이 이루어진 형태
>1. 정수형(int): 1, 2, 3 ...
>2. 실수형(float): 1.0, 2.0, 3.0 ...
>3. 복소수형(Complex): 1+2j, 1+3j ...

### 💡 사칙연산
>1. 더하기: +
>2. 빼기: -
>3. 곱하기: *
>4. 나누기: /
>5. 나눈 몫: //
>6. 나머지: %
>7. 제곱: **
>8. 단항연산자: y=100, y+=100, y*=100

### 💡 수치연산함수
>1. abs: 절대값
>2. divmod: 두 수를 나눈 몫과 나머지를 저장한다.
  * n, m = divmod(25, 5)
>3. math.ceil: 해당 값보다 큰 최소 정수 반환
>4. math.floor: 해당 값보다 작은 최대 정수 반환

---

## 📍 string, operator
문자열 생성, 연산, 슬라이싱을 알아보자

---

### 💡 문자열 생성
>1. len: 문자열의 size반환 (1부터 시작)
>2. escape: 'hi what\\'s your name?', 'Tap\tTap\tTap\t'
>3. Raw String: escape 영향받지 않고 있는 그대로 출력
>4. multiline: string을 길게 작성할 때

```python
str1 = 'I love you.'
str2 = 'hello'
str3 = ' '
str4 = str('ace')

print(len(str1), len(str2), len(str3), len(str4))

escape_str1 = 'Do you have a \'big collection?\''
escape_str2 = 'Tap\tTab\tTab'

# Raw String
raw_s1 = r'C:\Programs\Test\Bin'
👉🏽 C:\Programs\Test\Bin
raw_s2 = r"\\a\\a\t"
👉🏽 \\a\\a\t

# multiline
multi = \
''' 
내 이름은
영우
입니다.
'''
👉🏽 내 이름은
영우
입니다. 
```

---

### 💡 문자열 연산
문자열끼리 연산이 가능하다.

```python
# 문자열 연산
str_01 = '*'
str_02 = 'abc '
str_03 = 'def'
str_04 = 'Niceman'

print(str_01 * 100)
print(str_02 + str_03)
print('a' in str_04)
👉🏽 True
print('z' in str_04)
👉🏽 False
print('z' not in str_04)
👉🏽 True
print('z' in str_04)
👉🏽 False
```

---

### 💡 문자열 함수
```python
a = 'niceman'
b = 'orange'

print(a.islower())
👉🏽 True
print(b.endswith('e'))
👉🏽 True
print(a.capitalize())
👉🏽 Niceman
print(a.replace('nice', 'good'))
👉🏽 goodman
print(list(reversed(b)))
👉🏽 ['e', 'g', 'n', 'a', 'r', 'o']
```

---

### 💡 문자열 슬라이싱
여러 글자를 뽑아내는 방식
```python
a = 'niceman'
b = 'orange'
c = 'strawberry'
d = 'water'
print(a[0:4])
print(a[0:len(a)-1])
print(a[:])
👉🏽 niceman
print(b[0:4:2])
👉🏽 oa
print(b[0:4])
print(b[1:-2])
👉🏽 ran
print(b[::-1])
👉🏽 egnaro
```
---