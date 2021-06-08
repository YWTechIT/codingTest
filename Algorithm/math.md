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

