##  📍 프로그래머스 연습문제 

---
## ⚡️ Level 1

### 📌 빈 리스트 반환시 팁
파이썬의 `bool` == `False`인 값 (`[]`, `{}`, `()`, `''`, `0`, `None`)은 or를 써서 다음과 같이 표현 할 수 있다.

```python
def test(arr):
    return arr or -1

arr([])
arr({})
arr(())
arr('')
arr(0)

👉🏽 -1
```

---
### 📌 unpacking, append 팁
1. `unpacking` 변수를 반복문에도 선언 할 수 있다.(따로 선언하지 않아도 됨.)
2. sorted 사용 후 원하는 변수를 append 한 줄에 쓸 수 있다.

```python
# 1번
for i, j, k in commands:
    result.append(sorted(array[i-1:j])[k-1])

# 2번(comprehension)
result = [sorted(array[i-1:j])[k-1] for i, j, k in commands]
```

---
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

---
### 📌 완주하지 못한 선수
`count`를 이용해서 풀려고 했지만, 정확도가 100% 나오지 않아 완벽하게 풀지 못했다.

4가지 풀이 방법이 있다.
>1. Counter
>2. Hash
>3. range(len())
>4. zip()

첫번째로 `Counter` 모듈을 선언해서 풀 수 있는데, `Counter`끼리는 더하거나 뺄 수 있다. 이번문제를 풀면서 처음 보는데 되게 유용한것 같다. 단 1줄로 답을 제출 할 수 있다 ~~(WOW)~~
```python
# Counter
from collections import Counter
def solution(participant, completion):
    return str(*(Counter(participant) - Counter(completion)))
```

두번째는 `Hash`값을 이용하는건데, 제한사항에 `completion의 길이는 participant의 길이보다 1 작습니다.`처럼, 값이 무조건 1개가 나오기때문에 `temp`에 `hash`값을 누적해주고, 참가자 `hash`값을 빼주면 결과적으로 남는 `hash`값에 키를 붙여주면 누군지 알 수 있다.
```python
# Hash
def solution(participant, completion):
    hash_dic = {}
    temp = 0

    for part in participant:
        hash_dic[hash(part)] = part
        temp += hash(part)

    for com in completion:
        temp -= hash(com)

    return hash_dic[temp]
```

세번째와 네번째는 푸는 방법이 비슷한데, 정렬해서 `index`를 하나씩 비교하다 다른 값이면 출력, 끝까지 돌았는데도 다른 값을 찾지 못했다면 `participant[-1]`을 출력하는 방법이다. 
```python
# range(len())
def solution(participant, completion):
    participant.sort()
    completion.sort()

    for i in range(len(participant) -1):
        if participant[i] != completion[i]:
            return participant[i]
    return participant[-1]
```

---
### 📌 전화번호 목록
배열안에 한 번호가 다른 번호에 포함되어있으면 `False`를, 포함되어있지 않다면 `True`를 반환하는 문제다.

### 💡 나의 풀이
결론적으로 완벽한 해답을 찾지 못했다. 😅 😅

첫번째는 현재값과 다음값을 비교하는 방법이었다.
배열을 정렬`(sort)`하고 `if array[i] in array[i+1]`을 생각했는데 정확성에서 100% 답이 아니었다. 왜냐면 현재 번호가 포함되어있는 다음 번호에서도 자릿수가 다른 경우`(['11', '1211)`가 있을 수 있기 때문이다. `질문하기`를 보니까 예전에는 통과한 코드인데, `21.3.4.`부로 테스트 케이스가 변경되면서 더 이상 통과하지 않는 코드가 되었다.

두번째는 해쉬(hash)값을 이용하는 방법이었다. 
`for문`으로 값을 하나하나씩 불러와서 0부터 hash값을 누적했을 때 다음 hash값과 동일하면 `False`, 아니면 `True`를 생각했다.
이때까지만 해도 `hash('119')`의 값과 `hash('11') + hash('9')`값은 동일하지 않을까?라고 생각했다. 왜냐면 문자열끼리 더하면 `'11'+9' = '119'`가 되니까... 지금 생각하면 엉뚱한 생각이지만, 문제 풀때까지만 해도 <span style='color:blue'>~~(와 나 천재?)~~ 라는 생각을 잠깐 했었다.</span>

---
다른 사람의 코드를 보고 잘 이해되는 코드가 2개 있었는데 다음과 같았다.
> `zip + startswith`, `hash값`

zip함수부터 살펴보면 풀이 방법은 다음과 같다.
>1. array와 array[1:]를 선언한다.
>2. 두개의 배열을 `정렬(sort)`시킨다.
>2. `zip`으로 하나씩 비교하면서 `array[1:]` 현재값이 `array` 현재값으로 시작한다면 `False`, 아니면 `True`

```python
# zip
def solution(phone_book):
    phone_book.sort()

    for prev, n in zip(phone_book, phone_book[1:]):
        if n.startswith(prev):
            return False
    return True
```

hash함수는 다음과 같다.
내가 풀려고 했던 두번째 방법과 비슷하지만, 조금 달랐는데 hash값을 더하는 대신 `key`값을 누적하면서 더했을 때 다른 값과 같은지 비교하는 방법이었다. 조금만 더 생각했으면 접근했을텐데 아쉬웠다.
그리고 이 코드의 마지막 `if`조건문을 이해하는데 시간이 필요했다. 
배열안에 여러개의 값이 들어있을 때 값을 찾으려면 배열안의 배열 그 자체를 하나의 원소로 취급하는데 어떻게 현재 값 `temp`가 다른 원소 `123`과 같을 수 있단 말인가?

예를 들어 `phone_book`이 다음과 같을 때 현재 `temp`가 12면 값을 찾을 수 없는 상태가 아닌가?
```python
phone_book = { '123': 1, '1235': 1, '567': 1, '88': 1}
current_value = '12'

print(current_value in phone_book)
👉🏽 False
```

그런데, 거꾸로 시야를 넓혀보면 금방 답을 찾을 수 있다.
예를 들어, 현재 number는 `1235` 이고 현재 `temp`가 `123`이라고 생각하면 이때는 `temp in hash_dic`이 성립한다.
앞 원소에만 집중한 나머지, 뒤의 `index`를 이용하여 `temp`를 만들 때 앞 `index`와 동일하다는것을 신경쓰지 못했다.

```python
# dict
def solution(phone_book):
    hash_dic = {}

    for i in phone_book:
        hash_dic[i] = 1
    
    for number in hash_dic:
        temp = ''
        for j in number:
            temp += j

            # temp가 현재 비교하려는 number와 같지않지만 다른 index에 존재할 때
            if temp != number and temp in hash_dict: 
                return False
    return True
```

------
### 📌 2016년
00월 00일처럼 날짜가 주어졌을 때 무슨요일인지 맞추는 문제이다.
처음에 생각한 방법은 1일부터 31일까지 쭉 나열하고 7일이 되면 한바퀴를 다 돌기때문에 7로 나눈 나머지가 0, 1, ... 7이면 해당요일을 출력하는 방법을 떠올렸다.

전체적인 방법은 벗어나지 않았지만, if문을 사용하지 않고 그냥 `요일[날짜]`처럼 작성하면 코드도 간결해진다.

그리고 `1월`의 요일만 구하는게 아니라 `1월 ~ 12월`의 요일도 구해야하므로 months라는 변수를 선언해 1~12월의 요일들을 리스트에 선언했다. 구하려고 하는 달(month)은 그 전까지의 달(month)의 합과 일(day)을 더한 값에 %7을 해주면 해당 요일이 나온다.
```python
def solution(a, b):
    months = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
    days = ['FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED', 'THU']
    
    return days[(sum(month[:a-1]) + b-1) % 7]
```


