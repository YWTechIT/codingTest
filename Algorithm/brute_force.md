## brute_force

모든 경우의 수를 판단하는 알고리즘
`브루트 포스(BruteForce)`라고 불리며, 보통 데이터가 `1,000,000`개 이하 일때 완전탐색을 이용하면 적절하다.

## 💡 [21. 2. 18.]
모든 케이스를 계산하는것이 완전탐색이다. 
완전탐색을 사용하려면 먼저, 입력 조건을 살펴보자.
일반적인 코딩테스트의 채점 환경에서 1초에 2,000만에서 1억정도의 연산처리가 가능하므로 그 전까지의 경우의 수는 완전탐색으로 살펴보자.

---

## 💡 1차원 배열을 입력만큼 회전

```python
# slicing 기법
def rotate(arr, n):
    if not arr:
        return 0

    N = len(n)
    n %= N

    left = [:-n]
    right = [-n:]
    return right + left

print(rotate([1, 2, 3, 4, 5], 2))
👉🏽 [3, 4, 5, 1, 2]
```

```python
# for문을 사용한 기법
def rotate(arr, n):
    if not arr:
        return 0

    N = len(n)
    new_arr = [0 for _ in range(N)]
    n %= N

    for i in range(N):
        new_arr[(i % n) % N] = arr[i]
    return new_arr
    
print(rotate([1, 2, 3, 4, 5], 2))
👉🏽 [3, 4, 5, 1, 2]
```
---
## 💡 2차원 배열 90도, 180도, 270도, 360도 회전
```python
def rotate(arr, n):
    N = len(arr)
    new_arr = [[0] * N for i in range(N)]

    # 90도
    if n % 4 == 1:
        for i in range(N):
            for j in range(N):
                new_arr[j][N - 1 - i] = arr[i][j]
    # 180도
    elif n % 4 == 2:
        for i in range(N):
            for j in range(N):
                new_arr[N - 1 - i][N - 1 - j] = arr[i][j]
    # 270도
    elif n % 4 == 3:
        for i in range(N):
            for j in range(N):
                new_arr[N - 1 - j][i] = arr[i][j]
    # 360도
    else:
        for i in range(N):
            for j in range(N):
                new_arr[i][j] = arr[i][j]
    return new_arr

arr = [[0, 0, 0], [1, 1, 1], [0, 0, 0]]
print(rotate(arr, 1))
```
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

---
## 📍 백준 2231 - 분해합

<a href='https://www.acmicpc.net/problem/2231'>백준 2231 - 분해합</a>

## ⚡️ 나의 풀이
언젠가 백준의 단계별 문제풀이에서 이 문제를 봤었는데 그때는 이해가 안돼서 그냥 넘겨버렸다. 이번엔 집중해서 문제를 잡았더니 풀 수 있었는데 `시간단축`하는 방법은 끝내 찾지못했다. 브루트포스의 문제는 보통 범위가 `1,000,000`으로 주어진 경우가 많다. 코딩테스트 볼 때 범위가 `1,000,000`이라면 브루트포스를 의심해보자!

총 3번에 걸쳐서 풀었고, 첫번째는 `시간 초과`, 두번째는 성공이지만 시간이 많이 걸렸다. 세번째는 다른사람의 코드 중 시간최적화했던 부분을 가져왔다.

1. 입력을 받는다.
2. `target`의 분해합을 구하기위해 해당 값을 `str`로 바꾸고 각 자리수를 모두 더해준 값을 `temp`에 넣어준다.
3. 현재 i값과 `temp`를 더한 값을 `result`로 초기화시킨다.
4. 만약 `result` 값이 `target`과 동일하다면? 해당 값은 생성자다. 
5. 반복문을 모두 돌았는데도 생성자가 없다면 0을 출력한다. (for - else 구문)

이렇게 정답판정을 받았는데 `1376 m/s`이 걸렸다. 실행시간이 생각보다 길어서 최적화가 필요해보였다. 반복문의 시작범위를 줄이면 될것같은데, 어떻게 줄여야할지 감이 오지 않았다.

시간최적화하는 방법은 다음과 같다.
1. 분해합은 `N과 N의 각 자리수의 합`이다.
2. 반대로, 생성자를 구하려면 분해합을 구하는 과정 중 N은 놔두고 N의 각 자리수의 합만 빼주면 되는데, 어떤 수가 나올지 모르니까 각 자리수에 나올 수 있는 최대 수(0~9)인 9를 빼주면 된다.
3. 그대로 적용하게 되면 `N이 0~9`가 나올때는 `음수`가 나온다. 따라서 절댓값(`abs`)을 씌워주자.

![](https://images.velog.io/images/abcd8637/post/daf6d35b-bd9b-4aa9-afaf-4640400196d1/KakaoTalk_Photo_2021-05-12-11-39-07.jpeg)

```python
# 첫번째 시도: 시간 초과
target = int(input())
n, result = 0, 0

while target != result:
    n += 1
    temp = sum(map(int, str(n))) 
    result = n + temp
print(n)
```

```python
# 두번째 시도: 성공
target = int(input())

for i in range(target):
    temp = sum(map(int, str(i)))
    result = i + temp
    if result == target:
        print(i)
        break
else:
    print(0)
```

```python
# 다른사람의 코드: 시간 최적화
target = int(input())
min_target = abs(target - (len(str(target)) * 9))

for i in range(min_target, target):
    temp = sum(map(int, str(i)))
    result = i + temp
    if result == target:
        print(i)
        break
else:
    print(0)
```

![](https://images.velog.io/images/abcd8637/post/49c1636d-f501-408a-b305-0a7c43af735f/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-12%2010.17.10.png)

---
## 📍 백준 7568 - 덩치

<a href='https://www.acmicpc.net/problem/7568'>백준 7568 - 덩치</a>

## ⚡️ 나의 풀이
언젠가 `단계별 풀이`에서 한번 봤었는데, 어떻게 풀어야할지 몰라 넘겼었는데 이번엔 풀었다. 여기에서 가장 핵심 문장은 `각 사람의 덩치 등수는 자신보다 더 큰 덩치의 사람의 수로 정해진다.`이다. 이중 반복문의 범위는 `A-B, A-C, A-D, A-E` / `B-A, B-C, B-D, B-E` / `C-A, C-B, C-D, C-E` / `E-A, E-B, E-C, E-D` 처럼 모든 경우의 수를 비교 할 수 있게 선언해야한다. `A-B`나 `B-A`나 같은거아닌가?! 라고 생각 할 수도 있지만, 각각의 케이스에서 덩치 등수를 셀때 나를 제외한 모든 사람의 덩치를 비교해야하기 때문에 같지 않다. 

1. 자신을 포함한 모든 경우의 수를 조사한다.(반복문의 범위 설정의 편의성 위해 자신도 포함시켰다. 자신끼리는 대소관계가 성립되지 않는다.)
2. 1등보다 높은 등수(0등은 없다.)가 없으므로 등수(`prize`)의 초기값은 `1`이다.
3. 현재 값과 다음값을 비교해서 자신보다 더 큰 사람이 있다면 `prize`를 `1` 증가시킨다.(순위가 내려간다는 의미)

정답판정을 받았는데, 다른 사람의 코드에서는 나처럼 2중 반복문 중간에 `prize = 1`을 사용하지않고, `prize=[1]*n`으로 초기화를 해놓고나서 나중에 해당 인덱스만 1 증가하는 방법을 사용했다. 가독성이 괜찮은 코드였고, 인덱스마다 `cnt`를 증가하는 문제를 풀 때 사용하면 좋을것 같다.

```python
n = int(input())
people = [tuple(map(int, input().split())) for _ in range(n)]
result = []

# 나의 코드
for i in range(n):
    prize = 1
    for j in range(n):
        if people[i][0] < people[j][0] and people[i][1] < people[j][1]:
            prize += 1
    result.append(prize)
print(' '.join(map(str, result)))

# 다른사람의 코드
prize = [1] * n

for i in range(n):
    for j in range(n):
        if people[i][0] < people[j][0] and people[i][1] < people[j][1]:
            prize[i] += 1
print(' '.join(map(str, result)))
```
