## quick_sort(퀵 정렬)
지금까지 배운 정렬 알고리즘 중 가장 많이 사용하는 알고리즘이다. `병합 정렬`만큼이나 많이 쓰인다.

> 기준 데이터를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 정렬

3가지 풀이방법이 있는데, 나에겐 2번째 방법이 잘 맞았다.

```python
# 1번째
array = [5, 7, 9, 0, 3, 1, 6, 2 ,4, 8]

def quick_sort(array, start, end):
    if len(array) <= 1:
        return array

    pivot = start
    left = start + 1
    right = end

    while left <= right:
        while left <= end and array[left] <= array[pivot]:
            left = left + 1
        while right > start and array[right] >= array[pivot]:
            right = right - 1
        if left > right:
            array[right], array[pivot] = array[pivot], array[right]
        else:
            array[left], array[right] = array[right], array[left]

    quick_sort(array, start, right - 1)
    quick_sort(array, right + 1, end)
quick_sort(array, 0, len(array) -1)
print(array)
```

```python
# 2번째
import random

array = random.sample(range(100), 10)

def quick_sort(array):
    if len(array) <= 1:
        return array

    pivot = array[0]
    left, right = list(), list()

    for idx in range(1, len(array)):
        if array[idx] < pivot:
            left.append(array[idx])
        else:
            right.append(array[idx])
        
    return quick_sort(left) + [pivot] + quick_sort(right)

print(quick_sort(array))
```

```python
# 3번째
import random

array = random.sample(range(100), 10)

def quick_sort(array):
    if len(array) <= 1:
        return array

    pivot = array[0]
    tail = array[1:]

    left = [x for x in tail if x <= pivot]
    right = [x for x in tail if x > pivot]
        
    return quick_sort(left) + [pivot] + quick_sort(right)

print(quick_sort(array))
```
