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

---
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
---
### 📌 체육복
체육복을 도난당한 학생에게 여벌의 체육복을 갖고있는 학생이 빌려주는 문제이다.
n = 전체 학생, reserve = 여벌의 체육복이 있는 학생, lost = 체육복을 잃어버린 학생

### 💡 나의 풀이
문제에서는 각각의 학생을 `key - value`의 형태를 띄고있는 `dictionary`가 아닌, 리스트로 주어졌다. 
전체 학생의 수가 5이면 `n = [1, 2, 3, 4, 5]` 또, 체육복을 빌려줄때는 바로 앞번호의 학생이나 뒷번호의 학생에게만 빌려 줄 수 있다고 했다. 그래서 `index`별로 값을 비교해서 나올수 있는 경우의 수를 분류했다.

여벌의 체육복을 빌려주는 경우의 수는 크게 2가지가 있다.
>1. `lost`가 `reserve`에 포함되지 않는 경우
  * `reserve[i] == lost[j]+1`이면 여벌의 체육복을 빌려 줄 수 있다.
  * `reserve[i] == lost[j]-1`이면 여벌의 체육복을 빌려 줄 수 있다.
>2. `lost`에 `reserve`가 포함되는 경우
  * 이때는 여벌 체육복을 가져온 학생이 체육복을 도난당했으므로, 다른 학생에게 체육복을 빌려 줄 수 없다. 따라서, reserve의 값은 사용할 수 없다.

마지막에는 
1. 전체 학생에서 잃어버린 학생을 빼주고(`rest`)
2. 여벌의 체육복을 빌려준 `reserve`는 잃어버린 학생(`lost`)의 값을 가지고 있으므로 (`borrow`)
3. `rest`와 `borrow`의 합집합을 구하면 체육복을 가지고 있는 학생의 최댓값을 구할 수 있다.

코드는 다음과 같다.
```python
def solution(n, lost, reserve):
    n = [i for i in range(1, n+1)]

    for i in range(len(reserve)):
        for j in range(len(lost)):
            if lost[j] in reserve:  # 여벌의 체육복을 가져온 학생이 도난당한 경우
                continue
            elif reserve[i] == lost[j] + 1 or reserve[i] == lost[j] - 1: # 여벌의 체육복을 빌려 줄 수 있는 경우
                reserve[i] = lost[j]
    
    rest = set(n) - set(lost)
    borrow = set(lost) & set(reserve)
    return len(rest | result)
```

---
### 📌 수박수박수
길이가 n인 '수박수박수...'와 같은 패턴을 갖고있는 문자열을 리턴하는 함수를 만드는 문제다.

정답판정을 받고 `다른 사람의 풀이`를 보니까 리스트 슬라이싱을 이용해 쉽게 풀었던 코드를 봤다. 나중에 써먹자.

### 💡 나의 풀이
`수박수박수..`와 같은 패턴을 띄는 문자열을 빈 리스트에 선언했다.
n의 길이가 `10,000`이하의 자연수이므로 범위를 `fruit = [0] * 10001`로 설정했다.

다음으로 홀수번째는 `수`, 짝수번째는 `박`이라는 패턴을 찾아냈다.
그래서 `fruit`리스트에 패턴을 넣어줬다.

그리고 n번만큼 리스트를 출력해 문자열(str)로 바꿔주었다.

```python
def solution(n):
    fruit = [0] * 10001
    fruit = ['수' if i % 2 == 0 else '박' for i in range(len(fruit))]
    return ''.join([fruit[i] for i in range(n)])
```

### 💡 다른 코드
리스트 슬라이싱을 이용해 코드를 작성했지만, 개인적으로 범위를 다시 설정했으면 더 좋은 코드가 됐을것 같다.

`n=3`이면 `s = 수박수박수박`이 될텐데 출력은 `수박수`까지만 필요하다. 
따라서, 범위 설정을 `(n//2+1)`로 해주면 `s = 수박수박`이 되므로 기존코드보다 메모리면에서 더 효율적이다.

```python
# 다른사람의 풀이
def solution(n):
    s = '수박' * n
    return s[:n]

# 다른사람의 풀이 수정코드
def solution(n):
    s = '수박' * (n//2+1)
    return s[:n]
```

---
### 📌 약수의 합
정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하자.

### 💡 나의 풀이
약수를 구하는것엔 3가지 방법이 있다.
1. 처음부터 `n`까지 약수 구하기
2. 처음부터 `n//2`까지 약수 구하기
3. 처음부터 `int(n**0.5)`까지 약수 구하기

이전에 <a href='https://velog.io/@abcd8637/python-level-1-소수판별'>소수 판별 문제</a>를 풀었을 때 범위를 제곱근까지만 구해서 소수를 구했었는데, 이번에는 2로 나눈값으로 구했다.

약수의 주요 특징은 자신을 제외한 가장 큰 약수는 `n//2`다.
예를 들어 `n = 12`일때는 자신을 제외한 가장 큰 약수는 6이고(`1, 2, 3, 4, 6, 12`) `n = 30`일때는 자신을 제외한 가장 큰 약수는 15다.(`1, 2, 3, 5, 6, 10, 15, 30`)

이처럼 범위를 `n // 2+1`까지만 구해주고 자기 자신을 더해주면 문제에서 요구하는 n의 약수를 모두 더한 값이 된다.

물론, 몫을 2로 나누지 않아도 정답판정이 나오지만 수가 커질수록 계산해야하는 수가 많아지게 된다.

제곱근으로 구할때는 다음의 성질을 이용한다.
`n = 12`일때, 제곱근(`int(n**0.5)`) == `3`까지 구한 약수 `1, 2, 3`을 이용해 `n//1 = 12`, `n//2 = 6`, `n//3 = 4`를 통해 약수를 구하면된다. 이때, 제곱수는 한번만 약수에 포함되야하므로 `if n != n//i:`를 붙여주었다.

만약 `n = 1,000,000`라면, `1000`번의 반복만으로 결과를 출력할 수 있으므로 시간복잡도가 현저하게 줄어듦을 확인 할 수 있다.


```python
# 1번
def solution(n):
    return sum([i for i in range(1, n+1) if n % i == 0])

# 2번
def solution(n):
    return n + sum([i for i in range(1, (n//2)+1) if n % i == 0])

# 3번
def solution(n):
    result = 0

    for i in range(1, int(n**0.5)+1):
        if n % i == 0:
            result += i
            if n != n//i: # 제곱 수는 한번만 넣기
                result += (n//i) 
    return result
```

---
### 📌 자릿수 더하기
int형으로 주어진 수의 각 자리수의 합을 더하는 문제이다.

### 💡 나의 풀이
`list comprehension`으로 사용해야겠다는 생각을 했는데, 값을 누적하는 코드(`result+=i`)를 어떻게 구현해야할지 잘 몰랐다. 그냥 `result` 빼고 나열된 원소를 `sum`으로 구하면된다.

한줄로 표현 할 수 있기 때문에, 2번과 3번은 알고있으면 많이 도움이 될 것 같다.

1. for문을 이용한 방법
2. list comprehension을 이용한 방법
3. map함수를 이용한 방법

```python
# 방법1
def solution(s):
    result = 0
    for i in str(s):
        result += int(i)
    return result

# 방법2
def solution(s):
    return sum([int(i) for i in str(s)])

# 방법3
def solution(s):
    return sum((list(map(int, str(s)))))
```

---
### 📌 정수 내림차순으로 배치하기
자리수를 큰 것부터 작은 순으로 정렬한 새로운 정수를 리턴하라.
예를들어 n이 118372면 873211을 리턴하면 됩니다.

### 💡 나의 풀이
이전에 풀었던 자리수 더하기 문제와 비슷하게 자리수를 정렬하려면 `문자형(str)`으로 접근하는것이 핵심포인트다.
이후, `sorted`를 사용해 정렬하고 나중에는 `''.join`을 이용해 하나로 뭉쳐줬다. 하지만 문제에서 정수로 리턴하라고 했기때문에 `int`형을 다시 붙여줘야한다.

다른 사람의 코드를 보며 배운 점은, `sorted`를 사용하면 `list`를 자동으로 반환해주기 때문에 따로 `list`를 선언 할 필요가 없다는 점이었다. 또, `map` 함수를 사용하지 않았는데 이유는 `str`을 바로 `int`형으로 바꿔주지 않고 제일 마지막에 `int`형으로 바꿔주기때문에 사용하지 않았다.

`list, map`만 빠져도 이전보다 간결한 코드가 되기 때문에 가독성이 좋아지는것을 확인 할 수 있다.

```python
# 나의 코드
def solution(n):
    return int(''.join(sorted(list(map(str, str(n))), reverse=True)))

# 다른사람의 코드
def solution(n):
    return int(''.join(sorted(str(n), reverse=True)))
```

---
### 📌 콜라츠 추측
주어진 수가 1이 될 때까지 다음 작업을 반복하면, 모든 수를 1로 만들 수 있다는 추측이다.

1. 입력된 수가 짝수라면 2로 나눕니다. 
2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
3. 결과로 나온 수에 같은 작업을 1이 될 때까지 반복합니다.

### 💡 나의 풀이
이전에 백준인가 어디서 한번 풀어봤던 문제였다.
`while`문을 사용하면 쉽게 해결 할 수 있다.

해결 과정은 다음과 같다.
>1. n이 짝수 일 때, 기존 n에 2로 나눈 몫을 n으로 저장한다.
>2. n이 홀수 일 때, 기존 n에 3을 곱하고 1을 더한 n으로 저장한다.
>3. 1번과 2번의 과정을 거쳤다면 cnt를 1 증가시킨다.
>4. 만약, cnt가 500번 이상일때는 -1을 반환시키고 종료한다.
>5. n이 1보다 작거나 같아진다면 `while`문을 종료시킨다.

`JS`도 마찬가지로 구현해주면 된다. 특이점은 삼항연산자를 이용했다.

```python
# python 코드
def solution(n):
    cnt = 0
    while n > 1:
        if n % 2 == 0:
            n //= 2
        else:
            n = (n * 3) + 1
        cnt+=1
        if cnt >= 500:
            return -1
    return cnt

print(solution(626331))
```

```javascript
// JS코드
function solution(num){
    let cnt = 0;
    while (num > 1){
        num % 2 ? (num = num * 3 + 1) : (num /= 2);
        cnt += 1;
        if (cnt > 500){
            return -1;
        }
    }
    return cnt
}
```

---
### 📌 제일 작은 수 제거하기
`arr`에서 가장 작은 수를 제거한 배열을 리턴하는 함수를 완성하라.
단, 리턴하려면 배열이 빈 배열일 경우 `[-1]`을 리턴하라.

### 💡 나의 풀이
가장 작은 수를 제거할 때는 다음과 같은 방법이 있다.
>1. `sorted`함수로 오름차순 / 내림차순으로 정렬한 뒤 맨 앞 / 뒤 원소를 제거하기
>2. `min`함수로 제일 작은 값을 찾아 해당 원소만 제거(remove)하기

문제에서는 n의 범위가 주어지지 않았지만, 시간복잡도를 고려해서 2번으로 선택했다.
`sorted`함수의 시간복잡도는 `O(NlogN)`이고, `max/min` 함수의 시간복잡도는 `O(N)`이기 때문이다.
<a href='https://wiki.python.org/moin/TimeComplexity'>자료구조 별 시간복잡도: 파이썬 공식문서</a>

`remove`함수는 원소 제거 후 `empty`면 빈 배열을 반환한다.

다른사람은 `comprehension`으로 구현했는데 `i`는 제일 작은 원소보다 큰 값만 리스트로 리턴하게 짰다.
또, `return [] or -1`의 코드는 `True`값을 `return`하게 되어있는데, 이는 `빈 배열([])`은 `False`이고 `-1`은 `True`이기 때문이다. 

글을 작성하다가 다시 한번 풀어보니까 가장 작은 값이 중복되는 케이스 (`[1, 1, 2, 3]`)는 내 코드가 틀렸다는것을 알 수 있다. 이때는 다른사람의 코드가 정답이 되므로 예외케이스도 꼭 생각해서 풀어야겠다.

```python
# 내 코드
def solution(arr):
    arr.remove(min(arr))

    if not arr:
        return [-1]
    return arr

# 다른사람의 코드
def solution(arr):
    return [i for i in arr if i > min(arr)] or [-1]
```

---
### 📌 하샤드 수
양의 정수 x가 x의 자릿수의 합으로 x가 나누어져야 하는 문제이다.
예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 

### 💡 나의 풀이
이전에 풀었던 `자릿수 더하기`와 `제일 작은 수 제거하기` 문제와 비슷한 방식으로 접근하면 되는데, 마지막에 `x % harshad == 0`으로 떨어지면 `True`를 리턴하면 된다.

다른사람의 코드를 보며 배운점은 `return x % harshad == 0`의 코드는 `harshad`이 0이면 `True`, 아니면 `False`를 반환하는 간결한 코드이다.

```python
# 내 코드
def solution(x):
    harshad = sum(list(map(int, str(x))))
    if x % harshad == 0:
        return True
    return False

# 다른사람의 코드
def solution(x):
    return x % sum(list(map(int, str(x)))) == 0
```

---
### 📌 행렬의 덧셈
행과 열의 크기가 같은 2차원의 두 행렬을 서로 더한 결과를 반환하는 문제이다.

### 💡 나의 풀이
1차원 리스트를 더할 때는 어렵지 않았는데, 2차원끼리 더하려고 하니까 조금 어려웠다.
나는 `zip`함수를 사용했는데, `temp`에 `zip`으로 꺼내온 원소들을 더하고 빈 리스트에 `append`시켰다. 한 번 돌게되면 `temp`를 다시 빈 리스트로 초기화 시키게끔 작성했다. 이 코드는 `for range(len)`문을 사용하는것보다 코드의 길이가 아주 조금 줄었지만 가독성이 좋다고 생각하지 않았다.

다른 사람의 코드 중 `map`과 `zip(*x)`를 활용한 코드가 마음에 들었다. 
`map`은 리스트의 요소를 지정된 함수로 처리해주는 함수이다. 프로그래머스 문제를 풀다보면 많이 접하는 함수이다.

`zip`은 동일한 개수로 이루어진 자료형을 묶어주는 역할을 하는데, 인자를 1개로 받게되면 `([1, 2], [3, 4])`, `([2, 3], [5, 6])` 처럼 동일한 `index`값들을 튜플로 하나로 묶어준다.

`*(asterisk)`는 보통 다음과 같은 상황에서 사용되는데 여기서는 `unpacking`의 목적으로 사용되었다.
1. 곱셈 및 거듭제곱 연산으로 사용할 때
2. 리스트형 컨테이너 타입의 데이터를 반복 확장하고자 할 때
3. 가변인자 (Variadic Arguments)를 사용하고자 할 때
4. 컨테이너 타입의 데이터를 Unpacking 할 때

이 코드의 풀이 순서는 다음과 같다.
>1. `for x in zip(arr1, arr2)`: `([1, 2], [3, 4])`, `([2, 3], [5, 6])`
>2. `map(sum, zip(*x))`: `unpacking`한 값(`[1, 2], [3, 4]`, `[2, 3], [5, 6]`)에서 동일한 `index`끼리 더해준(sum) 값을 다시 리스트에 담는다.
>3. 출력: [[4, 6], [7, 9]]

<span style='color:blue'>zip을 사용할때는 *(asterisk)를 잘 활용하자!</span>

```python
# 내 코드 1
def solution(arr1, arr2):
    result = []
    for i, j in zip(arr1, arr2):
        temp = []
        for k, m in zip(i, j):
            temp.append(k+m)
        result.append(temp)
    return result

# `내 코드 1`을 comprehension으로 작성한 코드
def solution(arr1, arr2):
    return [[k+m for k, m in zip(i,j)] for i, j in zip(arr1, arr2)]

# 다른 사람의 코드
def solution(arr1, arr2):
    return [list(map(sum, zip(*x))) for x in zip(arr1, arr2)]
```

---
### 📌 자연수 뒤집어 배열 만들기
`12345`를 `[5,4,3,2,1]`로 만들면 된다.

### 💡 나의 풀이
문제를 풀면서 배운점이 있는데, `reverse`와 `reversed`의 차이점이다.
`sorted` 사용할 때만 `reversed`를 사용했었는데, 이런 차이점이 있는것은 몰랐다. 이제부터 까먹지 않도록 잘 외워놔야겠다.

> `array.reverse()`: `list`에서만 사용가능하다.
> `reversed(seq)`: 메서드(method)나, 시퀀스(sequence)를 지원하는 객체에서 사용 가능하다.
  * `sequence(시퀀스)`: str(문자형), list(리스트), tuple(튜플)

참고로 `reverse`, `reversed` 모두 시간복잡도는 `O(N)`이다.

reference: 
1. <a href='https://docs.python.org/3/library/array.html?highlight=reverse#array.array.reverse'>파이썬 공식문서 - reverse </a>
2. <a href='https://docs.python.org/3/library/functions.html?highlight=reverse%20reversed#reversed'>파이썬 공식문서 - reversed </a>

```python
# 내 코드
def solution(n):
    return list(map(int, list(str(n))[::-1]))

# 다른 코드
def solution(n):
    return list(map(int, reversed(str(n))))
```

---
### 📌 정수 제곱근 판별
`n`이 어떤 양의 정수 `x`의 제곱인지 아닌지 판단하는 문제.

### 💡 나의 풀이
`root`를 선언해서 `root * root`의 값과 `n`이 같은지 아닌지를 판별하면 된다.
이때, 같다면 `root+1`값을 제곱해주고 아니면 `-1`을 반환하면 된다.

`root`를 선언하지 않고 `return`문에 풀어서 작성해도 되는데, 가독성을 위해 줄여봤다.

```python
# 내 코드
def solution(n):
    root = int(n ** 0.5)
    return (root+1) * (root+1) if root * root == n else -1

# 내 코드를 줄여쓴 코드
def solution1(n):
    root = int(n ** 0.5)
    return (root+1) ** 2 if root ** 2 == n else -1
```

---
### 📌 짝수와 홀수
짝수일 경우 `"Even"`을 반환하고 홀수인 경우 `"Odd`"를 반환해라.

### 💡 나의 풀이
문제 자체는 쉽지만 다른 사람의 코드 중 `논리연산자`와 `단락평가`를 이용해서 표현한게 신기해서 작성했다.

```python
# 내 코드
def solution(num):
    return 'Even' if num % 2 == 0 else 'Odd'

# 다른 사람의 코드
def solution(num):
    return num % 2 == 0 and 'Even' or 'Odd'
```

---
### 📌 휴대폰 번호 가리기
전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 `*`으로 가린 문자열을 리턴하는 함수를 완성해주세요.

### 💡 나의 풀이
처음에 든 생각은 `for range(len))`문을 사용하려고 했는데, 가독성을 위해 `enumerate`로 수정했다. 하지만, 한 줄로 작성한 나의 코드마저 다른 사람의 코드에 비해서는 긴 코드였다.

`s[0:-4]`까지는 `*`로 정해져있으니까 그것을 유지한채 나머지 s[-4:]만큼만 떼서 가져오면 됐었는데 문제풀때는 왜 생각이 안 났을까😓 😓

```python
# 내 코드
def solution(ㄴ):
    return ''.join(['*' if idx < len(s)-4 else val for idx, val in enumerate(s)])

# 다른사람의 코드 
def solution(s):
    return '*' * (len(s)-4) + s[-4:]
```

---
### 📌 이상한 문자 만들기
각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수를 완성하세요.

1. 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
2. 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

### 💡 나의 풀이
`s.split(' ')`의 중요성을 깨닫게 해준 문제였다. 각 단어는 <span style='color:blue'>하나 이상</span>의 공백문자라고 했는데, 문제를 간과하고 `s.split()`만 사용해서 정답률이 `31%`로 나왔었다.

`for ~ in range(len))`, `for ~ in enumerate` 중 내가 쓰기 편한 코드인 `enumerate`를 사용했다. 

다른사람은 내가 작성한 코드를 한 줄로 표현했다. 
이 코드를 한 줄로 표현하니까 코드가 길어져서 나는 눈에 잘 들어오지 않았는데 가독성이 괜찮은가? 
👇🏽 댓글로 의견을 남겨주세요!! 👇🏽

```python
# 내 코드
def solution1(s):
    s = s.split(' ')
    result = ''
    for word in s:
        for idx, value in enumerate(word):
            if idx % 2 == 0:
                result += value.upper()
            else:
                result += value.lower()
        result += ' '
    return result[:-1]

# 다른사람의 코드
def solution(s):
    return ' '.join([''.join([value.upper() if idx % 2 == 0 else value.lower() for idx, value in enumerate(word)]) for word in s.split()])
```

---
### 📌 최대공약수와 최소공배수
두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요.

### 💡 나의 풀이
최대공약수와 최소공배수의 문제는 `유클리드 호제법(Euclidean algorithm)`을 이용하면 간단하게 해결 할 수 있다.

<a href='https://ko.wikipedia.org/wiki/유클리드_호제법'>유클리드 호제법(Euclidean algorithm)의 정의</a>는 다음과 같다.

<span style='color:blue'>2개의 자연수(또는 정식) a, b에 대해서 a를 b로 나눈 나머지를 r이라고 하면(단, a>b), a와 b의 최대공약수는 b와 r의 최대공약수와 같다.</span>

다음 사진과 같은 과정을 거치면 손쉽게 `최대공약수(GCD)`를 구할 수 있는데, `최대공배수(LCM)`는 처음 `a * b`값에 `GCD`로 나눠주면 된다.

![](https://images.velog.io/images/abcd8637/post/f415ae3f-21af-4236-855d-79723ed33e77/KakaoTalk_Photo_2021-04-05-09-17-39.jpeg)

이 문제의 팁을 작성하자면 `최소공배수`를 구할 때 처음 입력받은 `a`와 `b`값이 필요하므로 다른곳에 저장했다가 나중에 사용하자.

그렇지 않으면, `a`와 `b`값이 바뀌게 된다.

또, 유클리드 호제법으로 문제를 풀 때는 a가 b보다 커야한다는 조건이 있으므로 a에는 `max`값을, b에는 `min`값을 주도록 하자.

```python
def solution(a, b):
    x, y = max(a, b), min(a, b)

    while y:
        x %= y
        x, y = y, x
    return [x, a*b // x]
```

---
### 📌 x만큼 간격이 있는 n개의 숫자
정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴하는 함수를 만드시오.

제한 조건
1. x는 -10000000 이상, 10000000 이하인 정수입니다.
2. n은 1000 이하인 자연수입니다.

### 💡 나의 풀이
x가 -10000000 이상, 10000000이하인 정수이므로, 계산 방법을 양수일 때, 음수일 때로 나눴다.

또, 이 문제는 `while`, `range`로 풀 수 있는데, 코드를 짧게 만들고 싶어 한 줄로 요약하려다가 실패하고 `while`문으로 풀었다.(그냥 양수, 음수별로 나눠서 `range`로 작성했으면 더 짧았을 텐데...)

1. `while`: 기존 `number = number + x`의 값을 누적하는 방식이다. 한 사이클이 돌면 `cnt`를 증가시키고 `cnt가 n보다 크거나 같을 때` 종료하는 과정이다.
2. `range`: x가 양수 혹은 음수일때로 나눠서 작성했다. `range`의 세번째 파라미터에서 `step(x)`만큼 증가하는 코드가 특징이다.
3. `range`: `등차수열`의 특징을 이용했고, `공차(n)`만큼 곱해주었다.

```python
# while로 작성한 코드
def solution1(x, n):
    number, result = x, []
    cnt = 0
    while cnt < n:
        result.append(number)
        number += x
        cnt += 1
    return result

# range로 작성한 코드
def solution2(x, n):
    if x > 0:
        return list(range(x, x*n+1, x))
    else:
        return list(range(x, x*n-1, x))

# 다른사람의 코드
def solution3(x, n):
    return [i*x for i in range(1, n+1)]
```

---
### 📌 비밀지도
<a href='https://programmers.co.kr/learn/courses/30/lessons/17681'>문제 설명</a>

### 💡 나의 풀이
비밀지도 문제의 핵심은 다음과 같다.

> 벽 부분은 `1`, 공백 부분은 `0`으로 부호화한다.
> 지도 1과 2를 겹쳤을 때 어느 하나라도 벽이면 전체 지도에서도 벽이다.
> 출력시 벽은 `#`, 공백은 `' '`으로 설정하자.
> 각각의 배열을 이진수로 변경하고 논리연산자 `or`를 사용해 겹치는 부분을 판단한다.

먼저 배열로 선언된 10진수의 값을 2진수로 바꿨다.
`format`함수를 사용했는데 `'{0:>0{1:}b}'.format(i, n)`의 해석은 다음을 참고하자.

![](https://images.velog.io/images/abcd8637/post/7346991c-ebf8-4fae-b4c9-24aabeaf6659/KakaoTalk_Photo_2021-04-07-09-49-34.jpeg)

1. `{0:}, {1:}`: format함수의 인자 순서
2. `>`: 오른쪽 정렬
3. `0`: 자리수만큼 정렬 후 남은 공간은 0으로 채움(미 사용시 공백으로 채움)
4. `b`: `이진수(bin)` 형태로 반환

`zfill`함수로도 동일하게 사용할 수 있다. (`bin(i)[2:].zfill(n))`)

문제에서 지도 1과 지도 2를 합쳤을 때 값이 1이면 `#`으로 출력하라고 했었다. 
그렇다면 둘 중 하나라도 벽으로 설정하는 방법은 무엇일까?

여러가지 방법이 있겠지만 나는 논리연산자인 `or`를 사용했다.
이전에 <a href ='https://ywtechit.tistory.com/26'>논리연산자와 단락평가</a>를 공부할 때 배웠던 내용인데,
`A or B`: <span style = 'color:blue'>A가 True일때는 B의 값을 보지않고 A를 리턴하고, A가 False일때는 B의 값을 리턴한다</span>고 배웠다.

출력은 `0(False)`과 `1(True)`뿐이니까 `or`를 사용하면 나올 수 있는 경우의 수는 다음과 같다.
![](https://images.velog.io/images/abcd8637/post/8dfb3ec7-249f-43d6-bda2-e80c1e61518b/smaple.jpeg)

이후, `zip`함수를 사용하여 `index`를 하나씩 꺼내준 다음 논리연산자(`or`)를 사용하여 서로의 값을 비교하여 새로운 배열에 담았다.

그리고 값이 1이면 `#`을 출력하고 0이면 ` `공백을 출력하는 값을 `return`해줬다.

---

정답을 제출하고 다른사람의 코드를 보니까 `map`함수로 `zip`을 비교하고 비트 or연산(`|`)을 사용해서 쉽게 작성한 코드가 있었다.

또, `replace`함수를 사용해 `1`과 `0`을 쉽게 변경했다.

```python
# 나의 코드
def solution(n, arr1, arr2):
    arr1_bin = ['{0:>0{1:}b}'.format(i, n) for i in arr1]
    arr2_bin = ['{0:>0{1:}b}'.format(i, n) for i in arr2]
    secret_map = [[int(k) or int(m) for k, m in zip(i, j)] for i, j in zip(arr1_bin, arr2_bin) ]

    return [''.join(['#' if j == 1 else ' ' for j in i]) for i in secret_map]

# zfill을 사용한 코드
def solution(n, arr1, arr2):
    arr1_bin = [bin(i)[2:].zfill(n)) for i in arr1]
    arr2_bin = [bin(i)[2:].zfill(n)) for i in arr2]
    secret_map = [[int(k) or int(m) for k, m in zip(i, j)] for i, j in zip(arr1_bin, arr2_bin) ]

    return [''.join(['#' if j == 1 else ' ' for j in i]) for i in secret_map]

# 다른사람의 코드 + zfill
def solution(n, arr1, arr2):
    arr = list(map(lambda x: x[0] | x[1], zip(arr1, arr2)))
    arr = list(map(lambda x: bin(x)[2:].zfill(n), arr))
    result = []
    
    for i in arr:
        i = i.replace('1', '#')
        i = i.replace('0', ' ')
        result.append(i)
    return result
```

---
### 📌 실패율
<a href='https://programmers.co.kr/learn/courses/30/lessons/42889'>문제 설명</a>

### 💡 나의 풀이
처음 문제를 풀면서 다음과 같은 방법을 떠올렸다.
1. 반복문이 진행될 때마다 전체 `len`의 값이 `count`만큼 줄어들어야 하므로 `stages`를 `sort`해주고 `pop`으로 `i`값을 빼주기: 실패
2. 이중 반복문을 사용해서 첫번째 순서를 제외한 나머지 순서는 다음과 같이 선언하기 `arr.count(i) / len(arr) - 이전 count(i)`: 실패
3. 이전 `count`로 반복문이 끝나기 전에 전체 `len`을 빼주기: 성공

결과적으로 3번째 방법으로 풀어서 맞았는데, 1번과 2번 방법으로 1시간 넘게 고민하다가 기운이 다 빠져버렸다. 😅 😅

그리고 반례를 생각하지 않아서 `1, 6, 7, 9, 13, 23, 24, 25번` 테스트케이스에서 오답판정을 받았다.
혹시라도 저 테스트케이스에서 오답판정을 받았다면 다음 테스트케이스를 실행해보자! `N = 5, stages = [3, 1, 2, 2, 2]` 

힌트는 다음과 같다.(하단 드래그!)
`마지막 stages`에서 0명의 사용자가 지원했으므로 분모가 0이 된다. 따라서, 아직 마지막 `stages`가 끝나지도 않았는데 더 이상 나눌 값이 없다면...? 어떻게 처리를 해줘야 할까? 한번 생각해보자.

3번을 이용하여 풀었던 자세한 방법은 다음과 같다.
1. 전체 `stages`를 변수로 선언해준다.(한 반복문이 끝날 때마다 이전 `count`값을 빼줘야 하기 때문이다.)
2. 반복문에서 현재 i값을 key로, `스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수`를 value로 선언해준다.
3. 전체 `stages`에서 `스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수`를 빼주자.

여기까지 진행하게되면, 다음과 같은 출력을 볼 수 있다.
`{1: 0.125, 2: 0.42857142857142855, 3: 0.5, 4: 1.0, 5: 0}`

왜 결과 값을 `리스트`로 하지않고 `딕셔너리`로 선언했는지 궁금할 수도 있을텐데, 실패율이 높은 `stage`부터 내림차순으로 정렬해야하기 때문이다. 
즉, 일반적인 수의 큰값과 작은값을 기준으로 오름차순 / 내림차순을 하는게 아니라, 실패율을 기준으로 정렬해야하기때문에 `key:value`형태인 딕셔너리로 선언했다.

이제 `value`값을 기준으로 정렬하는데 내 방식은 이랬다.
`return list(dict(sorted(stages_dic.items(), key=lambda x: x[1], reverse=True)).keys())`
1. `stages_dic`의 `item` 중 `value`값을 기준으로 정렬한다.
2. `sorted`는 자동으로 `list`로 반환해주기 때문에 `dict`으로 바꾸고 그 중 `key`값을 반환한다.
3. return 값이 `list`이므로 `list`를 붙여준다.

다른 사람의 코드는 다음과 같이 선언할 수 있다.
`return sorted(stages_dic, key = lambda x: stages_dic[x], reverse = True)`
1. 딕셔너리에서 `sorted`를 사용하면 `key`를 기준으로 정렬하는데 람다함수를 사용해서 `stages_dic[x]` 즉, `value`를 기준으로 정렬한다.
  * 우리가 딕셔너리 `value` 값에 접근하기위해서 `dic['key']`를 사용하는것과 같은 원리다.

두번째코드가 더 간편해보인다. 기억했다가 나중에 써먹어야겠다.

```python
# 나의 코드
def solution(N, stages):
   stages_dic = {}
   stages_len = len(stages)

    for i in range(1, N+1):
        if stages_len == 0:
            stages_dic[i] = 0
        else:
            stages_dic[i] = stages.count(i) / stages_len
        stages_len -= stages.count(i)

    return list(dict(sorted(stages_dic.items(), key=lambda x: x[1], reverse=True)).keys())

# 다른사람의 코드
def solution(N, stages):
   stages_dic = {}
   stages_len = len(stages)

    for i in range(1, N+1):
        if stages_len == 0:
            stages_dic[i] = 0
        else:
            stages_dic[i] = stages.count(i) / stages_len
        stages_len -= stages.count(i)

    return sorted(stages_dic, key = lambda x: stages_dic[x], reverse = True)
```

---
### 📌 소수만들기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12977'>문제 설명</a>

### 💡 나의 풀이
풀이 방법은 다음과 같다.

1. `nums`에 있는 숫자들 중 서로 다른 3개를 고른다: `combination(3, nums)`
2. 각각의 `combination`을 모두 더한 후 소수 판별과정을 거친다.
3. 소수가 맞으면 `cnt +=1`
4. 반복문이 끝나면 `return cnt`

처음에 `break`를 사용해야할지, `continue`를 사용해야할지 헷갈렸다. 
결론적으로 `sum(i)`를 j로 나눌 때 한번이라도 0으로 나누어떨어지는 값이 나오면 해당 반복문을 더 이상 실행하지 않아야 다음 `sum(i)`로 넘어가기때문에 `break`를 사용했다. `continue`를 사용하면 다음 `sum(i)`값을 불러오는 것이 아닌, 다음 j값을 불러오게 된다.

여기서 중요한 문법은 `for - else`문법인데, `j`가 반복문 끝까지 돌았는데 `break`에 걸리는것이 없다면, `cnt+=1`을 하게 작성했다.
같은 반복문 안에서만 사용가능한 것이 아니라, 밖에서도 사용가능한점 숙지하자.

```python
from itertools import combinations

def solution(nums):
    result = [sum(i) for i in combinations(nums, 3)]
    cnt = 0
    
    for i in result:
        for j in range(2, i//2+1):
            if i % j == 0:
                break
        else:
            cnt+=1
    return cnt
```

---
### 📌 키패드 누르기
<a href='https://programmers.co.kr/learn/courses/30/lessons/67256'>문제 설명</a>

### 💡 나의 풀이
<a href='https://ywtechit.tistory.com/147'>저번</a>에 풀었던 <a href='https://www.acmicpc.net/problem/20436'>백준 - ZOAC 3</a> 문제와 비슷하다는 것을 느꼈다. 다만, 
`ZOAC 3`는 택시거리를 구했고, `키패드 누르기` 문제는 같은 거리 일때 더 가까운 손가락은 어떤 손가락인가?를 구해야했다.

이 문제의 큰 흐름은 다음과 같다.
1. 맨 처음 왼손 좌표는 `*(3, 0)`, 오른손 좌표는 `#(3, 2)`로 초기화 시킨다.
2. `numbers`가 반목문을 돌면서 거리를 구해야한다.
3. `numbers`의 열에 따라 왼손 좌표, 오른손 좌표를 각각 `update`시킨다. 만약, `numbers`의 `column`좌표가 `0`이면 왼손 좌표를 `update`시키고, `column`좌표가 `1`이면 왼손과 오른손 중 더 가까운 손 좌표를 `update`, 마지막으로 `column`좌표가 `1`이면 오른손 좌표를 `update` 시킨다.

더 자세한 흐름을 살펴보자.
1. `numbers`가 `keypad` 좌표 중 어디에있는지 반환해주는 함수를 만들어야 한다.
2. `column`좌표가 `1`이고, 두 엄지손가락 중 어떤 손가락의 거리가 더 가까운지 찾고(`bfs`), 만약 두 거리가 같다면 오른손잡이인지 왼손잡이인지에 따라 `update`해야한다.

처음에는 오답판정을 받았는데 `bfs` 함수 내에서 `상, 하, 좌, 우` 좌표를 탐색하는 `20`번째 코드 이후에 `return`문을 작성했는데 `numbers`가 똑같은 값이 들어올 때 정답이 일정하게 나오지 않았다. 예를 들어 `numbers=[0, 0, 0, 0], hand = 'right'`일 때 정답은 `RRRR`이어야 하지만 `RLRR`와 출력이 반환됐다. `상, 하, 좌, 우` 반목문이 들어가기 전인 `16`번째에 `return`문을 작성했더니 정답 판정을 받았다. 또, `result`를 반환 할 때 리스트에 `append -> ''.join(result)` 하는 것 보다 문자열이기 때문에 `+=`를 사용하는게 가독성이 더 좋아보인다. `R`, `L` 판정 이후 현재 좌표를 `갱신`시키는 것 또한 잊지말자. 하단에 `bfs`를 돌 때 `visited` 변화를 보여주는 그림을 그려봤다. 마지막으로 중요한 것은 `bfs` 함수를 사용한다면 `visited`를 한번 돌 때마다 초기화하는 작업을 ⭐️ 꼭 ⭐️ 시켜주자!! 그렇지 않으면 방문표시를 하는 코드가 의미없어지고 `bfs`가 정상적으로 작동하지 않는다!!

![](https://images.velog.io/images/abcd8637/post/3e466f69-cea9-4a9c-b1f5-92fc4fe7db9e/KakaoTalk_Photo_2021-06-21-13-41-28.jpeg)

```python
from collections import deque

def find_row_column(key):    # number의 행과 열을 찾는 함수
    for i in range(4):
        if key in keypad[i]:
            return i, keypad[i].index(key)

def bfs(x, y, target):    # 두 엄지손가락의 거리 중 더 가까운 거리 찾기
    visited = [[0] * m for _ in range(n)]    # 매번 visited 변수 초기화
    queue = deque()
    queue.append((x, y))
    visited[x][y] = 1    

    while queue:
        x, y = queue.popleft()

        if keypad[x][y] == target:
            return visited[x][y] - 1

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if nx < 0 or ny < 0 or nx >= n or ny >= m:
                continue

            if not visited[nx][ny]:
                visited[nx][ny] = visited[x][y] + 1
                queue.append((nx, ny))

def solution(numbers, hand):
    result = ''
    cur_left_hand = (3, 0)  # 초기 왼손 좌표 '*'
    cur_right_hand = (3, 2)  # 초기 오른손 좌표 '#'

    for number in numbers:
        row, column = find_row_column(str(number))

        if not column:  # number가 [1, 4, 7] 중 한 개 일 때
            result += 'L'
            cur_left_hand = (row, column)

        elif column == 2:  # number가 [3, 6, 9] 중 한 개 일 때
            result += 'R'
            cur_right_hand = (row, column)

        else:  # number가 [2, 5, 8] 중 한 개 일 때
            temp_left = bfs(cur_left_hand[0], cur_left_hand[1], str(number))
            temp_right = bfs(cur_right_hand[0], cur_right_hand[1], str(number))
            
            if temp_left < temp_right:
                result += 'L'
                cur_left_hand = (row, column)
            elif temp_left > temp_right:
                result += 'R'
                cur_right_hand = (row, column)
            else:
                if hand == 'right':
                    result += 'R'
                    cur_right_hand = row, column
                else:
                    result += 'L'
                    cur_left_hand = row, column
    return result


keypad = ['123', '456', '789', '*0#']
n, m = 4, 3  # keypad row, column
dx = [-1, 0, 1, 0]  # U, R, D, L
dy = [0, 1, 0, -1]
```

---
### 📌 기능개발
<a href='https://programmers.co.kr/learn/courses/30/lessons/42586'>문제 설명</a>

### 💡 나의 풀이
처음으로 2단계 문제를 풀어봤다. 앞으로 2단계 문제를 꾸준히 풀어야하는데 괜찮을까.. 한번 도전해보자!

(문제의 이해도를 높이기 위해 나중에 `progress` 변수명 대신 `queue`를 사용했다.)

1. 완성되기까지 남은 진도율에서 현재 속도만큼 일했을 때 며칠만에 완성 할 수 있는지 구하기. (이 경우를 식으로 변환 할 때 나머지가 없으면 몫을 그냥 `append` 시키고 나머지가 있으면 `몫 + 1` 해준 다음 `append`했다.)
2. 이중 `while`문을 선언했는데 그 이유는 내 다음 순서가 나보다 값이 작더라도 내가 먼저 나가야 같이 나갈 수 있고 만약, 연속으로 나가야 할 일이 생길때를 대비해서 이중 `while`문으로 작성했다. (`break` 해주는것도 잊지말자.)
3. `queue`가 있다는 조건 하 `day`가 1씩 증가하면서 먼저 배포되어야 하는 순서(0번째)가 `day`와 같거나 크다면 `pop`시키고 그렇지 않으면 반복문을 종료시켰다. (나중에 `queue`가 없는데 비교하면 오류가 생기므로 `queue`가 있을 때라는 조건을 걸어줘야한다.) 
4. 두번째 `while`문 종료 후에 빠져 나간 기능이 있으면 몇개인지 체크하여 `result`로 옮기고 `stack`은 원 위치시킨다.

정답판정을 맞고 다른 사람의 코드를 보니까 1번 과정을 조금 더 짧게 표현한 코드가 있었다. `lambda`함수로 `range`를 더하여 구현했는데 내가 딱 구현하고 싶었던 기능이었다. 그리고 나머지의 유무를 보는 대신 음수의 나눗셈을 사용하여 구현했는데 음수는 써본적이 없었는데 `ceil`라이브러리를 쓰는 것보다 편해보여서 좋았다. (참고로, `python`에서 `음수 나눗셈(ex: -3 / 2 = -1.5, -3 // 2 = -2)`은 음의 무한대로 반올림되는데 왜 그런지 잘 모르겠다면 <a href='https://ywtechit.tistory.com/195'>다음</a> 글을 살펴보자.)

```python
# 나의 코드
def solution(progress, speeds):
    rest_progress = list(map(lambda x: 100 - x, progress))
    day = 1
    queue, stack, result = [], [], []

    for divisor, dividend in zip(speeds, rest_progress):
        if not dividend % divisor:
            queue.append(dividend // divisor)
        else:
            queue.append((dividend // divisor) + 1)

    while queue:
        while True:
            if queue and queue[0] <= day:
                stack.append(queue.pop(0))
            else:
                day += 1
                break

        if stack:
            result.append(len(stack))
            stack = []

    return result
```

```python
# 나의 수정코드
def solution(progress, speeds):
    day = 1
    stack, result = [], []
    queue = list(map(lambda x: -((progress[x] - 100) // speeds[x]), range(len(progress))))

    while queue:
        while True:
            if queue and queue[0] <= day:
                stack.append(queue.pop(0))
            else:
                day += 1
                break

        if stack:
            result.append(len(stack))
            stack = []

    return result
```
