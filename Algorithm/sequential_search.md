## sequential_search(순차탐색)
> 1. 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례대로 확인하는 방법
> 2. 보통 정렬되어있지 않은 리스트에서 데이터를 찾아야할때 사용함.
> 3. 시간만 충분하다면 항상 값을 찾을 수 있다.
> 4. 리스트의 데이터에 하나씩 방문하며 특정한 문자열과 같은지 검사한다
> 5. 시간복잡도는 `O(N)`


```python
def sequential_search(n, target, array):
    for i in range(n):
        if array[i] == target:
            return i + 1

input_data = input().split()
n = int(input_data[0])
target = input_data[1]

array = input().split()

print(sequential_search(n, target, array))
```