## counter_function

1. counter(): 등장 횟수를 세는 기능
   * `list iterable` 객체가 주어졌을 때, 해당 객체 내부의 원소가 몇 번씩 등장했는지 알려준다

```python
from collections import Counter
data_counter = ['red', 'blue', 'blue', 'orange', 'green', 'blue', 'green']

print(Counter(data_counter))
👉🏽 Counter({'blue': 3, 'green': 2, 'red': 1, 'orange': 1})

print(dict(data_counter))
👉🏽 {'red': 1, 'blue': 3, 'orange': 1, 'green': 2}

print(counter['blue'])
👉🏽 3
```