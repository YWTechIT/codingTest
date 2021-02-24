## 📍 함수 정의 및 람다식 사용
> 함수의 특징: 함수를 선언하면 모든 곳에서 사용이 가능하다.

>1. 함수 사용패턴
```python
# return 값을 사용하지 않을 때
def say_hello():
    print('say Hello')
say_hello()

# return 값을 사용 할 때
def say_return(x):
    return 'hello' + x
print(say_return('world'))

# 다중 return 사용 시
def multi_return(x):
    y1 = x * 10
    y2 = x * 100
    y3 = x * 1000
    return y1+y2+y3

# list, tuple, set형 변환도 가능하다.
return [ y1+y2+y3 ]
return ( y1+y2+y3 )
return { y1+y2+y3 }

v1, v2, v3 = multi_return(100)
print(v1, v2, v3)
```

>2. *args
매개변수가 얼마나 넘어 올 지 모를 때 사용한다. 
`default`값은 `tuple`로 출력되고 입력값에 list, tuple, set형을 넣을 수 있다.

```python
def func_args(*args):
    for i in args:
        print(i)

func_args('kim', 'An')
👉🏽 kim park

def func_args(*args):
    for i, v in enumerate(args):
        print(i)

func_args('kim', 'An')
👉🏽 
0 kim
1 park
```

>3. **kwargs
키워드를 제공하는 argument이다.
보통, `dictionary`형태로 {'key' : 'value'}을 넣을 때 주로 사용한다.

```python
def key_kwargs(**kwargs):
    for i, v in kwargs:
    print(i, v)

key_kwargs(name1 = 'ayw', name2 = 'jung', name3= 'lee')
👉🏽
name1 ayw
name2 park
name3 jung

def key_kwargs(**kwargs):
    for i, v in enumerate(kwargs):
    print(i, v)

key_kwargs(name1 = 'ayw', name2 = 'jung', name3= 'lee')
👉🏽
0 name1
1 name2
2 name3

def key_kwargs(**kwargs):
    for i, v in enumerate(kwargs.values()):
    print(i, v)

key_kwargs(name1 = 'ayw', name2 = 'jung', name3= 'lee')
👉🏽
0 ayw
1 park
2 jung

def key_kwargs(**kwargs):
    for i, v in enumerate(kwargs.items()):
    print(i, v)

key_kwargs(name1 = 'ayw', name2 = 'jung', name3= 'lee')
👉🏽
0 ('name1', 'ayw')
1 ('name2', 'park')
2 ('name3', 'jung')
```

>4. mix *args, **kwagrs
`*`면 `Tuple`, `**`면 `Dict`

```python
def mix_args_kwargs(arg1, arg2, *args, **kwargs):
    print(arg1, arg2, *args, **kwargs)

mix_args_kwargs(10, 10)
👉🏽 10 10 () {}

mix_args_kwargs(10, 20, 'park', 'AYW', name1='You',name2='ME')
👉🏽 10 20 ('park', 'AYW') {'name1': 'You', 'name2': 'ME'}

mix_args_kwargs(10, 10, 1, 2, 3, name='AYW', age=27)
👉🏽 10 10 (1, 2, 3) {'name': 'AYW', 'age': 27}
```

>5. 중첩함수(closure)
함수 내부에 함수를 또 선언하는 것
```python
def nested_func(num):
    def func_in_func(num):
        print(num)
    print('>>> in function')
    func_in_func(num+100)

nested_func(100)
👉🏽 >>>in function
200
```

>6. func_hint

```python
def func_mul(x: int) -> list:
    y1 = x * 100
    y2 = x * 200
    y3 = x * 300
    return [y1, y2, y3]
print(func_mul(100))
```

>7. lambda식
메로리가 절약되고, 가독성이 향상되며 코드가 간결해진다.
`일반 함수`는 객체 생성 이후 리소스(메모리)가 할당되지만,
  * 변수를 할당하면 메모리에 기억된다.
`lambda`는 즉시 실행(heap초기화) 이후 메모리를 초기화시킨다

```python
# 일반적 함수(변수 할당)
def mul_10(num:int) -> int:
    return num * 10

var_func = mul_10

print(var_func)
👉🏽 <function mul_10 at 0x7f9c160d53a0>
print(type(var_func))
👉🏽 <class 'function'>
print(var_func(10))
👉🏽 100

# lambda식
lambda_mul_10 = lambda x: x * 10

def func_final(x, y, func):
    print(x * y * func(5))

func_final(10, 10, lambda_mul_10)
👉🏽 5000

func_final(10, 10, lambda x: x + 500)
👉🏽 50500
```