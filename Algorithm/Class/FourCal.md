## 📍 사칙연산 Class
1. Class명: `FourCal`
2. 사용 method: `setdata`, `sum`, `minus`, `mul`, `div`
3. a는 객체이다.
4. a는 FourCal의 인스턴스(instance)이다.


```python
class FourCal:
    def setdata(self, first, second):
        self.first = first
        self.second = second

    def sum(self):
        return self.first + self.second

    def minus(self):
        return self.first - self.second

    def mul(self):
        return self.first * self.second

    def div(self):
        return self.first / self.second

a = FourCal()
a.setdata(1, 2)

print(a.sum())
print(a.mul())
print(a.minus())
print(a.div())

print(a.first)
print(a.second)
```