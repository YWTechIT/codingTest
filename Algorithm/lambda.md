## 💡 람다식의 간편한 사용

---
## 📍 조건식 사용
```python
# 1차원
arr = [1, 2, 3, 4, 5]
result = list(map(lambda x: x-2 if x >= 2 else x, arr))
print(result)
👉🏽 [1, 0, 1, 2, 3]

# 2차원
arr2 = [[ 1, 2, 3, 4, 5], [2, 3, 4, 5, 6], [3, 4, 5, 6, 7]]
result = [list(map(lambda x: x-2 if x >= 2 else x, i)) for i in arr2]
print(result)
👉🏽 [[1, 0, 1, 2, 3], [0, 1, 2, 3, 4], [1, 2, 3, 4, 5]]
```

---
## 📍 딕셔너리의 value값을 기준으로 정렬하고 key값을 뽑아내고 싶을 때
딕셔너리에서 `sorted`를 사용하면 `key`값을 출력한다.
만약, `key`값으로 출력하는건 동일하나, `value`를 기준으로 정렬하고 싶으면 `lambda x: dic[x]`를 사용하자.

```python
cnt_dict = {1: 0.125, 2: 0.42857142857142855, 3: 0.5, 4: 1.0, 5: 0}

# 1. lambda value기준
cnt_dict = sorted(cnt_dict, lambda x: cnt_dict[x])
print(cnt_dict)

# 2. keys()
cnt_dic = list(dict(sorted(cnt_dic, key=lambda x: cnt_dic[x], reverse=True), keys())
👉🏽 [5, 1, 2, 3, 4]
```

---
## 📍 sorted(key = lambda) 사용
우선순위

1. 식별자를 제외한 문자열 모두를 검사한다.
2. 그럼에도 불구하고 문자열 모두가 동일하다면 식별자를 기준으로 정렬한다.

```python
logs = ["dig1 8 1 5 1", "let1 art can", "dig2 3 6", "let2 own kit dig", "let3 art zero"]

def solution(logs):
    letters, digits = [], []

    for i in logs:
        if i.split()[1].isdigit():
            digits.append(i)
        else:
            letters.append(i)

    letters = sorted(letters, key= lambda x: (x.split()[1:], x.split()[0]))

    return letters + digits
```

---
## 📍 zip함수 사용하기
1. 2개의 배열을 zip함수를 사용하여 비트or연산하기
   
```python
# 5자리수까지 출력
n = 5
arr1 = [1, 2, 3, 4, 5]
arr2 = [5, 6, 7, 8, 9]

arr = list(map(lambda x: x[0] | x[1], zip(arr1, arr2))
arr = list(map(lambda x: bin(x)[2:].zfill(n), arr))
```

---
## 📍 원하는 튜플기준으로 출력하고 싶을 때
```python
n = int(input())

array = []
for i in range(n):
    input_data = input().split()
    array.append((input_data[0], int(input_data[1]))

# 점수 기준 sort(오름차순)
array = sorted(array, key = lambda student: student[1])

# 점수 기준 sort(내림차순)
array = sorted(array, key = lambda student: student[1], reverse=True)

for score in array:
    print(score[1], end=' ')

👉🏽 입력
3
이순신 93
장보고 50
문성공 99

👉🏽 출력
50 93 99 (오름차순)
99 93 50 (내림차순)

# 이름 기준 sort(오름차순)
array = sorted(array, key = lambda student: student[0])

# 이름 기준 sort(내림차순)
array = sorted(array, key = lambda student: student[0], reverse=True)

for name in array:
    print(name[0], end=' ')

👉🏽 입력
3
이순신 93
장보고 50
문성공 99

👉🏽 출력
문성공 이순신 장보고 (오름차순)
장보고 이순신 문성공 (내림차순)
```
---