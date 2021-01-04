## combination
> 조합(combination): 서로 다른 `n개`에서 순서에 상관없이 서로 다른 `r개`를 선택하는 것
> 
> nCr으로 불림 
> 
> 순서에 의미가 없을 때 주로 사용함.
> 
> 참고영상: <a href='https://www.youtube.com/watch?v=1I6fAgEOPt4'>수학삼촌</a>

```python
import itertools

data = [1, 2, 3]

for i in itertools.combination(data, 3):
    print(list(i), end=' ')

👉🏽 [1, 2][1, 3][2, 3]
```
---

### [ 예제 ] 백준 1759
<a href='https://www.acmicpc.net/problem/11659'>문제</a>

조합을 사용하는 대표적인 문제이다.
길이가 `l`인 모든 암호 조합을 확인한 뒤
`최소 1개의 모음`과 `최소 2개 이상의 자음`이 있는 경우를 `and`로 묶어 출력하면 된다.

처음에 문제를 풀다 막히는 부분이 있었다.
`list`내의 특정 문자열을 포함 여부를 풀 때 `if`문을 사용해도 결과가 나오지 않았다.
구글링을 해보니 `for문`을 돌려 리스트를 벗겨 낸 다음 특정 문자열을 찾으면 된다.

알고리즘 문제를 풀면서 부족하다 느낀건 조건에 정답이 거의 주어져있는데 100% 활용하지 못한다는 점이다.
문제를 좀 더 꼼꼼히 읽어보고 풀어야겠다는 생각을 했다.

```python
import itertools

vowels = ['a', 'e', 'i', 'o', 'u']
l, c = map(int, input().split())

array = input().split()
array.sort()

for password in itertools.combinations(array, l):
    count = 0
    for i in password:
        if i in vowels:
            count = count + 1
    print(count)
    if count >= 1 and count <= l - 2:
        print(''.join(password))
```
---

### [ 예제 2 ] 백준 6603
조합에 관한 문제를 하나 더 풀어봤다.
마찬가지로 기능구현은 어떻게 해야하는지 알았지만, `input`값을 어떻게 줘야할지 막막했다.
그러던 중 list[0]값과 list[1:]값을 분리하는 식을 알았다.

예를 들어, `list`의 값이 `[1, 2, 3, 4, 5]`라고 하자. 
그러면, `[1]`과 나머지 `[2, 3, 4, 5]`로 분류 할 수 있다.

쉽게 예를 들어보자.
`k, *s = map(int, input().split())`일때 값을 `1 2 3 4 5`로 넣게 된다면
k는 `1`, *s는 `[2, 3, 4, 5]`가 된다.

또 문제에서 입력 값이 0이면 입력을 더 이상 하지 않는데,
`while True`문을 사용하여 `if`의 값이 0 이면 더 이상 입력을 받지 않게 설정하면 된다.

마지막에 출력 값을 `list`를 벗겨내야하는데 이는, `join`함수를 사용해서 중간에 `' 공백 '`을 넣어주었다.
다만, `join`을 `int` 형에 적용 할 수 없기 때문에 `문자형(str)`으로 바꿔줘야한다.

```python
import itertools

while True:
    k, *s = map(int, input().split())
    s.sort()
    if k == 0:
        break
    for result in itertools.combinations(s, 6):
        print(' '.join(map(str, result)))
    print()
```

