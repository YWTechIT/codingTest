## implementation(구현)
머릿속으로는 잘 떠오르지만 막상 코드로 작성하면 잘 떠오르지 않는 문제들

## 📍 list를 str로 변환하기
```python
array = ''.join([str(_) for _ in range(10)])
char = ''.join([chr(i) for i in range(65, 71)])

👉🏽 '0123456789'
'ABCDEF'

```

---

## 📍 pass, continue, break
```python
# pass
for i in range(10):
    if i % 2 == 0:
        pass
        print(i)
    else:
        print('나머지')
👉🏽 0
나머지입니다.
2
나머지입니다.
4

# continue
for i in range(5):
    if i % 2 == 0:
        continue
        print(i)
    else:
        print('나머지')
👉🏽 나머지입니다.
나머지입니다.

# break
for i in range(5):
    if i % 2 == 0:
        break
        print(i)
    else:
        print('나머지')
👉🏽 빈 화면
``` 
> 1. pass: 조건문에서 넣어줄 조건이 딱히 없을경우
> 2. continue: 해당 조건을 건너 뜀
> 3. break: 해당 반복문 자체를 멈춤

---

## 📍 n의 배수일 때, 배수가 아닐 때

```python
# n이 4의 배수로 나누어 떨어질 때
n = 12

if n % 4 == 0 
    print('4의 배수입니다.')
elif n % 4 != 0:
    print('4의 배수가 아닙니다.')
```
---

## 📍 입력마다 최대값을 갱신할 때
```python

max_index = 0
index = 0

for i in range(1, 10):
    number = int(input())
    if number > max_index:
        max_index = number
        index = i
print(max_index)
print(index)
👉🏽 85
8
```
---

## 📍 리스트 내부 인덱스에 접근하기
```python
array = [1, 2, 3, 4, 5]
print(array.index(2))
👉🏽 3
```
---

## 📍 리스트컴프리헨션을 이용한 i제곱
```python
import sys
sys.stdin.readline
array = [i*i map(int, input().split())]
print(sum(array)%10)
```
---

## 📍 중복되는 문자열 정렬
```python
# 만약, list(array)와 중복된 단어를 정렬한 array와 같다면 count+=1
n = int(input())
for i in range(n):
    array = input()
    if list(array) = array.sorted(array, key=array.find):
        count+=1
```
---

## 📍 array[i] == array[i+1] 범위 설정
```python
# 1번
for i in range(len(array)):
    if i < len(array) -1 and array[i] == array[i+1]:

# 2번
for i in range(len(array)):
    if i != len(array) -1 and array[i] == array[i+1]:
```
---

## 📍 이중반복문 내부 숫자배열
반복문 1개당 시간복잡도: O(N)

```python
array = 'scv'
for i in range(3):
    for j in range(len(array)):
        print(i)
👉🏽 0 0 0 1 1 1 2 2 2 (s s s c c c v v v)

for i in range(3):
    for j in range(len(array)):
        print(j)
👉🏽 0 1 2 0 1 2 0 1 2 (s c v s c v s c v)
```

---

## 📍 백준 1152 - 단어의 개수
주어진 문자열에서 단어의 개수를 찾고 싶을 때는 띄어쓰기를 기준으로 나누고 + 1을 해주면된다.

예외상황으로 문자열의 제일 앞, 뒤는 `strip()` 함수를 사용해서 공백을 제거해준다.

그리고, `input=' '` 공백일때를 고려해서 공백이라면 print(0) 아니면 `cnt+=1`을 하는 코드를 작성했다.

```python
array = input().strip()

if len(array) == 0:
    print(0)
else:
    print(array.count(' ')+1)
```

---

## 📍 백준 2675 - 문자열 반복
시간복잡도를 최소화하기 위해 반복문도 최소화선언
```python
# 1번
T = int(input())

for i in range(T):
    case = input().split()
    n, s = int(case[0]), list(case[1])
    for j in range(len(s)):
        for k in range(n):
            print(s[j], end='')
    print()

# 2번 
T = int(input())

for i in range(T):
    n, s = input().split()
    for j in range(len(s)):
        print(int(n) * s[j], end='')
    print()

```

---



