## 📍 코드업 100문제를 풀면서 알아두면 좋을 팁들
1. 무조건 소숫점 n번째자리까지 출력하는문제는 `'%.nf'`를 쓰자.
2. `bool()`형태`(True, False)`로 반환할 때는 `bool(n)`을 사용하자.
3. python 정수형에서 `0(False)`을 제외한 나머지는 `True다`.
4. `0 and 0 == False`
5. AND(&), OR(|), XOR(^), NOT(~)
6. 한 줄 비교식 `print(a if a > b else b)`


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



