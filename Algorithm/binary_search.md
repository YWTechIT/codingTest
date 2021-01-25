## binary_search(이진탐색)
> 1. 찾으려는 데이터와 중간점(Middle) 위치에 있는 데이터를 반복적으로 비교해서 찾는 과정`(quick_sort와 비슷)`
> 2. 데이터가 무작위 일때는 사용할 수 없고, `정렬(sort)`이 되어있어야만 사용이 가능함
> 3. 탐색 범위를 절반씩 좁혀가며 데이터를 탐색함
> 4. 시간복잡도는 `O(logN)`
> 5. 재귀함수를 호출하는 방법, 반복문을 돌리는 방법 2가지가 있음
> 6. 이진탐색에서 `target`에 `for`문을 넣어 확인하는데, 비교 연산자는 `list`와 `int`를 동시에 사용 할 수 없기때문이다.


```python
# 재귀함수 호출
'''
10 7
1 3 5 7 9 11 13 15 17 19
'''
def binary_search_recursive(array, target, start, end):
    if start > end:
        return None

    mid = (start + end) // 2

    if array[mid] == target:
        return mid
    elif array[mid] > target:
        return binary_search_recursive(array, target, start, mid-1)
    else:
        return binary_search_recursive(array, target, mid+1, end)

n, target = list(map(int, input().split()))
array = list(map(int, input().split()))
result = binary_search_recursive(array, target, 0, n-1)

if result == None:
    print('찾는 값이 없습니다.')
else:
    print(result + 1)

👉🏽 출력
4
```

```python
# for문
'''
10 7
1 3 5 7 9 11 13 15 17 19
'''
def binary_search_recursive(array, target, start, end):
    while start <= end:
        mid = (start + end) // 2

        if array[mid] == target:
            return mid
        elif array[mid] > target:
            return end = mid - 1
        else:
            return start = mid + 1
    return None

n, target = list(map(int, input().split()))
array = list(map(int, input().split()))
result = binary_search_recursive(array, target, 0, n-1)

if result == None:
    print('찾는 값이 없습니다.')
else:
    print(result + 1)

👉🏽 출력
4
```

## bisect_range(이진탐색)
> bisect_left(a,x): 정렬된 순서를 유지하면서 배열 a에 x를 삽입 할 가장 왼쪽 인덱스를 반환
> bisect_right(a,x): 정렬된 순서를 유지하면서 배열 a에 x를 삽입 할 가장 오른쪽 인덱스를 반환


```python
# 값이 특정 범위에 속하는 데이터의 개수 구하기
from bisect import bisect_left, bisect_right

def count_range(array, left_value, right_value):
    right_index = bisect_right(array, right_value)
    left_index = bisect_left(array, left_value)
    return right_index - left_index

array = [1, 2, 3, 3, 3, 3, 4, 4, 8, 9]

print(count_range(array, 4, 4))
print(count_range(array, -1, 3))
👉🏽 2 6
```

```python
# 이진탐색에서의 계수정렬
'''
5
8 3 7 9 2
3
5 7 9
'''
# array는 최대값 + 1
# 전체 부품 번호를 입력받아 자리수에 1을 넣어줌
# 전체 부품의 자리와 `target`의 자리를 비교해 출력
import sys

n = int(input())
array = [0] * 1000001

for i in input().split():
    array[int(i)] = 1

m = int(input())
target = list(map(int, sys.stdin.readline().split()))

for i in target:
    if array[i] == 1:
        print('yes', end=' ')
    else:
        print('no', end=' ')

👉🏽 no yes yes 
```

```python
# set 자료형을 통한 이진탐색
import sys

n = int(input())
array = set(map(int, sys.stdin.readline().split()))

m = int(input())
target = list(map(int, sys.stdin.readline().split()))

for i in target:
    if i in array:
        print('yes')
    else:
        print('no')
👉🏽 no yes yes 
```
