## 📍 코드업 100문제를 풀면서 알아두면 좋을 팁들
1. 무조건 소숫점 n번째자리까지 출력하는문제는 `'%.nf'`를 쓰자.
2. `bool()`형태`(True, False)`로 반환할 때는 `bool(n)`을 사용하자.
3. python 정수형에서 `0(False)`을 제외한 나머지는 `True다`.
4. `0 and 0 == False`
5. AND(&), OR(|), XOR(^), NOT(~)
6. 한 줄 비교식 `print(a if a > b else b)`
7. 문제에서 나올수 있는 모든 경우 => `brute force(무작위 대입)`을 떠올리기
8. 입력값을 16진수로 바꾸기 `n = int(input(), 16)`

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
<a href='https://codeup.kr/problem.php?id=6070'> 코드업 - 6070, 월 입력받아 계절 출력하기</a>

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
<a href='https://codeup.kr/problem.php?id=6074'> 코드업 - 6074, 문자 1개 입력받아 알파벳 출력하기</a>

`while`문에 시작과 끝을 잘 넣어주면 된다.
```python
alphabet = ord(input())
t = ord('a')
while t<= alphabet:
    print(t)
    t+=1
```

<a href='https://codeup.kr/problem.php?id=6079'> 코드업 - 6070, 언제까지 더해야 할까?</a>

`while`문에 조건을 세울 때 언제 `while`문을 벗어나지?를 잘 생각할수 있었던 문제였다.

>1. `while S < N`일 경우:  S >= N, S가 N보다 크거나 같을 때 탈출
>2. `while S <= N`일 경우:  S > N, S가 N보다 클때만 탈출

처음에는 `while S != N`를 작성했는데, 파이참에서는 결과값이 잘 나왔는데 코드업에서는 시간초과 판정이 나왔다. number를 계산할때는 부등호를 자주 이용하자.

---
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
<a href='https://codeup.kr/problem.php?id=6083'>코드업 6083 - 빛 섞어 색 만들기</a>

모든 경우의 조합이라는 문제가 나왔을 때 `combination(조합)`을 사용하는 것이 아닌 경우의 수를 찾는 문제(`brute force`)이다.

또 색의 가짓수가 모두 몇 개인지 계산할 때는 각각 경우의 수를 모두 곱해주면 된다.
예를 들어 RGB의 각각 경우의 수가 3개라고 가정하면, 모든 경우의 수는 27가지가 된다.