##  📍 프로그래머스 연습문제 

---
## ⚡️ Level 1

### 📌 두 정수 사이의 합

### 💡 나의 풀이
문제를 보고 3가지 경우의 수를 판단했다.
1. a == b
2. a < b
3. a > b

`sum(range())`를 사용하면 간편하게 줄일 수 있었는데, 무심코 반복문을 사용해서 효율성을 극대화시키지 못할 뻔했다.

a가 b보다 크면, `swap`처리를 해준다. 이후, `sum(range())`를 사용하여 값을 계산해준다.

a와 b가 같으면, 0아니야? 라고 할 수도 있지만 마지막 값은 +1을 해줬기 때문에 입력값 그대로 리턴되는것을 알 수 있다.

```python
def solution(a, b):
    if a > b:
        a, b = b, a

    return sum(range(a, b+1)))
```

---
### 📌 문자열 다루기 기본
문제 설명에서 나온 조건은 무조건 사용하자.

### 💡 나의 풀이
숫자로만 구성되어있는지 확인하면 되는 문제라서 문자열만 들어있는 변수를 따로 만들고, 만약 `input`에 문자열이 포함되어있으면 `return False`를 하는 방법으로 만들었다.

한 가지 헷갈린 점이 있었다. 
문제 설명에 `s`의 길이가 4 혹은 6이라고 주어졌는데 제한 사항에도 s는 길이 1이상, 길이 8이하인 문자열이라고 적혀있었다. 처음에는 문제가 잘못 나온 줄 알았는데, 생각해보니까 입력은 1~8까지 주어지는데 출력해야하는 문자열의 길이는 4 혹은 6 이라는 얘기였다.

즉, 문자열이 4와 6일때만 함수를 실행하면 된다. 그래서 나는 `len(s) != 4 and len(s) != 6:`으로 풀었는데 해석하자면 `s`의 길이가 모두 4와 6이 아니면 `return False`를 한다는 의미다.

문제를 풀고 다른 사람의 코드를 봤는데 `try-except`로 푼 사람이 꽤 있었다. 
`try-except`를 사용해서도 다시 풀어봤다. 방금 푼 코드와는 조금 다르게 s가 `int()`형 일때만 `return True`하게 설정했다.

```python
character = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'

def check_string(s):
    if len(s) != 4 and 6:
        return False

    for i in s:
        if i in character:
            return False
    return True
```

```python
def check_string(s):
    if len(s) != 4 and 6:
        return False
    try:
        if int(s):
            return True
    except:
            return False
```

---
### 📌 소수 판별
기존에 나동빈 - 이코테 책에서 봤던 유형이었는데, 소수문제에는 2가지 유형이 있다.

>1. 입력값이 단순히 소수인지 판별할 때
>2. 입력 구간에서 소수값 출력

이 문제는 2번 유형에 가까운 문제였다.
1부터 n까지의 소수의 개수를 구하는 문제기 때문이다.

정답을 제출하고 다른사람의 코드를 보는데 신기한 코드가 있었다. `set`을 활용해서 반복문을 돌때마다 `i의 배수`만큼 빼주는 코드가 있었다. 

코드도 파이써닉했는데, 한눈에 이해가 되고 깔끔했다. 
앞으로 이렇게 코드를 작성하도록 노력해야겠다.

### 💡 나의 풀이
에라토스테네스의 체를 이용해 풀었다.
여기서 반복문의 범위를 2부터 제곱근까지 선언한 이유는 약수의 특징을 이용했는데, 예를 들어 10은 가운데 약수를 기준으로 대칭적으로 2개씩 앞뒤로 묶어서 곱하면 10이 된다.
(`1*10, 2*5, 5*2, 10*1`)

제곱근까지만 계산을 해주면 제곱근 뒤는 이미 앞에서 계산했기 때문에 `False`로 바뀐다. 시간복잡도면에서 효율적인 계산이다.

잠깐 팁인데, 제곱근은 다음의 유형으로 선언할 수 있다.
1. range(2, int(n**0.5) +1)
2. range(2, round(n**0.5) +1)
3. range(2, int(math.sqrt(n))+1)

이제 풀이방법을 보면
>1. `n+1`만큼 `True` 선언
>2. 2부터 제곱근까지 `array[i] == True`면, i의 배수만큼 array[i]를 False로 바꿔준다.
>3. 반복문을 통해 `False`로 바뀐 `index`를 출력하면 된다.

```python
# 나의 풀이
def solution(n):
    array = [True for i in range(n+1)]

    for i in range(2, int(math.sqrt(n))+1):
        if array[i]:
            j = 2
            while i * j <= n:
                array[i*j] = False
                j+=1

    result = [i for i in range(2, n+1) if array[i]]
    return len(result)
```

```python
# 방법 1
def solution(n):
    numbers = set(range(2, n+1))

    for i in range(2, int(n**0.5)+1):
        numbers -= set(range(2 * i, n + 1, i))

    return len(numbers)

# 방법 2
def solution(n):
    numbers = set(range(2, n+1))

    for i in range(3, int(n**0.5)+1):
        numbers -= set(range(i * i, n + 1, i))

    return len(numbers)
```

---
### 📌 문자열 내 p와 y의 개수
`lower()`, `count()` 함수를 써야한다고 인지했는데, 습관적으로 `for`문에 적용했다. 
하나의 문자열로 주어졌기때문에 `for`문을 사용하지 않아도 적용이 가능하다.

### 💡 나의 풀이
```python
# my_answer
def solution(s):
    s = s.lower()
    p, y = 0, 0
    for i in s:
        p += i.count('p')
        y += i.count('y')

    if p == y:
        return True
    return False
```

```python
# other_answer
def solution(s):
    return s.lower().count('p') == s.lower().count('y')
```