## 📍 generator(제너레이터)

### ⚡️ 임의의 조건으로 숫자 1억개 중 100개 뽑아내기
```python
def get_number():
    n = 0
    while True:
        n +=1
        yield n

g = get_number()

for i in range(1, 100):
    print(next(g))
👉🏽 1 2 3 4 5 ... 99
```