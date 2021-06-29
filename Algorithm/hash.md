# hash
---

## 📍 백준 1620 - 나는야 포켓몬 마스터 이다솜

<a href='https://www.acmicpc.net/problem/1620'>백준 1620 - 나는야 포켓몬 마스터 이다솜</a>

## ⚡️ 나의 풀이
포켓몬을 좋아해서 풀어봤다.

입력의 범위가 `100,000`까지로 주어져있기 때문에 리스트로 풀기에 시간초과가 날 것 같아 `dict`의 `hash`를 이용하여 풀었다. `(hash 접근 시간복잡도는 O(1))` dict에서 `value`의 값을 찾는것은 `dict[key]`를 넣으면 되기때문에 비교적 쉬웠으나 반대로 `key`를 찾는것은 `dict`로는 찾을 수 없기 때문에 `dict.keys()`만을 뽑아 리스트로 만드는 `list(dict.keys())`를 사용했고, 여기서 몇 번째인지 알기위해 인덱싱을 사용했다. 

1. 입력을 `key:value` 형태인 `dict`로 넣어준다.(이때, `key`는 포켓몬 이름, `value`는 입력 순서)
2. `key`만 모아 새로운 `list`를 생성한다.
3. 입력이 `isdigit()`면 `key`를 출력하고 `not isdigit()`면 `value`를 출력한다.

```python
# 나의 코드
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
pocket_books = {}

for i in range(1, n+1):
    name = input().strip()
    pocket_books[name] = i

pocket_books_keys = list(pocket_books.keys())

for _ in range(m):
    name_or_number = input().strip()
    if name_or_number.isdigit():
        print(pocket_books_keys[int(name_or_number) - 1])
    else:
        print(pocket_books[name_or_number])
```

---

## 📍 백준 10546 - 배부른 마라토너

<a href='https://www.acmicpc.net/problem/10546'>백준 10546 - 배부른 마라토너</a>

## ⚡️ 나의 풀이
<a href='https://ywtechit.tistory.com/11?category=930543'>저번</a>에 풀었던 <a href='https://programmers.co.kr/learn/courses/30/lessons/42576'>프로그래머스 - 완주하지 못한 선수 </a>와 동일한 문제다.

참가자의 수가 `100,000`이기 때문에 기본적으로 `list`를 사용해서 풀면 시간초과가 난다. 그래서 `dict`를 사용해서 풀었다.

1. 참가자를 저장 할 `dict`와 완주 선수를 저장 할 `dict`를 `defaultdict`로 선언한다. `defaultdict`를 선언하면 동일 선수가 나와도 `+1`을 할 수 있기때문에 유용하게 사용 할 수 있다.
2. `Counter` 라이브러리로 참가자와 완주자의 `Counter`를 준다. 간단한 팁이지만 `Counter`끼리는 서로 빼거나 더할 수 있다.
3. 남은 값의 `key`를 출력한다.

이런방식은 정답판정을 받을 수 있으나, 메모리와 실행시간이 오래걸린다. 다른 좋은 방법이 있는지 찾아봤는데 다음과 같다.

1. 참가자를 `defaultdict`로 선언하고 한명씩 추가한다.
2. 완주자를 참가자의 값에서 빼준다.
3. 반복문을 사용하여 `value`가 1이상인 값만 출력한다.

이 방식으로 제출 했더니 큰 차이는 아니지만 `메모리`와 `실행시간`이 소폭 줄었다.

![](https://images.velog.io/images/abcd8637/post/276c97e3-4b9a-497f-8f5e-c54a3d83f825/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-06-29%2013.51.05.png)

```python
# 나의 풀이
import sys
from collections import defaultdict, Counter
input = sys.stdin.readline

n = int(input())
participants = defaultdict(int)
finisher = defaultdict(int)

for _ in range(n):
    name = input()
    participants[name] += 1

for _ in range(n-1):
    name = input()
    finisher[name] -= 1

print(''.join((Counter(participants) - Counter(finisher)).keys()))
```

```python
# 다른 사람의 풀이
import sys
from collections import defaultdict
input = sys.stdin.readline

n = int(input())
participants = defaultdict(int)

for _ in range(n):
    name = input().rstrip()
    participants[name] += 1

for _ in range(n-1):
    name = input().rstrip()
    participants[name] -= 1

for key, value in participants.items():
    if value >= 1:
        print(key)
```