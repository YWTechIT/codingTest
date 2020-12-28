## bisect_function
1. bisect(): `정렬된 배열`에서 특정한 원소를 찾을 때 주로 사용하고 `배열 위치`를 반환한다.
  * bisect_left: 정렬된 순서를 유지하면서 리스트 `a`에 데이터 `x`를 삽입할 가장 왼쪽 인덱스를 찾는 method
  * bisect_right: 정렬된 순서를 유지하면서 리스트 `a`에 데이터 `x`를 삽입할 가장 오른쪽 인덱스를 찾는 method


예를 들어, 정렬된 리스트 `[1, 2, 4, 4, 8]`이 있을 때, 새롭게 데이터 `4`를 대입한다고 가정하면
`bisect_left(a, 4)`는 2가 될 것이고, 
`bisect_right(a, 4)`는 
```python
from bisect import bisect_left, bisect_right

# 특정한 원소의 배열 위치 
a = [1, 2, 4, 4, 8]
print(bisect_left(a, 2))
👉🏽 2
print(bisect_right(a, 4))
👉🏽 4

# 값이 특정 범위에 속하는 원소의 개수
def count_by_range[a, left_value, right_value]:
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

a = [ 1, 2, 3, 3, 3, 3, 4, 4, 8, 9]
print(count_by_range(a, 4, 4))
👉🏽 2

print(count_by_range(a, 3, 3))
👉🏽 4

# 0 ~ 9 범위의 데이터 개수
print(count_by_range(a, 1, 9))
👉🏽 10
```