## itertools_function

1. permutation(): `list iterable` 객체에서 `r`개의 데이터를 뽑아 일렬로 나열하는 모든 경우(순열)

2. combination(): `list iterable` 객체에서 `r`개의 데이터를 뽑아 순서를 고려하지 않고 나열하는 모든 경우(조합)


```python
from itertools from permutations
from itertools from product
from itertools from combinations_with_replacement


data = ['A', 'B', 'C']

## 순열
data_permutation = list(permutations(data, 2))
👉🏽 [('A', 'B'), ('B', 'A')]

# 순열(중복허용)
data_product = list(product(data, repeat = 2))
👉🏽 [('A', 'A'), ('A', 'B'), ('B', 'A'), ('B', 'B')]

# 조합(중복허용)
data_combination = list(combinations_with_replacement(data, 2))
👉🏽 [('A', 'A'), ('A', 'B'), ('B', 'B')]
```