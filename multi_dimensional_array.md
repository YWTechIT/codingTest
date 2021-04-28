## 📍 다차원 배열 구현 팁
1. arr[세로][가로]로 표현한다.
2. 배열상에서 인덱스는 0부터 표현하기때문에 `-1`해주는것을 잊지말자.

```python
# 일반적인 2차원 배열 표현(5, 5)
arr = [[0] * 5 for _ in range(5)]
👉🏽 [[0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0], [0, 0, 0, 0, 0]]

# numpy 라이브러리 사용
import numpy as np
arr_np = np.zeros((5, 5), dtype=int)
print(arr_np)

👉🏽 [[0 0 0 0 0]
 [0 0 0 0 0]
 [0 0 0 0 0]
 [0 0 0 0 0]
 [0 0 0 0 0]]

for arr in arr_np:    # 예쁘게 출력하기
    print( *arr )

👉🏽
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
0 0 0 0 0
```