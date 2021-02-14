## for문을 이용한 ascii코드 출력
> 1. ord: number to ascii
> 2. chr: ascii to number

### 📍 영어 소문자 출력
```python
for i in range(97, 123):
    print(chr(i), end= ' ')
👉🏽 a b c d e f g h i j k l m n o p q r s t u v w x y z
```

---

### 📍 영어 대문자 출력
```python
for i in range(65, 91):
    print(chr(i), end= ' ')
👉🏽 A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
``` 

---

### 📍 모듈 호출
```python
import string

digits = string.digits
upper_case = string.ascii_uppercase

print(digits)
print(upper_case)

👉🏽 '0123456789'
👉🏽 '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
```

