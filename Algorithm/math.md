## 📍 백준 10886 - 0 = not cute / 1 = cute
<a href='https://www.acmicpc.net/problem/10886'>백준 10886 - 0 = not cute / 1 = cute</a>

### 💡 나의 풀이
나오는 경우의 수가 1과 0뿐일 때, 어떤 값이 cnt를 더 많이 받았는지 알 수 있는 방법
방법 1. 1과 0의 cnt를 변수로 선언한다
방법 2. 1이 나올 변수가 N // 2보다 크면 1이 나온얘기

```python
N = int(input())

op = []
for i in range(N):
    op.append(int(input()))

like = op.count(1)
unlike = op.count(0)

if like < unlike:
    print('Junhee is not cute!')
else:
    print('Junhee is cute!')

```

```python
N = int(input())

cute = 0
for i in range(N):
     if int(input()) == 1:
         cute+=1

if cute > N//2:
    print("Junhee is cute!")
else:
    print("Junhee is not cute!")
```

---
## 📍 백준 4153 - 직각삼각형
<a href='https://www.acmicpc.net/problem/4153'>백준 4153 - 직각삼각형</a>

## 💡 나의 풀이
중요한 원리는 입력받은 코드 중에서 제일 큰 값을 빼두고(remove()) 나머지값을 더해 같은지 확인하면된다. 


```python
while True:
    v = list(map(int, input().split()))
    m = max(v)
    v.remove(m)
    if m == 0:
        break
    else:
        if m**2 == v[0] ** 2 + v[1] ** 2:
            print('right')
        else:
            print('wrong')
```

---
## 📍 백준 1085 - 직사각형에서 탈출
<a href='https://www.acmicpc.net/problem/1085'>백준 1085 - 직사각형에서 탈출</a>

## 💡 나의 풀이
직사각형의 경계선까지 이동하면 되는데, 결론적으로 경계선은 `w` 혹은 `h`에 더 가까운 수를 구하면 된다. 또한 직사각형이기 때문에 대각선은 고려하지 않는다. 나의 코드에서 b의 `min(x-0, y-0)`은 `min(x, y)`와 동일하지만 사고 흐름을 남겨놓고 싶어 0을 붙였다. 더욱 간결하게 작성하려면 다른사람의 코드를 참고하자.

```python
# 나의 코드
x, y, w, h = map(int, input().split())
a = min(w - x, h - y)
b = min(x - 0, y - 0)
print(min(a, b))

# 다른사람의 코드
x, y, w, h = map(int, input().split())
print(min([x, y, w-x, h-y]))
```

---
## 📍 백준 2010 - 플러그
<a href='https://www.acmicpc.net/problem/2010'>백준 2010 - 플러그</a>

## 💡 나의 풀이
처음 문제 풀 때 각각 멀티탭을 꽂을 수 있는 개수만큼 `max`값만 갱신하면 되는거아냐? 라고 생각했는데 그게 아니었다. 멀티탭에 또 멀티탭을 꽂을 수 있다는 사실을 잊었다. 나처럼 잘 이해가 안되는 사람들을 위해 그림을 하나 그려봤다. (발(🦶🏾)그림 주의)

예를 들어 입력이 `4 4 3 2 1` 이라고 가정해보자. 벽단자는 그림의 이해를 위해서 그린것이고 멀티탭만 보면된다. 이미 꽂혀 있는 멀티탭을 제외하고 남은 멀티탭에서 최대 개수를 구할 때 규칙을 찾아보면 무조건 하나씩은 꽂혀있기 때문에 `총 멀티탭에서 꽂을 수 있는 구멍 - (멀티탭의 수 - 1)`가 된다. 그래도 이해가 잘 안되면 그림을 다시 한번 살펴보자.

![](https://images.velog.io/images/abcd8637/post/6250b8f9-95ff-43d2-ad3b-007ffd5a0187/KakaoTalk_Photo_2021-06-08-11-31-05.jpeg)

```python
import sys
input = sys.stdin.readline

n = int(input())
total_plug = 0

for _ in range(n):
    plug = int(input())
    total_plug += plug

print(total_plug-(n-1))
```

---
## 📍 백준 2480 - 주사위 세개
<a href='https://www.acmicpc.net/problem/2480'>백준 2480 - 주사위 세개</a>

## 💡 나의 풀이
이 문제의 핵심은 `같은 눈`이 몇개가 나왔는지 분류를 하는 방법이다.

내가 풀었던 방법은 `set`의 특징 중 `중복 제거`를 이용했는데 주사위를 더 많이 던질때 사용하면 괜찮은 방법인것 같다. 다시 본론으로 돌아가 `len(set(arr)) == 1`이면 모든 수가 같은 수이기 때문에 1개로 줄어들은 것이다. 따라서 같은 눈이 3개라고 할 수 있다. 반대로 `len(set(arr)) == 3`이면 모두 다르기때문에 중복제거가 일어나지 않았다. 이제 나머지 조건인 같은 눈이 2개만 나오는 경우를 찾으면 되는데 `set`으로 찾을 방법이 떠오르지 않아 `반복문 + count + index`를 이용했고 `count`가 2개 이상인 `index`를 찾아 `arr[index]`를 반환시켰다.

다른 사람의 코드는 `3개가 동일한 경우`, `2개가 동일한 경우`, `모두 다른 경우`를 각각 조건식으로 작성하여 논리연산자로 비교하는 방법을 사용했다. 다음에 문제를 풀 때 3개의 조건만 나온다면 논리연산자로 비교하는 방법을 사용하는 것이 가독성이 더 좋아 보였다.

```python
# 나의 코드
arr = list(map(int, input().split()))
temp = 0

if len(set(arr)) == 1:   # 3개가 동일한 경우
    print((10**4) + (arr[0] * 1000))

elif len(set(arr)) == 3:    # 모두 다른 경우
    print(max(arr) * 100)

else:    # 2개가 동일한 경우
    for i in range(3):
        if arr.count(arr[i]) == 2:
            temp = arr[arr.index(arr[i])]
    print(1000 + (temp * 100))
```

```python
# 다른 사람의 코드
a, b, c = map(int, input().split())

if a == b and b == c:    # 3개가 동일한 경우
    print(10000 + (a * 1000))

elif a == b or b == c:    # 2개가 동일한 경우
    print(1000 + (b * 100))

elif a == c:    # 2개가 동일한 경우
    print(1000 + (a * 100))

else:    # 모두 다른 경우
    print(max(a, b, c)*100)
```

---
## 📍 백준 1712 - 손익분기점
<a href='https://www.acmicpc.net/problem/1712'>백준 1712 - 손익분기점</a>

## 💡 나의 풀이
손익 분기점에 대한 이해가 있어야 이 문제를 풀 수 있다. 처음에 `while`문을 사용하여 풀 수 있을 줄 알았는데 다시보니까 `A`, `B`, `C`가 21억 이하의 자연수기때문에 `시간초과`판정이 날 것 같았다.(게다가 시간제한도 무려 `0.35`초 밖에 안된다.) 반복문을 사용하지 않고서 풀 수 있는 방법은 단순 `사칙연산`일텐데 공식이 잘 떠오르지 않았다. ㅠㅠ 구글링하다 <a href='https://www.youtube.com/watch?v=0We9SlFi3ow&t=682s'>코딩펜</a>님 영상을 봤는데 이해가 잘 됐다.

결론적으로 손익분기점은 `고정비용 + 가변비용 * n < 판매비용 * n` 과 같이 나타 낼 수 있는데 다음과 같이 식을 정리 할 수 있다. (고정비용은 a, 가변비용은 b, 판매비용은 c로 가정했다.)

1. a + (b * n) = (c * n)
2. a = (c * n) - (b * n)
3. a = (c - b) * n
4. (a // (c - b)) = n

여기서 총 수입(`(a // (c - b))`)이 총 비용(`n`)보다 많아지려면 `총 수입 + 1`을 해줘야 이익이 생긴다. 즉, `(a // (c - b)) + 1`을 작성하면 되는데 이때 주의 할 점은 `c <= b` 일때는 결과값이 `음수` 혹은 `0`이 계산되므로 이때는 손익분기점 자체가 존재하지 않는다. 그래서 하단의 코드와 같은 조건을 붙여줘야 한다.

```python
# 나의 코드(성공)
a, b, c = map(int, input().split())

if c <= b:
    print(-1)
else:
    print((a // (c - b)) + 1)
```

```python
# 나의 시간 초과 코드(실패)
a, b, c = map(int, input().split())

total_cost = a    # 총 비용 = 고정 비용 + 가변 비용
total_income = 0    # 총 수입 = 판매 비용
cnt = 1
flag = True

while total_cost >= total_income:
    total_cost += b
    total_income += c
    cnt += 1
```

---
## 📍 백준 2775 - 부녀회장이 될테야
<a href='https://www.acmicpc.net/problem/1712'>백준 2775 - 부녀회장이 될테야</a>

## 💡 나의 풀이
이 문제는 `DP`, `재귀`로 풀 수 있지만, `DP`로 푸는방법이 시간이 훨씬 단축된다. `재귀`로 풀때는 `python3`에서 시간초과에 걸리므로 `pypy`로 제출해야한다.

DP 풀이방법이다. 
1. `0`층의 `i`는 `i`명이 살기때문에 제일 아래는 `[1, 2, 3, 4...]`다.
2. 문제는 층수가 증가 할때마다 이전 층수의 1호부터 b호까지 더한값을 사용해야하는데 이때 DP가 쓰인다.
3. `arr[i] += arr[i-1]`로 1호부터 b호까지 값을 누적시킨다.
4. 층수가 올라갈때는 3번 반복문 바깥에 하나 더 선언한다. `for _ in range(k)` 

재귀 풀이방법이다. `a: 층 `, `b: 호`
1. 하단의 사진처럼 `이전 index` + `아래 index`를 더해준다.
2. 종료 조건은 `a == 0: return b`,  `b == 1: return 1`이다.

![](https://images.velog.io/images/abcd8637/post/d973d547-fd08-4397-bf16-3f9557077e5d/KakaoTalk_Photo_2021-06-10-07-21-50.jpeg)

```python
# DP
T = int(input())

for _ in range(T):
    k = int(input())
    n = int(input())
    floor = [i for i in range(1, n+1)]

    for _ in range(k):
        for i in range(1, n):
            floor[i] += floor[i-1]
    print(floor[-1])

# 재귀
def check(a, b):
    if not a:
        return b
    if b == 1:
        return 1
    return check(a, b-1) + check(a-1, b)

for _ in range(int(input())):
    k = int(input())
    n = int(input())
    print(check(k, n))
```

---
## 📍 백준 3053 - 택시 기하학
<a href='https://www.acmicpc.net/problem/3053'>백준 3053 - 택시 기하학</a>

## 💡 나의 풀이
유클리드 기하학에서의 원의 넓이와 택시 기하학에서의 원의 넓이를 구하는 방법이 다르지만 출력은 모두 소수 6번째자리까지 출력한다. `format`함수를 이용해 `0.6f`을 사용했다.

```python
r = int(input())
pi = 3.141592653589793
print('{0:0.6f}'.format(r*r*pi))
print('{0:0.6f}'.format(r*r*2))
```

---
## 📍 백준 10833 - 사과
<a href='https://www.acmicpc.net/problem/10833'>백준 10833 - 사과</a>

각 `학교의 사과 개수 % 학생 수`를 누적시켜주면 된다.

## 💡 나의 풀이
```python
n = int(input())
rest = 0

for _ in range(n):
    student, apple = map(int, input().split())
    rest += (apple % student)
print(rest)
```

---
## 📍 백준 5554 - 심부름 가는 길
<a href='https://www.acmicpc.net/problem/5554'>백준 5554 - 심부름 가는 길</a>

## 💡 나의 풀이
입력값을 초로 받았기 때문에 이를 분, 초로 변환해주면 된다. 이때 `divmod`를 사용해서 몫과 나머지를 한번에 구했다.

```python
time = sum([int(input()) for _ in range(4)])
print('\n'.join(map(str, divmod(time, 60))))
```

---
## 📍 백준 5086 - 배수와 약수

<a href='https://www.acmicpc.net/problem/5086'>백준 5086 - 배수와 약수</a>

## ⚡️ 나의 풀이
배수와 약수의 관계를 파악하는 문제다. 기준을 너무 첫번째 숫자로만 잡아서 생각이 고착되어있던것 같다. 나의 풀이는 다음과 같다.

1. 두 수를 대소비교한다.
2. `a < b`일 때는 `b`를 기준으로 약수를 구하고 `a`가 `b`의 약수와 같다면 `약수(factor)`이고 반복문을 다 돌았는데도 찾지 못하면 `neither`이다.
3. `a > b`일 때는 `a`를 기준으로 약수를 구하고 `b`가 `a`의 약수와 같다면 `배수(multiple)`이고 반복문을 다 돌았는데도 찾지 못하면 `neither`이다.
4. `a == b`인 경우는 없다.

이렇게 안해도 다른 사람은 더욱 쉽게 구현했다.
1. `a % b == 0`이면 `a >= b`이고 (이때, `a != b`), `a`는 `b`의 `배수(multiple)`다.
2. `b % a == 0`이면 `b >= a`이고 (이때, `a != b`), `a`는 `b`의 `약수(factor)`다.

```python
# 나의 코드 
def check(a, b):
    if a < b:
        for i in range(1, b//2 + 1):
            if not b % i and a == i:
                return 'factor'
        return 'neither'
    else:
        for i in range(1, a//2 + 1):
            if not a % i and i == b:
                return 'multiple'
        return 'neither'


while True:
    a, b = map(int, input().split())
    if a == 0 and b == 0:
        break
    print(check(a, b))
```

```python
# 다른 사람의 코드
while True:
    a, b = map(int, input().split())
    if not a and not b:
        break
    if not a % b:
        print('multiple')
    elif not b % a:
        print('factor')
    else:
        print('neither')
```

---
## 📍 백준 2292 - 벌집

<a href='https://www.acmicpc.net/problem/2292'>백준 2292 - 벌집</a>

## ⚡️ 나의 풀이
`계차수열`을 수학적으로 구현 할 수 있는지 묻는 문제이다. 규칙을 자세히보면 `1, 7, 19, 37, 81...`인데 여기서 계차는 `6의 배수만큼 증가`한다.
즉, `equation = equation + (6 * i)`에서 결과값에 `+1`씩 더한 값이 된다. 하지만 반복문 안에서 `+1`을 넣으면 `+1`이 들어간채로 누적되기때문에 조건절에서 `+1`을 넣고 `n`과 비교했다.

다른 사람의 풀이를 봤는데 `while`문으로 간단하게 풀었다. 놀랐다. `cnt`를 따로 쓸 생각을 하지 않고 `i`값으로 출력 할수도 있구나라는 생각을 했다. 그리고 왜 `1`일때의 조건은 따로 안넣어줬는지 의문이 생겼는데, `1`일때는 `while`문에 걸리지 않기때문에 생략했다. 왜 그 생각을 하지 못했을 까? (입틀막 🤭 🤭)

```python
# 나의 풀이
n = int(input())
equation = 0
cnt = 1

if n == 1:
    print(1)
else:
    for i in range(1, 100000):
        equation = equation + (6 * i)
        cnt += 1
        if n <= equation + 1:
            print(cnt)
            break
```

```python
# 다른 사람의 풀이
n = int(input())
room = 1
cnt = 1

while n > room:
    room = room + (6 * cnt)
    cnt += 1
print(cnt)
```