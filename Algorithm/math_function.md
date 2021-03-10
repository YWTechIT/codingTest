## math_function

1. math(): 수학계산을 요구하는 기능

```python
import math

# factorial(x)
print(math.factorial(5))
👉🏽 120
# sqrt(x): x의 제곱근
print(int(math.sqrt(49)))
👉🏽 7

# gcd(x): 최대 공약수
print(math.gcd(21, 14))
👉🏽 7

# 파이(pi) 출력
print(math.pi)
👉🏽 3.141592653589793

# 자연상수(e) 출력
print(math.e)
👉🏽 2.718281828459045
```

### 📍 divmod
몫과 나머지를 구하는 함수
무조건 `divmod`를 사용하는것보다 팀의 코드 스타일에 따라서 `a//b, a%b`를 사용하는것이 더 좋을 수 도 있다.
작은 숫자를 다룰 때는 `a//b, a%b`를 사용하는것이 더 빠르다.
후자는 반대

`print(divmod(3,7))`


