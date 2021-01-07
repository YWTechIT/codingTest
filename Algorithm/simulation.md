## simulation
알고리즘을 각 한 단계씩 직접 수행하는 알고리즘. `Brute_force`와 함께 구현의 핵심 알고리즘이 되는 경우가 많다.
`N x N Matrix` 문제로 자주 출제 됨.

---

## 📍 [ 문제 ] 상하좌우

```python
n = int(input())
directions = input().split()
vector = ['L', 'R', 'U', 'D']

# 최초위치
x, y = 1, 1

# 좌우상하 방향벡터 선언
# 행 Index
dx = [0, 0, -1, 1]
# 열 Index
dy = [-1, 1, 0, 0]

for direction in directions:
    for i in range(len(vector))
        if direction == vector[i]:
            nx = n + dx[i]
            ny = n + dy[i]
    
    if nx < 1 or ny < 1 or nx > n or ny > n:
         continue
    x, y = nx, ny

print(nx, ny)
👉🏽 입력
5 
R R R U D

👉🏽 출력
3 4
```
