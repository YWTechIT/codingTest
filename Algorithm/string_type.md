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
# 1번째 풀이
s = input().lower()

dial = ['abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
time = 0

for i in range(len(s)):
    for j in range(len(dial)):
        if s[i] in dial[j]:
            time += j+3
print(time)

# 2번째 풀이
s = input()
dial = ['', '', 'ABC', 'DEF', 'GHI', 'JKL', 'MNO', 'PQRS', 'TUV', 'WXYZ']
cnt = 0

for i in range(len(s)):
    for j in range(len(dial)):
        if s[i] in dial[j]:
            cnt += j+1
print(cnt)

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

### 📍 [ 문제 7 ] 백준 1157 - 단어 공부
<a href='https://www.acmicpc.net/problem/1157'>백준 1157 - 단어 공부</a>

### 💡 나의 풀이
언젠가 이 문제를 보고 풀 엄두가 나지 않아서 북마크로 추가만 했었는데, 오늘 다시보니까 풀 수 있었다.
약간 까다로운 문제인데 `count`, `index` 함수를 사용하면 금방 풀 수 있었다.

먼저 `for`문을 풀어서 작성하고 이후에 `list_comprehension`으로 코드를 단축시켰다.

이해하기 쉽도록 예제 입력에 나와있는 `Mississipi`를 기준으로 알아보자.
>1. 입력을 대문자 or 소문자로 통일 시킨다. (이후에 set으로 변환하기 위함.)
>2. 입력을 `set`으로 형 변환을 시켜 중복을 제거한다.
>3. set형으로 for문을 돌려 입력에 i값이 몇 번 쓰였는지 확인하고 빈 리스트에 append시킨다.
>4. count_list = [1, 4, 1, 4]가 나오게 되는데 이는 `compress_s = ['S', 'P', 'I', 'M']`가 몇 번 사용됐는지 `count`한 값이다.
>5. 조건문을 통해 만약, `[1, 4, 1, 4]`의 `count(max_index)` 즉, max값이 2개 이상(max값이 2개면 가장 많이 사용된 알파벳의 갯수가 동일하다는 얘기다.)이면 `?`를 출력하고
>6. 그렇지 않으면, `count_list.index(max(count_list))` 즉, `count_list` 중 `count`가 가장 많이 선언된 `index`의 위치를 반환하고 그 값을 `count_list[index]`에 넣어주면 어떤 값이 가장 많이 쓰였는지 알 수 있다.
이때, `compress_s`는 `list`로 변경해야 `index`를 대입 할 수 있다.
>7. 6번의 과정을 하나씩 살펴보기 전에 먼저, `set`은 순서가 정해져있지 않기때문에 결과값이 바뀔 수도 있다.
>8. `print(count_list.index(max(count_list)))` = 1이고, `compress_s[1]`과 같다.
>9. `compress_s = ['A', 'B']` 따라서, `compress_s[1] = B`이다.

조금 복잡하지만 구현 과정을 천천히 손으로 써내려가면 금방 이해 할 수 있다.

```python
s = input().upper()
compress_s = list(set(s))
count_list = [s.count(i) for i in compress_s]

if count_list.count(max(count_list)) > 1:
    print('?')
else:
    print(compress_s[count_list.index(max(count_list))])
```

---
### 📍 [ 문제 8 ] 백준 10798 - 세로 읽기
<a href='https://www.acmicpc.net/problem/10798'>백준 1157 - 세로 읽기</a>

### 💡 나의 풀이
첫번째 조건은 잘 풀었는데 두번째 조건은 고민하는 시간이 오래 걸렸다.

주어진 리스트에서 세로로 읽으려면 2중 for문이 선언되어야한다.
만약, 입력이 빈칸없이 연속으로 주어진다면 단순하게 구할 수 있지만 입력에 빈칸이 존재한다면 조건문을 붙여줘야한다.

해결방법의 흐름은 크게 2가지가 있다.

먼저, 입력이 `n줄`로 한정되어있다면 반복문을 `n`으로 변경하면 되지만, 입력이 몇 줄이라고 주어지지 않을때는 `max(len)`을 구해야한다.

그리고, `max(len)`의 i가 j보다 크거나 같다면 `continue`를 사용해 상위 코드로 올라가서 건너뛰고 그렇지 않다면 값을 출력해주면 된다.

```python
'''
ABCDE
abcde
01234
FGHIJ
fghij

AABCDD
afzz
09121
a8EWg6
P5h3kx
'''
s = [input() for i in range(5)]
max_length = 0

if len(s) > max_length:
    max_length = len(s)

# 방법 1
for i in range(max_length):
    for j in range(len(s)):
        if i >= len(s[j]):
            continue
        else:
            print(s[j][i], end='')

# 방법 2
for i in range(max_length):
    for j in s:
        if i >= len(j):
            print(j[i], end='')

👉🏽 Aa0FfBb1GgCc2HhDd3IiEe4Jj
👉🏽 Aa0aPAf985Bz1EhCz2W3D1gk
```

