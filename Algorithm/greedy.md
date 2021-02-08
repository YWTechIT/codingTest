# greedy
> 최종 해답을 찾기 위해 각 단계마다 하나의 답을 고름
> 각 단계에서 답을 고를 때 가장 좋아 보이는 답을 선택
> 선택할 당시 최적의 답을 고르지만, 최종 해답이 반드시 최적임을 보증하지 않음

2021.2.8.
> 1. 다음 해를 계산하기 전까지는 모두 만들 수 있다고 가정함.
> 2. 만약에 만들수 없다면, `n-1`번째를 확인함

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

---

## ✏️ [ 문제 ] 곱하기 혹은 더하기
각 자리의 숫자로만 이루어진 문자열 S가 주어졌을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 숫자 사이에 `x(곱하기)` 혹은 `+(더하기)`연산자를 넣어 만들어 질 수 있는 가장 큰 수를 구하는 프로그램을 작성하시오.

### 🤔 나의 풀이
큰 수를 만들기 위해서는 더하기보다는 곱하는것이 타당하다고 생각했다. 하지만 입력 예시에 `0`과 `1`이 포함되는 경우가 있었는데, `1`은 간과하고 `0`만 생각하고 `0`이 나오면 조건에 더해주는 코드만 넣었다. 

그리고 `multi`의 초기값은 곱하기때문에 1로 설정하자<spans style ='color:blue'>(습관적으로 0으로 선언했다가 결과값이 자꾸 0으로 나오길래 `pycharm`이 고장난 줄 알았다. ~~컴퓨터는 거짓말을 하지 않았다.~~)</span>

또, 문제에 입력 예시가 2개나 있었지만, 혹시 몰라 반증의 예를 찾다가 `91110`을 떠올렸다.  

내가 작성한 코드로 계산하면 `9x1x1x1+0 = 9`가 되는데 이는, 더하기 조건에 1을 포함하면 나오는 `9+1+1+1+0 = 12` 값이 반례가 되기때문에 결론적으로 0과 1을 더하기 조건에 포함시켰다.

그리고 책에서는 `input`값에 `list`을 쓰지 않았는데 이후에 `if array[i] <= '1':`에서 1은 문자열(str)이기 때문에 따옴표를 붙여준것도 헷갈리지 말자.

```python
'''
02984
567
91110
'''
array = list(map(int, input()))
multi = 1
plus = 0
result = 0

for i in range(len(array)):
    if array[i] <= 1:
        plus = plus + array[i]
    else:
        multi = multi * array[i]
    result = multi + plus
print(result)
👉🏽 
576
210
12
```

---

## ✏️ [ 문제 ] 문자열 뒤집기
연속된 하나 이상의 숫자를 잡고 모두 뒤집는다. 
뒤집는 것은 1을 0으로, 0을 1로 바꾸는 것을 의미한다.

### 🤔 나의 풀이
접근을 어떻게 할까 고민했는데, 약간의 힌트를 얻어 현재 array[i] 값과 다음 array[i+1]이 비교하여 서로 같지 않을때 array[i+1]의 수가 0인지 1인지에 따라 `count` 하는 변수를 다르게 설정하여 조건을 걸었다.

마지막에는 두개의 변수 중 `min값`을 출력하게 설정했다.

```python
array = list(map(int, input()))
count_0 = 0
count_1 = 0

if array[0] == 1:
    count_1 += 1
else:
    count_0 += 1

for i in range(len(array)-1):
    if array[i] != array[i+1]:
        if array[i+1] == 1:
            count_1 += 1
            print(array[i+1])
        else:
            count_0 += 1

result = min(count_0, count_1)
print(result)
👉🏽 1
```
---

## ✏️ [ 문제 ] 만들 수 없는 금액
N개의 동전을 이용하여 만들 수 없는 양의 정수 금액 중 최솟값을 구하는 프로그램을 작성하시오.

### 🤔 나의 풀이
어떤 방식을 사용해야하는지 고민을 오래했다.
만들 수 없는 금액이면 반대로 만들 수 있는 금액을 구하고 나머지 값 중 최소값을 구하면되나? 라는 생각도 했는데 접근 방향이 잘못됐다.. 😅 😅

먼저 화폐를 오름차순으로 정렬하고 현재 금액 값을 선언한 이후 하나씩 비교하면서 현재 금액값을 만들 수 있으면 현재 금액값을 갱신하는 방식을 이용했다.

![](https://images.velog.io/images/abcd8637/post/5c1dfb92-64bf-409c-8d51-d3bc3e8d09ed/KakaoTalk_Photo_2021-02-08-13-22-10.jpeg)

중요한 점은 갱신한 값보다 작은 값들은 화폐로 만들 수 있다.
예를 들어 `current = 4`보다 작은 값 `3`은 `1, 2`를 사용해서 만들 수 있다. 

만약, 갱신이 불가능하면 `-1`값은 만들 수 있는지 살펴보자

```python
'''
3 2 1 1 9
'''
n = int(input())
coins = list(map(int, input().split()))
current = 1

coins.sort()

for i in coins:
    if i <= current:
        current = current + i
    print(current)
👉🏽 8 
```
---

## ✏️ [ 문제 ] 코드업 2001 - 최소 대금
<a href='https://codeup.kr/problem.php?id=2001'>코드업 - 2001 문제 </a>

### 🤔 나의 풀이
이렇게 풀어도 되나 싶은데, 2가지 방법을 이용했다.
결과적으로 최소의 가격을 선택해 최소값을 구하는 문제이기때문에 `.sort`를 사용해서 맨 앞에 있는 값을 출력해서 계산하는 방법과 `min()` 함수를 사용해 최소값을 출력하는 방법을 사용했다.

민망할 정도로 코드가 짧긴하지만 정답판정을 받았다.

```python
'''
800
700
900
198
330
'''

total_set = []
pasta = []
juice = []

for i in range(5):
    input_set = int(input())
    total_set.append(input_set)
    pasta = total_set[0:3]
    juice = total_set[3:5]

pasta.sort()
juice.sort()

result = (pasta[0] + juice[0]) * 1.1
print(round(result, 2))
👉🏽 987.8
```

```python
## 방법 2
'''
800
700
900
198
330
'''

total_set = []
pasta = []
juice = []

for i in range(5):
    input_set = int(input())
    total_set.append(input_set)
    pasta = total_set[0:3]
    juice = total_set[3:5]

result= (min(pasta) + min(juice)) * 1.1
bill = round(result, 2)
print(bill)
👉🏽 987.8
```
