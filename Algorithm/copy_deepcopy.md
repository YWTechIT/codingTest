## 📍 copy(얕은복사), deepcopy(깊은복사)

### ⚡️ 얕은복사
> 현재 가르키고 있는 instance, 변수의 id값을 그냥 복사한다. 내부는 어떤지 모른다.
> a의 객체를 참조하는게 아니라 복사해놓은 객체를 참조하기때문에 a가 변해도 b의 값은 변하지 않는다.

```python
# Dictionary
a = {'name': 'AN'}
b = a
print(a == b, a is b)
👉🏽 True True
print(id(a), id(b))
👉🏽 140688105958592 140688105958592

# Tuple
c = (1, 2, 3)
d = c
print(c == d, c is d)
👉🏽 True True
print(id(c), id(d))
👉🏽 140688106591360 140688106591360

```

---
### ⚡️ 깊은복사
> 객체 내부의 정의되어있는 또 다른 속성값의 할당되어있는 reference id 까지 복사 
> 메모리에 부하가 많이 걸릴 수 있다.
> b는 a가 참조하는 객체의 참조마저도 복사하니까 재귀적으로 호출한다. 재귀 마지막으로 참조하는 객체의 값은 서로 같다.

### 💡 매개변수 사용시 주의 점
`immutable`형은 원본도 변경된다.(주소도 같이 넘기기 때문)

```python
def mul(a, b):
    a += b
return a

a = [10, 20, 30]
b = [40, 50]
print(mul(a, b), a, b)
```