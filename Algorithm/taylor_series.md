### taylor_series(테일러 급수)

### 📍 radian(라디안)
>1. 호도법: 호가 반지름과 같아지는 각도, 약 57.3도를 1라디안으로 하며 보통의 경우 기호를 사용하지 않는다.

| degrees | radians(π) | radians(number) | 
| :----: | :----: | :----: |
| 30°  | π / 6 | 0.524 | 
| 45°  | π / 4 | 0.785 | 
| 60°  | π / 3 | 1.047 | 
| 90°  | π / 2 | 1.571 |

---

### 📍 삼각비
| degrees | 30° | 45° | 60° |
| :----: | :----: | :----: | :----: |
| sin  | 1 / 2 | 1 / √2 | √3 / 2 |
| cos  | √2 /2 | 1 / √2 | 1 / 2 |
| tan  | 1 / √3 | 1 | √3 |

---

### 📍 sin(x)
> 1. sin(x): `x=0`에서 계속 미분가능하다.

 ![](https://images.velog.io/images/abcd8637/post/7b1e1cff-b987-415f-8ed1-a851105583bc/KakaoTalk_Photo_2021-02-15-12-55-04.jpeg)

### ⚡️ 유도과정

> 1. `f(x) = f(a) + f'(a)(x-a) + f''(a)/2! * (x-a)^2 + f'''(a)/3! * (x-a)^3 +  f''''(a)/4! * (x-a)^4`
> 2. `f(0) = f(0) + f'(0)(x-0) + f''(0)/2! * (x-0)^2 + f'''(0)/3! * (x-0)^3 +  f''''(0)/4! * (x-a)^4`
> 3. `f(0) = x - x^3/3! + x^5/5! - x^7/7! + x^9/9!`
> 4. 즉, `1 <= n <= ∞` 이면, `(-1)^n * x^(2n+1)/(2n+1)!`
> 5. 이전항에서 `x=-x^2/(2n*(2n+1))`마다 곱하면 된다.

점화식을 이용해 식을 나타내면 다음과 같다.

```python
# x는 각도
# count_term은 테일러급수 점화식에서 변수만큼 식을 계산함
'''
sin(0, 15) => sin 0도
sin(pi/6, 15) => sin 30도
sin(pi/4, 15) => sin 45도
sin(pi/3, 15) => sin 60도
'''
import pi
pi = math.pi

def sin(x, count_term):
    if x < 0:
        return -sin(-x, count_term)
        
    while x >= 2*pi:
        x -= 2*pi

    current_term = x
    estimated = current_term
    
    for n in range(1, count_term):
        current_term *= -x*x/(2*n*(2*n+1))
        estimated += current_term
    return estimated

result = sin(0, 15)
print(result)
👉🏽 0, 0.4996, 0.7046, 0.8558
```

---

### 📍 cos(x)
> 1. cos(x): `x=0`에서 계속 미분가능하다.

 ![](https://images.velog.io/images/abcd8637/post/168ebd09-a4ac-40ac-b558-b474e12b99f2/KakaoTalk_Photo_2021-02-15-13-24-21.jpeg)

 ![](https://images.velog.io/images/abcd8637/post/1f2e6fe5-300e-416c-957e-7e08e3ebb974/2.jpeg)

### ⚡️ 유도과정
> 1. `f(x) = f(a) + f'(a)(x-a) + f''(a)/2! * (x-a)^2 + f'''(a)/3! * (x-a)^3 +  f''''(a)/4! * (x-a)^4`
> 2. `f(0) = f(0) + f'(0)(x-0) + f''(0)/2! * (x-0)^2 + f'''(0)/3! * (x-0)^3 +  f''''(0)/4! * (x-a)^4`
> 3. `f(0) = 1 - x^2 / 2! + x^4 / 4! - x^6 / 6! + x^8 / 8!`
> 4. 즉, `1 <= n <= ∞` 이면, `(-1)^n * x^(2n)/(2n)!`
> 5. 이전항에서 `x=x^n/n!`마다 곱하면 된다.

점화식을 이용해 식을 나타내면 다음과 같다.

```python
# x는 각도
# count_term은 테일러급수 점화식에서 변수만큼 식을 계산함
'''
cos(0, 15) => cos 0도
cos(pi/6, 15) => cos 30도
cos(pi/4, 15) => cos 45도
cos(pi/3, 15) => cos 60도
'''
import pi
pi = math.pi

def cos(x, count_term):
    if x < 0:
        return cos(-x, count_term)
        
    while x >= 2*pi:
        x -= 2*pi

    current_term = 1
    estimated = current_term
    
    for n in range(1, count_term):
        current_term *= -x*x/(2*n*(2*n-1))
        estimated += current_term
    return estimated

result = cos(0, 15)
print(result)
👉🏽 1.0, 0.8660, 0.7071, 0.5
```

---

### 📍 tan(x)

> 1. tan(x) = sin(x) / cos(x)
> 
```python
# x는 각도
# count_term은 테일러급수 점화식에서 변수만큼 식을 계산함
'''
tan(0, 15) => tan 0도
tan(pi/6, 15) => tan 30도
tan(pi/4, 15) => tan 45도
tan(pi/3, 15) => tan 60도
'''
import pi
pi = math.pi

def tan(x, count_term):
    return sin(x, count_term) / cos(x, count_term)

result = tan(0, 15)
print(result)
👉🏽 0.0, 0.5769, 0.9965, 1.7116
```
---