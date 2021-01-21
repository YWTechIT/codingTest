## sorted() vs sort()
### 📍 sorted()
>1. 내장함수로 기존의 리스트를 변경하는 것이 아니라 정렬된 새로운 리스트를 반환한다.
   * 이때, 원본 리스트 값은 유지함
>2. 어떤 `iterable` 객체도 받을 수 있다.(tuple, dictionary ...)

---

### 📍 sort()
>1. 리스트만을 받을 수 있다.(리스트형의 메소드)
>2. 원본 자체의 배열도 바꾼다.

레퍼런스: https://docs.python.org/ko/3/howto/sorting.html

---

## 백준 2750
<a href='https://www.acmicpc.net/problem/2178'>문제</a>

`N의 범위가 (1 <= N <= 1,000,000)`일때는 input 대신 `sys.stdin.readline()`을 사용하자.

```python
import sys

n = int(input())

array = []

for i in range(n):
    array.append(int(sys.stdin.readline()))

array = sorted(array)

for i in array:
    print(i)
```

---

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

---

## [ 문제 ] - up_to_down
다음 수를 큰 수부터 작은수로 나열하는 내림차순 프로그램을 만드시오.
>1. 선택 정렬
>2. 삽입 정렬
>3. 퀵 정렬
>4. 계수 정렬

```python
# 선택 정렬
import sys

n = int(input())

array = []
result = []
for i in range(n):
    array.append(int(sys.stdin.readline().rstrip()))

for i in range(len(array)):
    min_index = i
    for j in range(i+1, len(array)):
        if array[min_index] > array[j]:
            min_index = j
    array[i], array[min_index] = array[min_index], array[i]

result.reverse()

print(result)
👉🏽 입력: f'3\n15\n27\n12\n'
👉🏽 출력: 27 15 12
```

```python
# 삽입 정렬
import sys

n = int(input())

array = []
result = []
for i in range(n):
    array.append(int(sys.stdin.readline().rstrip()))

for i in range(1, len(array)):
    for j in range(i, 0, -1):
        if array[j] < array[j-1]:
            array[j], array[j-1] = array[j-1], array[j]

array.reverse()

print(array)
👉🏽 입력: f'3\n15\n27\n12\n'
👉🏽 출력: 27 15 12
```

```python
# 퀵 정렬
import sys

n = int(input())

array = []
result = []
for i in range(n):
    array.append(int(sys.stdin.readline().rstrip()))

def quick_sort(array):
    if len(array) <= 1:
        return array
    pivot = array[0]
    tail = array[1:]

    left = [x for x in tail if x <= pivot]
    right = [x for x in tail if x > pivot]

    return quick_sort(left) + [pivot] + quick_sort(right)

result = quick_sort(array)
result.reverse()

print(result)
👉🏽 입력: f'3\n15\n27\n12\n'
👉🏽 출력: 27 15 12
```

```python
# 계수 정렬
import sys

n = int(input())

array = []
result = []
for i in range(n):
    array.append(int(sys.stdin.readline().rstrip()))

count = [0] * (max(array) + 1)

for i in range(len(array)):
    count[array[i]] = count[array[i]] + 1

for i in range(len(count)):
    for j in range(count[i]):
        result.append(i)

result.reverse()

print(result)
👉🏽 입력: f'3\n15\n27\n12\n'
👉🏽 출력: 27 15 12
```

---

### 📍 [ 문제 2 ] low_score
N명의 학생 정보가 있다. 학생 정보는 학생의 이름과 학생의 성적으로 구분된다. 각 학생의 이름과 성적 정보가 주어졌을 때, 성적이 낮은 순서대로 학생의 이름을 출력하는 프로그램을 작성하시오.

```python
n = int(input())

array = []

for i in range(n):
    input_data = input().split()
    array.append((input_data[0]), (int(input_data[1])))

array = sorted(array, key = lambda student: student[1])

for student in array:
    print(student[1], end=' ')

👉🏽 입력
3
홍길동 95
이순신 77

출력
이순신 홍길동
```

---

다음은 지금까지 다뤘던 정렬 알고리즘을 비교한 표이다.

| 정렬 알고리즘 | 평균 시간 복잡도 | 최악의 시간 복잡도 | 공간 복잡도 | 특징 |
| :----: | :------: | :------: | :------: | :------: |
| 선택 정렬 | O(N^2) | O(N^2) | O(N) | 아이디어가 매우 간단합니다. |
| 삽입 정렬 | O(N^2) | O(N^2) | O(N) | 데이터가 거의 정렬되어 있을 때는 가장 빠르다. |
| 퀵 정렬 | O(NlogN) | O(N^2) | O(N) | 대부분의 경우에 가장 적합하고, 충분히 빠르다. |
| 계수 정렬 | O(N+K) | O(N+K) | K값에 따라 다름 | 사용조건을 만족하면 매우 빠르게 동작한다.  |


추가적으로 대부분의 프로그래밍 언어에서 지원하는 표준 정렬 라이브러리는 최악의 경우에도 `O(NlogN)`을 보장하도록 설계되어 있다.
파이썬은 정확히 병합정렬과 삽입 정렬의 아이디어를 더한 하이브리드 방식의 정렬 알고리즘을 사용하고 있다. 

>문제에서 별도의 요구가 없고 단순히 정렬하는 상황에서는 기본 라이브러리를 사용하고, 데이터의 범위가 한정되어있고 더 빠르게 동작해야하는 상황에는 계수 정렬을 사용하자.


