## prefix_sum

1. `Prefix_sum(구간 합)`: 연속적으로 나열된 `N`개의 수가 있을 때, 특정 구간의 모든 수를 합한 값을 구하는 문제

<span style='color:blue'>각 쿼리에 대해 구간합을 빠르게 계산하기 위해서는 N개의 수의 위치 각각에 대하여 접두사 합을 미리 구해 놓으면 된다.</span>
여기서 접두사 합이란 리스트의 맨 앞부터 특정 위치까지의 합을 구해 놓은 것을 말한다.

`prefix_sum`을 사용하지 않은 구간 합의 시간복잡도는 `O(NM)`이나 (1 <= N <= 100,000 / 1 <= M <= 100,000 일때) `prefix_sum`을 사용하게 되면 `O(N+M)`이 된다.

```python
n = 5
data = [10, 20, 30, 40, 50]
prefix_sum = [0]

# 1번 방법
value_sum = 0
for i in data:
    value_sum = value_sum + i
    prefix_sum.append(value_sum)

# 2번 방법
for i in range(1, n):
    data[i] += data[i-1]
prefix_sum += data

left = 3
right = 4
result = prefix_sum[right] - prefix_sum[left - 1]
print(result)
👉🏽 70

# 3번 방법, prefix를 구하지 않고 원래 data 값에서 계산
print(sum(data[left-1:right]))
👉🏽 70
```

---
## 📍 백준 11659 - 구간 합 구하기 4 
<a href='https://www.acmicpc.net/problem/11659'>백준 11659 - 구간 합 구하기4</a>

### ⚡️ 나의 풀이
이 문제를 그냥 구현한다면 `시간 초과`에서 벗어나지 못할 것이다. 바로 시간복잡도가 높기 때문인데, 이럴 때 시간복잡도를 낮출 적절한 알고리즘이 바로 `prefix_sum`이다. `prefix_sum`의 난이도는 어렵지 않다. 

서두에서 말했듯이 이 문제를 `prefix_sum`을 사용하지 않고 구현 할 때  `N, M`의 입력범위가 `100,000`이 넘어간다면 시간복잡도는 `O(NM)`이 되므로 1초내에 구현 할 수가 없다. <span style='color:blue'>알고리즘을 설계할 때마다 고려해야 하는 점은 여러 번 사용될 만한 정보는 미리 구해서 저장해 놓을수록 유리하다.</span> 

구현 방법은 간단한데, 각각의 합들을 새로운 배열에 저장해뒀다가 나중에 입력에 구간이 들어오면 해당 구간을 `index`로 바꿔서 출력해주면 된다. 이때, `index`를 헷갈리게 하지 않기위해 새로운 배열에 0을 추가해둔다. 매 입력이 들어올 때 `P[right] - P[left-1]`을 수행하면 계산시간은 `O(1)`이 되고, 결과적으로 N개의 데이터와 M개의 입력이 있을 때, 전체 구간 합을 구하는 작업은 `O(N+M)`의 시간이 보장된다.

```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
arr = list(map(int, input().split()))
prefix_sum = [0]    # init prefix_sum    

temp = 0    
for i in arr:    # accumulate arr section 
    temp += i
    prefix_sum.append(temp)

for i in range(m):
    a, b = map(int, input().split())
    print(prefix_sum[b] - prefix_sum[a-1])
```
