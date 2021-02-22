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

### 📍 [ 문제 1 ] 백준 1546 - 평균
<a href='https://www.acmicpc.net/problem/1546'>백준 1546 - 평균</a>

### 💡 나의 풀이
어렵지 않게 풀 수 있었던 문제였다.
마지막에 `float`를 붙여야하는줄 알았는데, 붙이지 않아도 소수점까지 출력됐다.

```python
'''
3
40 80 60
'''

N = int(input())
score = list(map(int, input().split()))
M = max(score)

sum = 0
for i in score:
    result = (i/M) * 100
    sum+=result
print(sum/len(score))
👉🏽 75.0
```

---
### 📍 [ 문제 2 ] 백준 2908 - 상수
<a href='https://www.acmicpc.net/problem/2908'>백준 2908 - 상수</a>

### 💡 나의 풀이
`str`형을 거꾸로 뒤집을때는 문자열 슬라이싱을 통해 간단하게 구현 할 수 있다.
`[::-1]`을 붙여주면 된다.

```python
s1, s2 = input().split()
print(s1[::-1]) if s1[::-1] > s2[::-1] else print(s2[::-1])
```
---

### 📍 [ 문제 3 ] 백준 10809 - 알파벳 찾기
<a href='https://www.acmicpc.net/problem/10809'>백준 10809 - 알파벳 찾기</a>

### 💡 나의 풀이
`find` 함수의 특징은 찾는 값이 있을때는 처음 나온 위치를 반환해주고, 그렇지 않으면 -1을 반환한다.
그래서 알파벳 소문자를 모아둔 변수(character)를 선언해서 for문으로 하나씩 꺼내주고, find함수를 적용했다.
또, 예제 출력에 -1이 많이 쓰인것으로 보아 `find`함수를 사용해야겠다고 생각했다.

```python
s = input()
character = 'abcdefghijklmnopqrstuvwxyz'

for i in character:
    print(s.find(i), end=' ')
```

---

### 📍 [ 문제 4 ] 백준 10039 - 평균 점수
<a href='https://www.acmicpc.net/problem/10039'>백준 10039 - 평균 점수</a>

### 💡 나의 풀이
`score`가 40점 이하라면 40점으로 변경하고 나머지는 빈 리스트인 `result`에 `append`하고 이후에 평균을 구했다.
이렇게 작성하면 답이 68.0이 나오는데 예제 출력이 정수값이므로 int()를 붙여주었다.

```python
result = []
for i in range(5):
    score = int(input())
    if score < 40:
        score = 40
    result.append(score)
print(int(sum(result) / 5))
```
---

### 📍 [ 문제 5 ] 백준 5622 - 다이얼
<a href='https://www.acmicpc.net/problem/5622'>백준 5622 - 다이얼</a>

### 💡 나의 풀이
이 문제는 고민하는 시간이 길었다.
그림에 나와있는것처럼 숫자마다 알파벳 값이 정해져있는데, 어떻게 한번에 선언해야되지? 라는 생각을 했다.
처음에 `one = 'abc'`, `two = 'def'`, `one = 'ghi'` 이런식으로 선언했다가 아무리봐도 아닌것 같아서 그만두었다.
결론적으로 빈 리스트에 선언하면 되는 간단한 문제였다.

그리고 `time += j+3`을 해준이유는 `index`가 증가할 때마다 `time`도 `+2`씩 증가하게 되는데, `list`는 0부터 세기 때문에 +1을 더 해주었다.

이렇게 했는데도 답이 안나와서 당황했었다. 
예제입력은 대문자인데, 내가 작성한 `dial`은 소문자였기 때문이다. (파이참이 고장난 줄 알았다. 😅 😅 ~~컴퓨터는 진실만을 말한다.~~)
대문자면 대문자로, 소문자면 소문자로 맞춰주자.

```python
s = input().lower()

dial = ['abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
time = 0

for i in range(len(s)):
    for j in range(len(dial)):
        if s[i] in dial[j]:
            time += j+3
print(time)
```
---

### 📍 [ 문제 6 ] 백준 2941 - 크로아티아 알파벳
<a href='https://www.acmicpc.net/problem/2941'>백준 2941 - 크로아티아 알파벳</a>

### 💡 나의 풀이
개인적으로 난이도가 있었던 문제라고 생각했다.
단순하게 생각했어야 하는데 그러지 못해 시간을 길게 끌었다.
답을 보니 생각보다 너무 간단해서 당황했다.

`croatia`에서 입력값이 있는지 확인하고 있으면 `cnt+=1`까지는 좋았는데, 없는경우 처리를 잘 못했다.
답은 간단했다. 입력값이 존재하면 `replace`를 사용해 한 글자로 바꾸고 총 길이(len)를 구하면 됐는데
왜 이렇게 어렵게만 풀려고 했는지..
이런 기발한 생각은 어떻게 해야하는지 궁금하다.

```python
s = input()
cnt = 0
croatia = ['c=', 'c-', 'dz=', 'd-', 'lj', 'nj', 's=', 'z=']

for i in croatia:
    s = s.replace(i, '*')

print(len(s))
```

