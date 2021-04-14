### 📌 백준 13458 - 시험감독
<a href='https://www.acmicpc.net/problem/13458'>문제 설명</a>

### 💡 나의 풀이
문제가 생각보다 쉬워보는데?라고 했다가 왜 정답률이 `25%`인지 느낌이 왔다.

나는 이중반복문으로 작성했고, 계산 할 때마다 `cnt`가 1씩 증가하여 총 몇 명이 필요할까?를 계산했는데, `시간 초과`판정이 났다.
내가 작성했던 코드와 비슷한분들은 이중반복문을 사용하지 않는 다른 방법을 고민해야한다.

>1. `student`를 한명씩 가져온다.
>2. 모든 시험장에 들어가야하는 총 감독관은 1명만 사용하고 부 감독관은 여러 명 사용해도 된다.
>3. 먼저, `student`에서 총 감독관이 감시할 수 있는 응시자의 수를 모두 뺀다.
>4. 남은 응시자의 수에서 부감독관이 감시할 수 있는 응시자의 수로 나눈 몫을 사용한다.
>5. 이때, 나머지가 있으면 몫 +1, 나머지가 없으면 몫을 그대로 사용한다.
   * 여기서 `몫`은 응시생들을 감시할 때 부감독관이 몇 명 필요한지를 계산하는 과정이다.
   * 나머지가 있을때 몫에 1을 더하는 이유는, 감독해야하는 응시생이 남았기 때문에 부 감독관의 수를 한명 추가하는 것이다.
>6. cnt값에서 누적해준다
   * 처음 cnt는 N명인데, 이미 총 감독관이 한명씩 들어갔기때문에 N의 값을 초기에 선언해준것이다.

단순히 몫과 나머지를 구하면 `while`문 대신에 사용할 수 있는데, 왜 내가 풀땐 그게 떠오르지 않지?!?!?
아무튼, 비슷한 유형을 만나면 지금과 같은 방식으로 풀도록 기억해보자.

```python
# 공통 코드
import sys
input = sys.stdin.readline

N = int(input())
students = list(map(int, input().split()))
first_commander, second_commander = map(int, input().split())

# 내 코드(시간초과)
cnt = 0

for student in students:
    if student - first_commander > 0:
        student -= first_commander
        cnt += 1
        while student > 0:
            student -= second_commander
            cnt += 1
    else:
        while student > 0:
            student -= second_commander
            cnt += 1

print(cnt)

# 내 두번째 코드
cnt = N

# 총 감독관이 한명씩 들어가고 남은 응시생들을 계산하는 식
students = list(map(lambda x: x-first_commander, students))
for student in students:
    if student % second_commander:
        cnt += student // second_commander + 1
    else:
        cnt += student // second_commander
print(cnt)

# 다른사람의 코드 
cnt = N

for student in students:
    student -= first_commander
    if student % second_commander:
        cnt += student // second_commander + 1
    else:
        cnt += student // second_commander

print(cnt)
```