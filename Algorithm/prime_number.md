# 소수판별 알고리즘 1

```python
import math

n = 100

def is_prime_number(x):
    for i in range(2, int(math.sqrt(x))+1):
        if i % x == 0:
            print('not prime')
        else:
            print('prime')
```

# 소수판별 알고리즘 2(에라토스테네스의 체)
```python
import math

n = int(input())

array = [ True for in range(n+1) ]

for i in range(2, int(math.sqrt(n))+1):
    if array[i] == True:
        j = 2
        while i * j <= n:
            array[i*j] = False
            j = j + 1

for i in range(2, n+1):
    if array[i]:
        print(i, end = ' ')
```

# 소수판별 알고리즘 2(에라토스테네스의 체 응용: 구간 별 소수찾기) 
```python
import math

n, m = map(int, input().split())

array = [True for i in range(m + 1)]

for i in range(2, int(math.sqrt(m)) + 1):
    if array[i] == True:
        j = 2
        while i * j <= m:
            array[i * j] = False
            j = j + 1

for i in range(n, m + 1):
    if array[i]:
        print(i, end=' ')


```
