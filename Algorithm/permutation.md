## permutation
> 순열(permutation): 서로 다른 `n개`에서 `r개`를 선택하여 일렬로 나열하는 것
> nPr으로 불림 
> 순서가 의미있을 때 사용함
> 참고영상: <a href='https://www.youtube.com/watch?v=1I6fAgEOPt4'>수학삼촌</a>

```python
import itertools

data = [1, 2]

for i in itertools.permutations(data, 2):
    print(list(i), end= ' ')

👉🏽 [1, 2] [2, 1]
```
