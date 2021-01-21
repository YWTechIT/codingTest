## binary_search(이진탐색)
> 1. 찾으려는 데이터와 중간점(Middle) 위치에 있는 데이터를 반복적으로 비교해서 찾는 과정`(quick_sort와 비슷)`
> 2. 데이터가 무작위 일때는 사용할 수 없고, `정렬(sort)`이 되어있어야만 사용이 가능함
> 3. 탐색 범위를 절반씩 좁혀가며 데이터를 탐색함
> 4. 시간복잡도는 `O(logN)`
> 5. 재귀함수를 호출하는 방법, 반복문을 돌리는 방법 2가지가 있음

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

