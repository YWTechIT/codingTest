## recursive_function
자기 자신을 다시 호출하는 함수이다.

가장 간단한 식
```python
def recursive_function():
    print('재귀함수를 호출합니다.)
    recursive_function

print(recursive_function())
👉🏽 RecursionError: maximum recursion depth exceeded while calling a Python object
```

이 오류메시지는 재귀의 최대 깊이를 초과했다는 내용이다. 
보통 파이썬 인터프리터는 호출 횟수 제한이 있는데 이 한계를 벗어났기 때문이다. 따라서 무한대로 재귀 호출을 진행 할 수는 없다.

다음과 같이 종료조건을 준다.
```python
def recursive_function(i):
    if i == 3:
        return
    print(f'{i}번째에서 {i+1}번째 재귀 함수를 호출합니다.')
    recursive_function(i+1)
    print(f'{i}번째에서 함수를 종료합니다.')

recursive_function(1)
👉🏽1번째에서 2번째 재귀 함수를 호출합니다.
2번째에서 3번째 재귀 함수를 호출합니다.
3번째에서 4번째 재귀 함수를 호출합니다.
4번째에서 5번째 재귀 함수를 호출합니다.
4번째에서 함수를 종료합니다.
3번째에서 함수를 종료합니다.
2번째에서 함수를 종료합니다.
1번째에서 함수를 종료합니다.
```

재귀 함수의 수행은 스택 자료구조를 이용한다.
함수를 계속 호출했을 때 가장 마지막에 호출한 함수가 먼저 수행을 끝내야 그 앞의 함수 호출이 종료되기 때문이다.
(스택구조는 선입후출 방식이다.)
결론적으로 재귀함수는 내부적으로 스택 자료구조와 동일하다는 것만 기억하자.

재귀함수를 이용하는 문제는 대표적으로 `팩토리얼(factorial)` 문제가 있다. 팩토리얼문제는 `반복문`, `재귀함수`방식으로 풀 수 있다.

```python
# 반복문
def for_factorial(n):
    result = 1
    for i in range(1, n+1):
        result = result * i
    return result

print(for_factorial(5))
👉🏽 120

# 재귀함수
def recursive_factorial(n):
    if n <= 1:
        return 1
    
    return result * for_factorial(n-1)

print(recursive_factorial(5))
👉🏽 120    
```