## 정규표현식(regular_expression)
정규표현식은 특정한 규칙을 가진 문자열의 집합을 표시하는 형식 언어이다.
복잡한 문자열의 검색과 치환을 위해 사용되며, `python` 뿐만아니라 문자열을 처리하는 모든 곳에서 사용된다.

1. `\w`: word, 문자[a-z, A-Z] + 숫자[0-9]
2. `\W`: not word, 특수기호[.[]{}()\^&|?*+] + 공백[' '] + 한글
3. `/s`: space, 공백[' ']
4. `/S`: not space, 문자[a-z, A-Z] + 숫자[0-9] + 특수기호[.[]{}()\^&|?*+] + 한글

`reList = re.sub('(\w{%i})' %i, '\g<1> ', string).split()`

>1. string 변수를 `'(\w{%i})' %i`을 거쳐 `'\g<1> '`으로 처리한다.
  * for문을 돌기때문에 i는 1부터 `len(string) // 2 + 1`까지 증가함.
>2. `\w(word)`: 숫자와 문자를 합친 모든범위`([a-zA-Z0-9])`, 특수기호 제외
>3. `/g<1>`: 1개의 그룹으로 묶는다.
>4. 띄워쓰기를 기준으로 `[list]`에 담아준다. (미 사용시 string 반환)

* `\s`: 공백`[\t\n\r\f\v]`
* `+`: 앞에 있는 문자가 최소 한번 이상 반복되어야 매치

<a href='https://nachwon.github.io/regular-expressions/'>관련 문법</a>

---

## 📍 1. string 문자단위로 쪼개기
```python
import re

string = 'aabbaccc'

for i in range(1, len(string) // 2 + 1):
    reList = re.sub('(\w{%i})' %i, '\g<1> ', string).split()
    print(reList)

👉🏽['a', 'a', 'b', 'b', 'a', 'c', 'c', 'c']
['aa', 'bb', 'ac', 'cc']
['aab', 'bac', 'cc']
['aabb', 'accc']
```

---
## 📍 2. 주어진 문자열에서 공백 없애기

```python
import re
s = 'abc Def gh'
s = re.sub('\s', '', s)
s = re.sub('\W', '', s)
👉🏽 abcDefgh
```