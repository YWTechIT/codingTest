## 📍 Python coding convention
1. 코드를 작성하다 보면 나보다 다른 사람들이 보는 경우가 더 많다. (가독성은 중요하다.)
2. 멍청하게 일관성을 고집하는 것은 소인배의 발상이다(A Foolish Consistency is the Hobgoblin of Little Minds)
3. 절대 탭 문자와 공백 문자(4글자)를 섞어 쓰지 마라.

### ⚡️ 표현식, 구문에서의 공백 문자
```python
# Good
spam(ham[1], {eggs: 2})
if x == 1: print(123)
exe_func([1,2,3])

# Bad
spam( ham[ 1 ], { eggs :  2})
if x == 1 : print(123)
exe_func ([1,2,3])
```

---
### ⚡️ 기타 권고사항
```python
# Good
i = i + 1
i += 1
x = x*2 -1
sum = x*x + y*y
c = (a+b) * (a+b)

# Bad
i=i+1
i +=1
x = x * 2 - 1
sum = x * x + y * y
c = (a + b) * (a - b)
```







> reference
1. <a href='https://b.luavis.kr/python/python-convention'>번역본</a>
2. <a href='https://www.python.org/dev/peps/pep-0008/'>원본</a>