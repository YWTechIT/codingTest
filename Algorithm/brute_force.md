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

---
## 📍 백준 1436 - 영화감독 숌

<a href='https://www.acmicpc.net/problem/1436'>백준 1436 - 영화감독 숌</a>

## ⚡️ 나의 풀이
전형적인 `브루트포스`문제다.

1. `6`이 적어도 3개 이상 등장해야한다.
2. `number+=1`씩 증가하면서 `666`이 있는지 확인한다.
3. `number`가 있으면, `result`에 추가시킨다.

코드를 작성하고 나니까 굳이 `result`에 추가시키지 않아도 된다는 생각을 했다. 그리고 `while`문 종료조건이 가독성이 떨어져보여서 직접 작성하지말고 `flag`로 대체해야겠다는 생각을 했다.

```python
# 나의 풀이
n = int(input())
number = 665
result = []

while not len(result) >= n:
    if str(number).count('666') >= 1:
        result.append(number)
    number+=1

print(result[n-1])
```

```python
# 다른사람의 풀이
n = int(input())
number = 665
flag = True
cnt = 0

while flag:
    if '666' in str(number):
        cnt += 1
        print(cnt, number)

    if n == cnt:
        flag = False
    else:
        number+=1
print(number)
```

---
## 📍 백준 1018 - 체스판 다시 칠하기

<a href='https://www.acmicpc.net/problem/1018'>백준 1018 - 체스판 다시 칠하기</a>

## ⚡️ 나의 풀이
이 문제에서 고민해야 할 부분은 크게 다음과 같이 나뉜다.

1. 좌측상단이 `B` / `W`부터 시작하는 체스판을 만든다. (이때, 번갈아가면서 색칠되어있어야 함.)
2. `N * M` 크기의 보드를 입력받는다. (이때, `N`은 세로, `M`은 가로)
3. `N * M` 크기의 보드를 `8 * 8`형태로 자르고, 1번에서 작성한 두 개의 체스판의 좌표를 서로 비교한다.
4. 좌표의 값이 서로 다르면 `cnt`를 증가하는데, 더 작은 값을 `return` 한다.

`1번 방법`을 좌표가 나타내는 일정한 규칙으로 구현하지 않고 내 방식대로 구현하다가 시간을 다 까먹고 구현을 하지도 못했다. 😭 😭 `W`가 먼저 시작하는 체스판을 만들 때 좌표를 보면 다음과 같은 규칙이 있다. 

1. `W`가 나타내는 좌표를 작성한다.
2. `W`의 좌표 `i+j`는 모두 짝수이다.
3. `B`가 나타내는 좌표를 작성한다.
4. `B`의 좌표 `i+j`는 모두 홀수이다.

![](https://images.velog.io/images/abcd8637/post/7a9ae683-80d3-4273-9021-f89210fce34c/KakaoTalk_Photo_2021-05-24-07-50-12.jpeg)

이후 `n*m` 배열에서 `8*8` 좌표를 모두 확인해야하는데, 이것도 구현하는 방법을 잘 몰랐는데 다음과 같이 생각하면 된다. 이해가 잘 안된다면 저번에 작성한 <a href='https://ywtechit.tistory.com/125'>글</a>을 보자.

1. `n-7`, `m-7`의 범위로 이중 반목문을 선언한다. `n`과 `m`이 모두 8이면, `n-7 = 1`, `m-7 = 1`이 되는데 반복문의 범위는 `1-1`까지 세기때문에 `0`까지만 범위로 잡힌다.
2. 1번에서 선언한 이중 반복문이 `0`으로 고정되는동안 `8*8`의 범위로 한번 더 이중 반복문을 선언한다. 
3. `chess`판과 비교한다.

값이 2개 이상인데 최소값을 갱신할때는 다음과 같이 사용하자.
1. cnt = min(cnt, temp1)
2. cnt = min(cnt, temp2)

```python
# 4중 반복문
n, m = map(int, input().split())
chess_W = [[0] * m for _ in range(n)]
chess_B = [[0] * m for _ in range(n)]
arr = [list(input()) for _ in range(n)]
cnt = float('inf')

for i in range(n):
    for j in range(m):
        if not (i+j) % 2:
            chess_W[i][j] = 'W'
            chess_B[i][j] = 'B'
        else:
            chess_W[i][j] = 'B'
            chess_B[i][j] = 'W'

for i in range(n-7):
    for j in range(m-7):
        temp_W, temp_B = 0, 0
        for x in range(8):
            for y in range(8):
                if arr[i+x][j+y] != chess_W[i+x][j+y]:
                    temp_W += 1
                if arr[i+x][j+y] != chess_B[i+x][j+y]:
                    temp_B += 1
        cnt = min(cnt, temp_W)
        cnt = min(cnt, temp_B)
print(cnt)
```

```python
# 2중 반복문 + 함수
n, m = map(int, input().split())
chess_W = [[0] * m for _ in range(n)]
chess_B = [[0] * m for _ in range(n)]
arr = [list(input()) for _ in range(n)]
cnt = float('inf')

def check(a, b):
    global cnt
    temp_W, temp_B = 0, 0
    for x in range(8):
        for y in range(8):
            if arr[a + x][b + y] != chess_W[a + x][b + y]:
                temp_W += 1
            if arr[a + x][b + y] != chess_B[a + x][b + y]:
                temp_B += 1
    cnt = min(cnt, temp_W)
    cnt = min(cnt, temp_B)
    return cnt

for i in range(n):
    for j in range(m):
        if not (i+j) % 2:
            chess_W[i][j] = 'W'
            chess_B[i][j] = 'B'
        else:
            chess_W[i][j] = 'B'
            chess_B[i][j] = 'W'

for i in range(n-7):
    for j in range(m-7):
        check(i, j)

print(cnt)
```

---
## 📍 백준 2309 - 일곱 난쟁이

<a href='https://www.acmicpc.net/problem/2309'>백준 2309 - 일곱 난쟁이</a>

## ⚡️ 나의 풀이
`브루트 포스(brute force)`유형 문제인데 핵심은 다음과 같다. 아홉 난쟁이의 키는 모두 다르지만 그 중 일곱 난쟁이의 크기의 합은 100이된다. 즉, `sum(arr) - (난쟁이1, 난쟁이2) == 100`과 같은 말이다. 그런데 몇 번 난쟁이가 들어가야할지 모르기때문에 모든 경우의 수를 찾아야한다.

1. `sum(arr) - (arr[i] + arr[j]) == 100`이 되면 해당 난쟁이를 새로운 변수로 넣어두고 마지막에 `arr`에서 제거한다. 
2. `sum(arr) - (arr[i] + arr[j]) == 100`이 되면 반복문을 한번 더 선언하고 해당 난쟁이를 제외하고 출력 후 `exit()`로 빠져나온다. `break`문을 사용하게되면 해당 반복문만 빠져나오고 다시 반복문을 돌기때문에 주의하자.

```python
# 1번째 방법 (temp, remove)

n = 9
temp1, temp2 = 0, 0
arr = [int(input()) for _ in range(n)]

for i in range(n):
    for j in range(i+1, n):
        if sum(arr) - (arr[i] + arr[j]) == 100:
            temp1 = arr[i]
            temp2 = arr[j]

arr.remove(temp1)
arr.remove(temp2)

print('\n'.join(map(str, sorted(arr))))
```

```python
# 2번째 방법 (continue, exit)

n = 9
arr = [int(input()) for _ in range(n)]
arr.sort()

for i in range(n):
    for j in range(i+1, n):
        if sum(arr) - (arr[i] + arr[j]) == 100:
            for k in range(9):
                if i == k or j == k:
                    continue
                print(arr[k])
            exit()

print('\n'.join(map(str, arr)))
```
