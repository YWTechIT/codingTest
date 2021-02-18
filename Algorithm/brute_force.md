## brute_force

모든 경우의 수를 판단하는 알고리즘
`브루트 포스(BruteForce)`라고 불리며, 보통 데이터가 `1,000,000`개 이하 일때 완전탐색을 이용하면 적절하다.

## 💡 [21. 2. 18.]
모든 케이스를 계산하는것이 완전탐색이다. 
완전탐색을 사용하려면 먼저, 입력 조건을 살펴보자.
일반적인 코딩테스트의 채점 환경에서 1초에 2,000만에서 1억정도의 연산처리가 가능하므로 그 전까지의 경우의 수는 완전탐색으로 살펴보자.

---

## 📍 [ 문제 ] 시간

문제: 정수 `N`이 입력되면 00시 00분 00초부터 N시 59분 59초이하의 모든 시간 중 '3'이 포함되는 경우의 수를 찾아보세요.

```python
n = int(input())
count = 0

for h in range(n+1):
    for m in range(60):
        for s in range(60):
            if '3' in str(h) + str(m) + str(s):
                count = count + 1
print(count)
👉🏽 입력
5

👉🏽 출력
11475            
```

## ✏️ [ 문제 ] 백준 - 블랙잭(2798)
<a href='https://www.acmicpc.net/problem/2798'>문제</a>

```python
import itertools

n, m = map(int, input().split())
cards = list(map(int, input().split()))

result = 0

# 배열값을 큰 순으로 정렬하려면 result보다 크게 범위를 설정한다.
for card in itertools.combinations(cards, 3):
    if result < sum(card) <= m:
        result = sum(card)
print(result)
```