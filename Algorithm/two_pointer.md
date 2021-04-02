# two_pointer
> `two_pointer`: 리스트에 순차적으로 접근해야 할 때 2개의 점의 위치를 기록하면서 처리하는 알고리즘

Q. 특정한 합을 가지는 부분 연속 수열 찾기
>1. 시작점(start), 끝점(end)이 첫 번째 원소의 인덱스(0)을 가리키자
>2. 현재 부분합 `M`과 같으면 카운트한다.
>3. 현재 부분합이 `M`보다 작으면 `end`를 1 증가시킨다.
>4. 현재 부분합이 `M`보다 크거나 같으면 `start`를 1 증가시킨다.
>5. 모든 경우를 확인 할 때까지 `2번`과 `4번`의 과정을 반복한다.

```python
# 찾고자 하는 데이터의 개수
n = 5
data = [1, 2, 3, 2, 5] 

# 찾고자 하는 합의 값
m = 5

# 초기선언
interval_sum = 0
count = 0
end = 0

for start in range(n):
    while interval_sum < m and end < n:
        interval_sum = interval_sum + data[end]
        end = end + 1
    if interval_sum == n:
        count = count + 1
    interval_sum = interval_sum - data[start]

print(count)
👉🏽 3
```

---
Q2. 두 리스트의 모든 원소를 합쳐 정렬한 결과를 계산하기
>1. 정렬된 리스트 `A`와 `B`를 받는다.
>2. 리스트 `A`에서 처리되지 않은 원소 중 가장 작은 원소를 `i`가 가르키도록 한다.
>3. 리스트 `B`에서 처리되지 않은 원소 중 가장 작은 원소를 `j`가 가르키도록 한다.
>4. `A[i]`와 `B[j]` 중 더 작은 원소를 결과 리스트에 담는다.
>5. 리스트 `A`와 `B`에서 더 이상 처리할 원소가 없을 때 까지 `2번` ~ `4번`의 과정을 반복한다.

```python
# 기본버전: 값이 정해져 있을 때
# A 데이터
a = [1, 3, 5]
n = 3
i = 0

# B 데이터
a = [2, 4, 6, 8]
n = 4
j = 0

# 응용버전: input값을 통해서 넣어 줄때
# A 데이터
a = list(map(int, input(). split()))
n = len(a) 
i = 0

# B 데이터
b = list(map(int, input(). split()))
m = len(b) 
j = 0

# result 데이터
result = (m+n) * [0]
k = 0

while i < n or j < m:
    if j > m or (i < n and a[i] < b[j]):
        result[k] = a[i]
        i = i + 1
    else:
        result[k] = a[j]
        j = j + 1
    k = k + 1

for i in result:
    print(i, end = ' ')
👉🏽 1 2 3 4 5 6 8
```

---
Q3. 리턴없이 리스트 내부를 직접 조작하는 문자열을 뒤집는 함수를 작성하라.

투포인터를 이용해서 양쪽 끝 index자리를 기준으로 `swap`하도록 작성했다.

```python
s = ['h', 'e', 'l', 'l', 'o']
left, right = 0, len(s)-1

while left < right:
    s[left], s[right] = s[right], s[left]
    left += 1
    right -= 1
print(s)
👉🏽 ['o', 'l', 'l', 'e', 'h']
```