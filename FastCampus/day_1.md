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


---

## 📍 string, operator