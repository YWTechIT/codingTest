## 백준 2750
<a href='https://www.acmicpc.net/problem/2178'>문제</a>

>1. `sort()`
>2. `선택정렬(selection_sort)`
>3. `삽입정렬(insertion_sort)`

```python
# sort()
n = int(input())

array = []

for i in range(n):
    array.append(int(input()))

# 중복제거
array = sorted(set(array))

for i in array:
    print(i)
👉🏽 입력
5
5
2
3
4
1

👉🏽 출력
1
2
3
4
5
```
 
 ---

```python
# 선택정렬(selection_sort)
n = int(input())

array = []

for i in range(n):
    array.append(int(input()))

for i in range(len(array)):
    min_index = i
    for j in range(i+1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i]

for i in array:
    print(i)
👉🏽 입력
5
5
2
3
4
1

👉🏽 출력
1
2
3
4
5
```
---
```python
# 삽입정렬(insertion_sort)
n = int(input())

array = []

for i in range(n):
    array.append(int(input()))

for i in range(len(array)):
    for j in range(i, 0, -1):
        if array[j] < array[j-1]:
            array[j], array[j-1] = array[j-1], array[j]
        else:
            break

for i in array:
    print(i)

👉🏽 입력
5
5
2
3
4
1

👉🏽 출력
1
2
3
4
5
```
