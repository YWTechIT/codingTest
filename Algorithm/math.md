##  📍 백준 10886 - 0 = not cute / 1 = cute
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

##  📍 백준 4153 - 직각삼각형
<a href='https://www.acmicpc.net/problem/4153'>백준 4153 - 직각삼각형</a>

### 💡 나의 풀이
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
