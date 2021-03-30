## 📍 Class
1. 프로그래밍에서는 현실 시계에 있는 개념들뿐만 아니라 컴퓨터 안에서만 쓰이는 개념들도 클래스로 만들어서 표현함
2. 클래스는 특정 개념을 표현만 할 뿐 사용하려면 인스턴스를 생성해야 함.
3. 메서드는 클래스가 아니라 self, 인스턴스를 통해 호출한다.
4. 인스턴스를 통해 호출하는 메서드를 인스턴스 메서드라고 부름
5. 보통 객체만 지칭 할 때는 그냥 객체(object)라고 부르고, 클래스와 연관지어서 말할때는 인스턴스(instance)라고 부른다.
6. 메서드 안에서 메서드를 호출하려면 `self.메서드()` 형식으로 호출해야한다. `self`없이 메서드 이름만 사용하면 클래스 바깥쪽에 있는 함수를 호출한다는 뜻이 된다.
7. 현재 `instance가` 특정 `class`인지 확인하는 함(True, False)
8. 속성은 `__init__` 메서드에서 만든다는 점과 `self.`를 붙여 값을 할당하는것이 중요하다. 클래스 안에서 속성을 사용할때도 `self.hello` 처럼 사용하면 된다.
9. class의 속성은 class에 속해있기때문에 모든 instance에서 접근이 가능함.
10. instance에서 class속성을 찾고 없으면, class 속성에서 찾게된다.
11. 각각의 개인 값을 갖고싶으면 self로 선언하자.
12. 인스턴스 속성은 인스턴스별로 독립되어 있으며 서로 영향을 주지 않는다.
13. 클래스 속성과 인스턴스 속성의 차이점
  * 클래스 속성: 모든 인스턴스 공유, 인스턴스 전체가 사용 하는 값을 저장할 때 사용(전역변수)
  * 인스턴스 속성: 인스턴스별로 독립되어있음. 각 인스턴스 값을 따로 저장할때 사용(지역변수)
14. 클래스에 인스턴스를 만들지 않으면 다른 객체간의 공유가 가능하다.
15. mutable하게 사용하려면 self.를 선언해주기

> 클래스 변수: 클래스에 의해 생성된 모든 객체가 같은 값을 조회할 때 사용하는 변수
> 인스턴스 변수: 인스턴스화 될 때마다 새로운 값이 할당되며 서로 다른 객체 간에는 값을 공유할 수 없는 변수
  * 객체 단위로 값이 따로 관리되는 변수는 반드시 인스턴스 변수 사용
  * 클래스 변수에 string을 사용해도 문자열이 immutable이기 때문에 값이 변하지 않는다
  * 클래스 변수는 객체 이름이 아닌 클래스 이름으로 접근, 되도록 값이 변경되지 않는 경우에 사용하는 것이 안전하다!

```python
# instance변수 선언의 필요성
# 값이 공유되는 예시
class Exercise:
    name = []

    def __init__(self, exercise_list):
        self.exercise_list = exercise_list

    def add_name(self, name):
        self.name.append(name)

AYW = Exercise('soccer')
AYW.add_name('jeong')

AYU = Exercise('basketball')
AYW.add_name('yeong')

print(AYW.name)
👉🏽 ['jeong', 'yeong']

print(AYU.name)
👉🏽 ['jeong', 'yeong']

# 올바른 코드
class Exercise:

    def __init__(self, exercise_list, name):
        self.exercise_list = exercise_list
        self.name = name

    def add_name(self, name):
        self.name.append(name)


AYW = Exercise('soccer', 'jeong')
AYU = Exercise('basketball', 'ju')

print(AYW.name)
👉🏽 jeong

print(AYU.name)
👉🏽 ju

```

```python
# 값이 공유되지 않는 예시(string)
class Exercise:
    exercise = 'soccer'

    def __init__(self, name):
        self.name = name

    def play_exercise(self):
        print(self.name + '는(은) 현재 ' + self.exercise + '중 입니다.')

AYW = Exercise('안영우')
JBY = Exercise('정보영')

JBY.exercise = 'basketball'
AYW.play_exercise()
👉🏽 안영우는(은) 현재 soccer중 입니다.

# 새로운 값으로 바뀌어도 이전에 생성한 string 객체는 변하지 않는다
# immutable 클래스 변수 값을 변경하여 객체가 교체되면, 변경 전 생성된 객체의 클래스 변수는 이전에 생성한 값을 가리킨다.
Exercise.exercise = 'tabletennis'
KMJ = Exercise('기모찌')

AYW.play_exercise()
👉🏽 안영우는(은) 현재 tabletennis중 입니다.
JBY.play_exercise()
👉🏽 정보영는(은) 현재 basketball중 입니다.
KMJ.play_exercise()
기모찌는(은) 현재 tabletennis중 입니다.
```



---
```python
class Person
    def greeting(self):
        return 'Hello'
    def hello(self):
        self.greeting()

# AYW는 Person의 instance
AYW = Person()
print(AYW.greeting())
print(isinstance(AYW, Person))
```

```python
class Person:
    def __init__(self, 매개변수1, 매개변수2):
        self.속성1 = 매개변수1
        self.속성2 = 매개변수2
```
9. `self`는 인스턴스 자기 자신을 의미함

```python
# 비공개 속성 사용하기
# 클래스 안의 메서드에서만 접근 할 수 있음
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__wallet = __wallet

    def pay(self, amount):
        self.__wallet -= amount
        print('now, you have {0}dollars'.format(self.__wallet))

maria = person('AYW', 4000)
maria.pay(3000)
```

---
## 📍 정적 메서드
1. 정적 메서드를 사용하려면 `@staticmethod`를 붙인다.
2. 정적 메서드는 매개변수에 self를 지정하지 않음
3. @를 데코레이터라고 하며 메서드(함수)에 추가 기능을 구현할때 사용함
4. 정적메서드는 self를 받지 않으므로 인스턴스 속성에는 접근할 수 없음
5. 정적 메서드는 인스턴스 속성, 인스턴스 메서드가 필요 없을 때 사용함
6. 정적 메서드는 메서드의 실행이 외부 상태에 영향을 끼치지 않는 순수 함수를 만들 때 사용함
7. 입력 값이 같으면 언제나 같은 출력 값을 반환함
8. 정적 메서드는 인스턴스의 상태를 변화시키지 않는 메서드를 만들때 사용함


```python
class Calc:
    @staticmethod
    def add(a, b):
        print(a+b)

    @staticmethod
    def mul(a, b):
        print(a * b)

Calc.add(10, 20)
Calc.mul(10, 20)
```

---
## 📍 클래스 메서드
1. class method는 메서드 위에 @classmethod를 붙인다.

```python
class Person:
    count = 0

    def __init__(self):
        Person.count +=1

    @classmethod
    def print_count(cls):
        print(cls.count)

ted = Person()
maria = Person()

Person.print_count()
```


---
### 💡 객체 vs 인스턴스
파이썬에서 클래스에 의해 만들어진 객체를 인스턴스라고한다. 
예를들어, `eraser=WriteSupplies()`라고 선언했을 때, 
`eraser`는 객체이고, `eraser`객체는 `WriteSupplies`의 인스턴스라고 부른다.
즉, 인스턴스라는 말은 특정 객체(`eraser`)가 어떤 클래스(`WriteSupplies`)의 객체인지를 관계위주로 설명한다.

>reference: 점프 투 파이썬 - 클래스(p.172)