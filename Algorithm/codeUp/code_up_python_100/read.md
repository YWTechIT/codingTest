## ✏️ 서론
백준 알고리즘을 풀다가 조금 어렵다고 생각되어, 기본을 다시 다져보자는 의미에서 코드업의 `python 기초 100제`를 풀어보았다. 

문제를 풀면서 기존에 알고 있었던 내용들은 과감하게 삭제했고 내가 모르는 문제 혹은 앞으로 비슷한 유형이 나왔을 때 어떤 방법으로 접근해야할지 알아야겠다 싶은 문제들을 작성해봤다.

---
## ✏️ 본론

### 📍 코드업 100문제를 풀면서 알아두면 좋을 팁들
1. 무조건 소숫점 n번째자리까지 출력하는문제는 `'%.nf'`를 쓰자.
2. `bool()`형태`(True, False)`로 반환할 때는 `bool(n)`을 사용하자.
3. python 정수형에서 `0(False)`을 제외한 나머지는 `True다`.
4. `0 and 0 == False`
5. AND(&), OR(|), XOR(^), NOT(~)
6. 한 줄 비교식 `print(a if a > b else b)`
7. 문제에서 나올수 있는 모든 경우 => `brute force(무작위 대입)`을 떠올리기
8. 입력값을 16진수로 바꾸기 `n = int(input(), 16)`
9. 소수점 n번째 자리까지의 정확도로 출력 = `round()`, 소수점 n번째 자리에서 반올림하여 n째 자리까지 출력 = `%.nf %round()`
10. 이전에 만든 수열을 사용 할 때는 1부터 n까지, 초항이 정해져있다면 2, n+1까지

---
## 💡 비트시프트 연산(bit shift calculate)
1. 비트의 위치를 이동시키는 연산
2. 곱하기, 나누기보다 쉬프트 연산이 빠를 때 종종 사용된다.
3. ` << `: 각 비트를 왼쪽으로 옮긴다(*2와 같음)
4. ` >> `: 각 비트를 오른쪽으로 옮긴다(/2와 같음)
5. python에서는 실수(float)에 대한 비트연산자는 허용되지 않고 오류가 발생한다.(본래 실수 값도 동일하게 컴퓨터 내부적으로 2진수 형태로 저장된다.)
6. 1을 3번만큼 밀게되면(`1<<3`), `1(2) -> 1000(2)`가 된다.

```python
# 10 = 1010(2)
# n<<1 = 10100(2), n>>1 = 101(2)
n = 10

print(n<<1, n>>1)
👉🏽 10 20
```

---
## 💡 논리연산자
기준: `bool(True, False)`

1. 모두 True일 때만 True출력(`a and b`)
2. 서로 다를 때에만 True 출력(`a ^ b`, XOR)
3. 서로 같을때에만 True 출력(`a == b`, `a == True and b == True`)
4. 모두 False일 때 True 출력(`not(a or b)`, `a == False and b == False`)

```python
# 1. AND(&)
print(bool(int(a)) and bool(int(b)))

# 2. XOR(^)
print(a ^ b)

# 3. ==
print(a == True and b == True)

# 4. not, or
print(a == False and b == False)
```

---
## 💡 세 개의 수 비교하기
변수 a, b, c가 주어졌을 때 이 중 제일 큰 값을 찾기위해서는 다음과 같은 조건이 있다.
>1. a와 b를 비교했을 때 더 큰 값을 c와 비교한다.
>2. a와 c를 비교했을 때 더 큰 값을 b와 비교한다.
>3. b와 c를 비교했을 때 더 큰 값을 a와 비교한다.

제일 작은 값을 찾기위한 방법은 위 과정의 대소관계를 반대로 실행하면 된다.
>1. a와 b를 비교했을 때 더 작은 값을 c와 비교한다.
>2. a와 c를 비교했을 때 더 작은 값을 b와 비교한다.
>3. b와 c를 비교했을 때 더 작은 값을 a와 비교한다.

```python
# 1. 제일 큰 값 찾기
print((a if a > b else b) if (a if a > b else b) > c else c)

# 2. 제일 작은 값 찾기
print((a if a < b else b) if (a if a < b else b) < c else c)
```

---
## 💡 비트단위 논리연산
1. 4bytes -> 32bits
2. 부호비트가 양수(0)일 때 최대값 표현은 `2^31 -1` 만큼
3. 부호비트가 음수(1)일 때 최대값 표현은 `2^31` 만큼
4. 1byte 기준: -1은 음의 정수 중 가장 큰 값이므로 이진표현에서도 가장 큰값(`1111`), 음의 정수 중 가장 작은값은 이진표현의 가장 작은 값 -8(`1000`) 
5. 32 비트형의 정수 0은 `0*32`, 그리고 -1은 0에서 1을 더 빼고 32비트만 표시하는 형태이므로 `1*32`, -2는 여기서 1만 더 빼면된다 `1*31,0`
6. `~n = -n-1` => `~n = -(n+1)`
7. 비트단위 연산은 빠른 계산이 필요한 그래픽처리에서 마스크연산(특정 부분을 가리고 출력하는)을 수행하는 데에도 효과적으로 사용된다.
8. 비트단위 연산(^,XOR)은 두 장의 이미지를 겹쳤을 때 색이 서로 다른 부분만 처리할 수 있다.(배경이 되는 그림과 배경 위에서 움직이는 그림이 있을 때, 차이점 확인가능)
9. 네트워크에 연결되어 있는 두 개의 컴퓨터가 데이터를 주고받기 위해 같은 네트워크에 있는지 아닌지를 판단할 때 bitwise 연산자 &를 사용하면 된다. 
A = 192.168.0.31 : 11000000.10101000.00000000.00011111
B = 255.255.255.0 : 11111111.11111111.11111111.00000000

A & B
192.168.0.0 : 110000000.10101000.0000000.00000000

>reference: <a href='https://www.youtube.com/watch?v=yHBYeguDR0A'> 비트연산 완전정복 - 엔지니어대한민국</a>

---
## 📌 기억에 남았던 문제

### 1️⃣ 코드업 6070 - 월 입력받아 계절 출력하기
<a href='https://codeup.kr/problem.php?id=6070'>코드업 6070 - 월 입력받아 계절 출력하기</a>

주어진 월을 입력받으면 어떤 계절인지 출력하는 문제인데, 본래 범위로 구현(3 <= n <= 5: print('spring'))하려 했으나, 해당수를 3으로 나눴을 때 몫이 얼마인지에 따라 구분이 가능하다는것이 신기했다. 이 문제와 비슷한 조건이 나중에 등장하면 꼭 써먹어야겠다.
```python
n = int(input())

# 3, 4, 5월
if n//3 == 1:
    print('spring')

# 6, 7, 8월
elif n//3 == 2:
    print('summer')

# 9, 10, 11월
elif n//3 == 3:
    print('fall')

# 12, 1, 2월
else:
    print('winter')
```

---
### 2️⃣ 코드업 6071 - 0이 입력 될 때까지 무한 출력하기
<a href='https://codeup.kr/problem.php?id=6071'> 코드업 - 6071, 0이 입력 될 때까지 무한 출력하기</a>

`while`문을 써서 0이 입력 됐을 때 종료하는 문제인데 사용 가능한 방법이 많아서 여기에 적게되었다.

```python
# 1번
while True:
    n = int(input())
    if n == 0:
        break
    else:
        print(n)

# 2번
n = 1
while n != 0:
    n = int(input())
    if n == 0:
        break
    print(n)

# 3번
n = 1
while n != 0:
    n = int(input())
    if n!=0:
        print(n)     
```

---
### 3️⃣ 코드업 6072 - 정수 1개 입력받아 카운트다운 출력하기
<a href='https://codeup.kr/problem.php?id=6072'> 코드업 - 6072, 정수 1개 입력받아 카운트다운 출력하기</a>

다음 코드처럼 조건을 `while`문에다 붙여주면 짧고 간결하게 사용가능하다.

```python
# 1번
n = int(input())

while n != 0:
    print(n)
    a-=1

# 2번
n = int(input())
while True:
    print(n)
    n-=1
    if n < 1:
        break
```

---
### 4️⃣ 코드업 6074 - 문자 1개 입력받아 알파벳 출력하기
<a href='https://codeup.kr/problem.php?id=6074'> 코드업 - 6074, 문자 1개 입력받아 알파벳 출력하기</a>

`while`문에 시작과 끝을 잘 넣어주면 된다.
```python
alphabet = ord(input())
t = ord('a')
while t<= alphabet:
    print(t)
    t+=1
```

---
### 5️⃣ 코드업 6079 - 언제까지 더해야 할까?
<a href='https://codeup.kr/problem.php?id=6079'> 코드업 - 6079, 언제까지 더해야 할까?</a>

`while`문에 조건을 세울 때 언제 `while`문을 벗어나지?를 잘 생각할수 있었던 문제였다.

>1. `while S < N`일 경우:  S >= N, S가 N보다 크거나 같을 때 탈출
>2. `while S <= N`일 경우:  S > N, S가 N보다 클때만 탈출

처음에는 `while S != N`를 작성했는데, 파이참에서는 결과값이 잘 나왔는데 코드업에서는 시간초과 판정이 나왔다. number를 계산할때는 부등호를 자주 이용하자.

---
### 6️⃣ 코드업 6081 - 16진수 구구단 출력하기
<a href='https://codeup.kr/problem.php?id=6081'> 코드업 - 6081, 16진수 구구단 출력하기</a>

평소 9단까지 구구단 출력하는 식만 작성해봤는데 16진수를 작성하려니까 생각해야 할 부분들이 많았다. 또, 전체 식을 출력하는게 아닌 입력 값의 단수만 출력해야하는데 이중 반복문을 사용했는데 조금 헷갈렸다. 

다른사람의 풀이를 보니까 입력값의 단수만 출력하므로 반복문을 하나만 작성하여 풀었는데 구구단은 이중 반복문으로 설정해야 제 맛이지!라고 했던 나의 생각을 바꿔주는 꽤 신선한 충격이었다.

또 하나 팁은 `(ord(input()) - 55)`를 사용하는것보다 `n = int(input(), 16)`을 사용하는것이 훨씬 범용성이 좋다는것이다. 입력조건에서 A ~ F까지만 입력한다고 나와있어 ord()를 썼는데, 앞으로는 후자를 사용해야겠다.

```python
n = int(input(), 16)

# 방법 1
n = ord(input()) - 55)

for i in range(N, N+1):
    for j in range(1, 16):
        print('%X*%X=%X' %(N, j, N*j))

# 방법2
n = int(input(), 16)

for i in range(1, 16):
    print('%X*%X=%X' %(n, i, n*i))
```

---
### 7️⃣ 코드업 6082 - 3 6 9 게임이 왕이 되자
<a href='https://codeup.kr/problem.php?id=6082'>코드업 6082 - 3 6 9 게임이 왕이 되자</a>

`1부터 n+1`범위에서 `3, 6, 9`가 들어간 수가 있으면 `X`로 표현하는 문제인데, 2가지 방법으로 나눠서 풀었다.
>1. i를 10으로 나눴을때의 나머지를 3, 6, 9로 설정할 때
>2. i를 str()형으로 바꾸고 3, 6, 9를 포함할 때

```python
# 1번
n = int(input())

for i in range(1, n+1):
    if i % 10 == 3 or i % 10 == 6 or i % 10 == 9:
        print('X', end=' ')
    else:
        print(i, end= ' ')

# 2번
n = int(input())

for i in range(1, n+1):
    if '3' in str(i) or '6' in str(i) or '9' in str(i):
        print('X', end=' ')
    else:
        print(i, end=' ')
```

---
### 8️⃣ 코드업 6083 - 빛 섞어 색 만들기
<a href='https://codeup.kr/problem.php?id=6083'>코드업 6083 - 빛 섞어 색 만들기</a>

모든 경우의 조합이라는 문제가 나왔을 때 `combination(조합)`을 사용하는 것이 아닌 경우의 수를 찾는 문제(`brute force`)이다.

또 색의 가짓수가 모두 몇 개인지 계산할 때는 각각 경우의 수를 모두 곱해주면 된다.
예를 들어 RGB의 각각 경우의 수가 3개라고 가정하면, 모든 경우의 수는 27가지가 된다.

---
### 9️⃣ 코드업 6091 - 함께 문제 푸는 날
<a href='https://codeup.kr/problem.php?id=6091'>코드업 6091 - 함께 문제 푸는 날</a>

최소공배수로 푸는 문제인데 gcd함수를 선언하지 않아도 `while`문을 통해 간편하게 풀 수 있는 문제였다. 사실 `while`문으로 푸는 방법을 몰랐는데 이렇게 풀 수도 있구나라는 생각이 들면서 신기했다.

이전에 `while`문의 조건을 공부하면서 
>1. `while S < N`일 경우:  S >= N, S가 N보다 크거나 같을 때 탈출
>2. `while S <= N`일 경우:  S > N, S가 N보다 클때만 탈출

`while`문에 `or`, `and`가 들어갈 때도 탈출할 때는 반대라는걸 떠올리지 못했다.

`while d%a != 0 or d%b != 0`의 코드는 `d를 a로 나눈 나머지가 0일 때 동시에(and) d를 b로 나눈 나머지가 0일 때` 탈출한다라고 생각하면 편하다.

```python
a, b, c = map(int, input().split())

d = 1
while d%a != 0 or d%b != 0 or d%c != 0:
    d+=1
print(d)
```

---
### 1️⃣0️⃣ 코드업 6092 - 이상한 출석 번호 부르기1
<a href='https://codeup.kr/problem.php?id=6092'>코드업 6092 - 이상한 출석 번호 부르기1</a>

여러개의 값을 하나로 묶었다가 다시 사용할 필요가 있을 때 `list`형태로 만들어 사용할 수 있다. 일종의 참조번호 형식으로 사용하면 편리하다.

대표적으로 `계수 정렬(count sort)`에 사용할 수 있는데, 일반적으로 가장 큰 데이터와 가장 작은 데이터의 차이가 `1,000,000`을 넘지 않을 때 효과적으로 사용할 수 있다.


```python
n = int(input())
array = list(map(int, input().split()))
d = [0 for i in range(24)]

for i in range(n):
    d[array[i]] += 1

for i in range(1, 24):
    print(d[i], end=' ')
```

---
### 1️⃣1️⃣ 코드업 6095 - 바둑판에 흰 돌 놓기
<a href='https://codeup.kr/problem.php?id=6095'>코드업 6095 - 바둑판에 흰 돌 놓기</a>

19 * 19크기의 바둑판 위에 n개의 흰 돌을 올려놓고 n개의 흰 돌이 놓인 위치를 출력하는 문제이다. 

조금 난이도가 있어보이지만, 사실 잘 분석해보면 금방 이해할 수 있다.
2차원 배열을 초기화시킨 다음 입력에 들어오는 2개의 수를 x, y로 선언하고 해당 좌표의 값을 1로 바꿔주면 흰 돌이 올라가있는 점과 동일하게 적용할 수 있다.

다만, 2차원 배열을 초기화할때는 `board = [[0] * 20]] * 20`으로 하지말고 `board = [[0]*20 for i in range(20)]`으로 선언해주자.

또, 마지막 바둑판을 출력할 때는 범위를 정해놓고 반복문을 작성하면 원하는 보기형태로 출력된다.

```python
n = int(input())
go_board = [[0] * 20 for i in range(20)]

for i in range(n):
    x, y = map(int, input().split())
    go_board[x][y] = 1

for i in range(1, 20):
    for j in range(1, 20):
        print(go_board[i][j], end=' ')
    print()
```

---
### 1️⃣2️⃣ 코드업 6096 - 바둑알 십자 뒤집기
<a href='https://codeup.kr/problem.php?id=6096'>코드업 6096 - 바둑알 십자 뒤집기</a>

문제에 나와있는 예시를 활용해서 문제를 풀려다가 `list index out of range` 판정을 무지 받았다. 예시보다는 내가 편한방법을 사용해야겠다.

먼저, 2차원의 리스트값을 하나하나씩 받아야하기 때문에 `input`을 사용했다.

다음으로 `x, y`값을 받고 해당 좌표가 0이면 1로, 1이면 0으로 바꾸도록 설정했다.
이 때 주의할 점은 범위가 0부터 시작하기 때문에 바꾸고 싶은 좌표위치에 -1을 꼭 해줘야한다. 그렇지 않으면 범위초과 판정이난다.

```python
d = [list(map(int, input().split())) for i in range(19)]

n = int(input())

for i in range(n):
    x, y = map(int, input().split())
    for j in range(19):
        if d[j][y-1] == 0:
            d[j][y-1] = 1
        else:
            d[j][y-1] = 0

        if d[x-1][j] == 0:
            d[x-1][j] = 1
        else:
            d[x-1][j] = 0

for i in range(19):
    for j in range(19):
        print(d[i][j], end=' ')
    print()

```

---
### 1️⃣3️⃣ 코드업 6097 - 설탕과자 뽑기
<a href='https://codeup.kr/problem.php?id=6097'>코드업 6097 - 설탕과자 뽑기</a>

`list index out of range` 범위설정 때문에 시간을 많이 쏟은 문제였다. 막대를 올려놓은 곳은 1로 바꾸면 되는데, 정작 중요한 `j` 대신에 `l`로 넣는바람에 에러만 나왔었다. 디버그를 하니까 원인을 알 수 있었다. (디버그 쵝오)

```python
h, w = map(int, input().split())
n = int(int(input()))
array = [[0] * w for i in range(h)]

for i in range(n):
    l, d, x, y = map(int, input().split())
    if d == 0:
        for j in range(l):
            array[x-1][y+j-1] = 1
    else:
        for j in range(l):
            array[x+j-1][y-1] = 1

for i in array:
    print(' '.join(map(str, i)))
```

---
### 1️⃣4️⃣ 코드업 6098 - 성실한 개미
<a href='https://codeup.kr/problem.php?id=6098'>코드업 6098 - 성실한 개미</a>

2차원 배열을 활용하는 전형적인 구현문제이다.
개미가 오른쪽으로 움직이다가 벽을 만나면 아래쪽으로 움직여 가장 빠른 길로 움직일때의 코드를 작성하면 되는데, 개미가 밟은 자리는 값을 9로 변경해야한다.

`while True`문을 사용하면 되지만 경우의 수를 잘 따져봐야한다.
나는 이렇게 작성했다.

![](https://images.velog.io/images/abcd8637/post/70f1dfb2-be9d-46e8-b444-4d534f55269d/KakaoTalk_Photo_2021-03-15-21-20-12.jpeg)

개미가 2,2에서 시작한다고 했는데, 나는 `maze`선언을 0부터 했기때문에 1,1을 시작점으로 정했다.

또 개미가 먹이를 먹었을 때 먹었던자리도 9로 변경하고 `break`문을 사용하여 멈추게 하는것을 잊지말자.

```python
# 입력 값 설정
maze = [list(map(int, input().split())) for i in range(10)]

# 개미 시작점 설정
x, y = 1, 1
maze[1][1] = 9

while True:
    # 오른쪽 벽이 0일 때
    if maze[x][y + 1] == 0:
        y += 1
        maze[x][y] = 9

    # 오른쪽 벽이 1일 때
    elif maze[x][y + 1] == 1:
        if maze[x+1][y] == 1:
            break
        elif maze[x+1][y] == 2:
            x+=1
            maze[x][y] = 9
            break
        else:
            x += 1
            maze[x][y] = 9
    
    # 오른쪽 벽이 2일 때
    else:
        y += 1
        maze[x][y] = 9
        break

for i in maze:
    print(' '.join(map(str, i)))
```

---
## ✏️ 결론
이렇게해서 python 100제를 모두 풀어보았다.
풀기전에는 난이도가 어렵지 않으니까 하루만에 풀 수 있겠지라고 안일하게 생각했는데, 뒤로갈수록 시간이 조금 오래걸렸다. 특히 맨 마지막 성실한 개미는 90분정도 걸렸던것 같다. 😅 😅 좋았던 점은 기초적인 문법들을 다질 수 있었던 시간이 되었다. 또, 유일하게 다른사람의 코드를 보지않고 순전히 나의 힘으로만 작성했다는 점도 박수를 쳐주고 싶다.

이렇게 계속 기초를 쌓아가다보면 백준문제도 한번에 눈에 들어오지 않을까?
