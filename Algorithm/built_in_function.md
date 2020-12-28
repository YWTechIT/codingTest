## built_in_function

1. eval(): 해당 수식을 계산한 결과를 반환
```python
result = eval('(3+5) * 7')
👉🏽 56
```

2. sorted(): `iterable` 객체가 들어왔을 때, 정렬된 결과를 반환
   * `iterable`: [ List ], ( Tuple ), [ Dictionary ]
   * `key = lambda a: a[x]`, 원소기준으로 오름 / 내림 차순 정렬가능

3. sort(): `list iterable` 객체는 기본으로 `sort()` 함수 사용 가능
   * iterable: [ List ], ( Tuple ), [ Dictionary ]


```python
# sorted ()
data_list = [3, 1, 2, 5]
data_tuple = (3, 1, 2, 5)
data_dict = [('안영우', 26), ('동생1', 23), ('동생2', 13), ('동생3', 11)]
data_dict_key = sorted([('안영우', 26), ('동생1', 23), ('동생2', 13), ('동생3', 11)], key = lambda x: x[1], reverse=True)

print(sorted(data_list))
👉🏽 [1, 2, 3, 5]
print(sorted(data_list, reverse=True))
👉🏽 [5, 3, 2, 1]

print(sorted(data_tuple))
👉🏽 [1, 2, 3, 5]
print(sorted(data_tuple, reverse=True))
👉🏽 [5, 3, 2, 1]

print(sorted(data_tuple))
👉🏽 [('동생1', 23), ('동생2', 13), ('동생3', 11), ('안영우', 26)]
print(sorted(data_tuple), lambda a: a[1])
👉🏽 [('안영우', 26), ('동생1', 23), ('동생2', 13), ('동생3', 11)]

# sort(only list)
data_list = [3, 1, 2, 5]
data_list.sort()

print(data_list)
👉🏽 [1, 2, 3, 5]
```