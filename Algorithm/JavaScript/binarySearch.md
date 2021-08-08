## 📍 binary_search(이진탐색)

정렬된 리스트에서 원하는 항목을 찾기에 효율적인 알고리즘이다. 이진탐색을 가장 많이 사용하는 경우는 배열에서 어떤 항목을 찾아야 할 때인데, 예를들어 `1 ~ 100`까지의 범위에서 `37`이란 수를 찾으려면 1부터 100까지 1씩 증가하며 순서대로 찾는 방법이 있지만, 탐색범위를 `1/2`씩 줄이면서 찾는 방법이 있다. 순서대로 찾을 때는 최악의 경우 `100`번을 찾아야하지만 탐색범위를 반씩줄여 찾아간다면 최대 `7번`만에 원하는 값을 찾을 수 있다. 이진탐색을 코드로 구현하는 방법은 다음과 같다.

```javascript
// while
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let target = 3;

function binarySearch(arr, target){
    let min = 0;
    let max = arr.length - 1;
    let cnt = 0;
    
    while (min <= max){
        cnt += 1;
        let mid = Math.floor((min + max) / 2);
    
        if (arr[mid] === target){
            return "found!", cnt;
        }else{
            if (arr[mid] < target){
                min = mid + 1;
            }else{
                max = mid - 1;
            }
        }
    }
    return "not found!";
}
```

```javascript
// recursive
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let target = 3;

function binarySearch(start, end, arr, target){
    if (start > end){
        return "not found!";
    }

    let mid = Math.floor((min + max) / 2);

    if (arr[mid] === target){
        return "found!";
    }else{
        if (arr[mid] < target){
            binarySearch(mid + 1, end, arr, target);
        }else{
            binarySearch(start, mid - 1, arr, target);binarty
        }
    }
}
```

reference
1. <a href='https://ko.khanacademy.org/computing/computer-science/algorithms/binary-search/a/binary-search'>Khan Academy</a>


