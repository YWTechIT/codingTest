## brute_force

모든 경우의 수를 판단하는 알고리즘
`브루트 포스(BruteForce)`라고 불리며, 보통 데이터가 `1,000,000`개 이하 일때 완전탐색을 이용하면 적절하다.

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