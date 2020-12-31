## Prefix_sum

1. `Prefix_sum(구간 합)`: 연속적으로 나열된 `N`개의 수가 있을 때, 특정 구간의 모든 수를 합한 값을 구하는 문제

<span style='color:blue'>각 쿼리에 대해 구간합을 빠르게 계산하기 위해서는 N개의 수의 위치 각각에 대하여 접두사 합을 미리 구해 놓으면 된다.</span>

여기서 접두사 합이란 리스트의 맨 앞부터 특정 위치까지의 합을 구해 놓은 것을 말한다.

```python
n = 5
data = [10, 20, 30, 40, 50]

value_sum = 0
prefix_sum = [0]

for i in data:
    value_sum = value_sum + i
    prefix_sum.append(value_sum)

left = 3
right = 4
result = prefix_sum[right] - prefix_sum[left - 1]
print(result)
👉🏽 70
```

---

### [ 예제 ] 백준 11659
<a href='https://www.acmicpc.net/problem/11659'>문제</a>

```python
import sys

n, m = map(int, input().split())
data_input = list(map(int, sys.stdin.readline().split()))

value = 0
prefix_sum = [0]

for i in data_input:
    value = value + i
    prefix_sum.append(value)

for i in range(m):
    left, right = map(int, sys.stdin.readline().split())
    result = prefix_sum[right] - prefix_sum[left - 1]
    print(result)
```

![](https://images.velog.io/images/abcd8637/post/4cf4768d-b24e-407b-88c8-1d9aa907a413/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-31%2010.52.32.png)