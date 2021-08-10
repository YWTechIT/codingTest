## 📍 선택정렬(Selection Sort)
1. 자신보다 하위 `index`를 검사하여 자신보다 작은 값이 있으면 해당 값과 `swap`하는 방법
2. 기본적인 정렬방법이며, 이미 정렬이 되어있는 경우도 `O(N^2)`의 시간이 걸린다. 매번 정해진 자리에 올 수 있는 최소값을 찾아야 하기 때문이다.
3. 성능이 매우 떨어지는 정렬방법이다.

```javascript
let arr = [2, 1, 4, 5, 6, 7, 9];

console.log(selectionSort(arr));

function selectionSort(arr){
    for (let i = 0; i < arr.length; i ++){
        for (let j = i + 1; j < arr.length; j ++){
            if (arr[i] > arr[j]){
                let temp;
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr
}
```

---
## 📍 삽입정렬(Insertion Sort)
1. 왼쪽 `index`가 `cur`보다 크면 `cur`이 더 작기 때문에 `cur`을 왼쪽으로 이동시키는 방법
2. 안정적인 정렬방법이며, 거의 정렬되어있을 때 사용하면 `O(N)`의 시간으로 효과적으로 정렬시킬 수 있다. 정렬이 되지 않은 상태에서는 `O(N^2)`
3. 정렬이 되었는지 안되었는지 테스트하는 용도로 사용될 수 있다.

```javascript
let arr = [2, 1, 4, 5, 6, 7, 9];

console.log(insertionSort(arr));

function insertionSort(arr){
  for (let i = 1; i < arr.length; i ++){
    let cur = arr[i];
    let leftIdx = i - 1;

    while (leftIdx >= 0 && arr[leftIdx] >= cur){
      arr[leftIdx + 1] = arr[leftIdx];
      leftIdx -= 1;
    }

    arr[leftIdx + 1] = cur;
  }

  return arr
}
```

## 📍 프로그래머스 1단계 - K번째 수
<a href='https://programmers.co.kr/learn/courses/30/lessons/42748'>프로그래머스 1단계 - K번째 수</a>

### ⚡️ 나의 풀이

`JS`로는 처음 풀어본 문제인데, 나는 단순 `for`문으로 풀었지만 `for ~ of`로 풀면 조금 더 깔끔하게 풀 수 있다. 또 `slice`는 `start, end` 인덱스를 잘 계산해야 놓치지 않는다. `slice`에서 `end`는 포함하지 않는다는 것을 잊지말자.

추가로 `sort`는 `element`를 문자열로 취급하여 정렬하기 때문에, 유니코드 순서대로 정렬된다. 따라서 파라미터를 두개를 넘겨주고 오름차순은 `a-b`, 내림차순은 `b-a` 하는 과정을 거치자.

```javascript
// for 
function solution(arr, commands) {
  const answer = [];

  for (let i= 0; i < i.commands.length; i++) {
    let command = commands[i];
    let newArr = arr.slice(command[0] - 1, command[1]);
    newArr.sort((a, b) => a - b);
    answer.push(newArr[command[2] - 1]);
  }
  return answer;
}
```

```javascript
// for ~ of
function solution(arr, commands) {
  const answer = [];

  for (let command of commands) {
    let newArr = arr.slice(command[0] - 1, command[1]);
    newArr.sort((a, b) => a - b);
    answer.push(newArr[command[2] - 1]);
  }
  return answer;
}
```

```javascript
// map함수
function solution(arr, commands) {
  const answer = [];

  commands.map((command) => {
    let newArr = arr.slice(command[0] - 1, command[1]);
    newArr.sort((a, b) => a - b);
    answer.push(newArr[command[2] - 1]);
  });

  return answer;
}
```