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
