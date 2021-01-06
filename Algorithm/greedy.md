# greedy
> 최종 해답을 찾기 위해 각 단계마다 하나의 답을 고름
> 각 단계에서 답을 고를 때 가장 좋아 보이는 답을 선택
> 선택할 당시 최적의 답을 고르지만, 최종 해답이 반드시 최적임을 보증하지 않음

---

## 📍 유형 1. 거스름 돈
문제: 카운터에 거스름 돈으로 사용 할 500원, 100원, 50원, 10원짜리 동전히 무한히 존재한다고 가정한다.
손님에게 거슬러 줘야 할 돈이 N원일때, 거슬러줘야 할 동전의 최소 개수를 구하라. 단, 거슬러 줘야 할 돈 N은 항상 10의 배수이다.

```python
n = 1260
coin_array = [500, 100, 50, 10]
count = 0

# count: n을 coin으로 나눈 몫
# `n`을 `coin`으로 나눈 나머지를 0이될때까지 지속함 
for coin in coin_array:
    count = count + n // coin
    n = n % coin

print(count)
👉🏽 6
```
---

## ✏️ [ 문제 ] 백준 - 거스름 돈(5585)
<a href='https://www.acmicpc.net/problem/5585'>문제</a>

문제 중 `카운터에서 1000엔 지폐를 한장 냈을 때`라고 선언되어있기 때문에, 입력값은 항상 `1000`을 빼줘야한다.
다음 잔돈은 이미 주어져있기 때문에 `data` 값으로 넣으면 된다.

다음과 같이 풀 수 있다.

```python
t = int(input())
n = 1000 - t

data = [500, 100, 50, 10, 5, 1]
count = 0

for coin in data:
    count = count + n // coin
    n = n % coin
print(count)

👉🏽 예제 입력: 380, 예제 출력: 4
```

![](https://images.velog.io/images/abcd8637/post/61d03529-4479-4a12-8dd3-2f7a40f7ccca/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%2010.46.04.png)

---

## ✏️ [ 문제 ] 백준 - ATM(11399)
<a href='https://www.acmicpc.net/problem/11399'>문제</a>

해당 문제도 거스름 돈과 동일하게 `그리디(greedy)` 알고리즘을 사용하면 된다.

앞에 위치한 사람이 걸리는 시간만큼 누적되는 계산이다.
즉, 뒤로 갈수록 누적한 값이 최소가 되어야하고 리스트를 `sort(), 오름차순`으로 배열 한 다음 풀면되는 문제다.

여기까지 도출하는데 성공했으나, 뒤에 리스트에 값을 `누적`하면서 더하는 방법(?)을 몰랐다.

결국 `for문`을 `2번`돌면 풀수있는 문제였는데, 
그게 어려웠다. 아직 많이 부족한것 같다.

for문을 2번 사용하는 문제를 풀어봐야겠다. 

```python
n = int(input())
data = list(map(int, input().split()))
data.sort()

result = 0

for i in range(n):
    for j in range(i+1):
        result = result + array[j]
print(result)
👉🏽 예제입력
5 
3 1 4 3 2

👉🏽 예제출력
32
```

![](https://images.velog.io/images/abcd8637/post/9c31551c-f401-479f-b4b0-1deaa39c7145/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-05%2012.01.36.png)

---

## ✏️ [ 문제 ] 숫자카드게임
<a href='https://book.naver.com/bookdb/book_detail.nhn?bid=16439154'>이것이 코딩 테스트다 - 나동빈</a>

여러개의 숫자 중에서 가장 높은 숫자가 쓰인 카드 한 장을 뽑는 게임

>해설: 각 행마다 가장 작은 수를 찾은 뒤에 그 수 중에서 가장 큰 수를 찾기

```python
n, m = list(map(int, input().split()))
result = 0

# n만큼 열 생성
# data로 입력을 받음.
# min_value중에서 큰 수를 기존의 result와 비교한뒤에 새로운 result에 저장함

for i in range(n):
    data = list(map(int, input().split()))
    min_value = min(data)
    result = max(result, min_value)

print(result)
```

---

## ✏️ [ 문제 ] 1이 될 때까지
<a href='https://book.naver.com/bookdb/book_detail.nhn?bid=16439154'>이것이 코딩 테스트다 - 나동빈</a>

문제: 어떠한 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고한다. 단, 두 번째 연산은 N이 K로 나누어떨어 질 때만 선택할 수 있다.

```python
n, k = map(int, input().split())
count = 0

# 전체 while문을 사용해서 거짓 조건으로 먼저 빼고 이후 참인 조건을 넣자.
# 마지막으로 남은 수는 1씩 빼기
while n >= k:
    while n % k != 0:
        n = n - 1
        n = n / k
    n = n / k
    count = count + 1

while n > 1:
    n = n - 1
    count = count + 1

print(count)

```



