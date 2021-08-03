## 📍 프로그래머스 1단계 - 문자열을 정수로 바꾸기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12925'>프로그래머스 1단계 - 문자열을 정수로 바꾸기</a>

### ⚡️ 나의 풀이

단순하게 문자열 `s`를 숫자로 변환하면 되는데 `Number`로 풀면되는것 아닌가 했는데 자바스크립트는 이상하게도 `stringType` 앞에 부호를 붙이면 `numberType`으로 바뀌는 이상한 성질이 있었다. 그리고 `stringType과` `numberType`간의 사칙연산이 가능도 가능했는데 이상하게도 `string` + `number` 는 `string` + `string`의 형태를 보였고, 나머지는 `string` + `number` 형태를 보였다. 자바스크립트의 느슨한 타입 형태에 입이 떡 벌어졌다. 🤭 🤭  

다음과 같은 예제를 보자.

```javascript
console.log(10 + '10')    // 1010
console.log(10 - '10')    // 0
console.log(10 * '10')    // 100
console.log(10 / '10')    // 1
```

코드는 다음과 같다.

```javascript
// 내가 작성한 코드
function solution(s) {
    return Number(s);
}

// 다른 사람의 코드
function solution(s) {
    return +s
}
```

---
## 📍 프로그래머스 1단계 - 제일 작은 수 제거하기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12925'>프로그래머스 1단계 - 제일 작은 수 제거하기</a>

### ⚡️ 나의 풀이
가장 작은 수를 찾는 문제인데, `min` 함수의 활용법을 잘 몰랐다. 그래서 반복문을 선언해서 최소값을 하나씩 찾는 방법과 해당 최소값을 `indexOf`로 몇 번째 위치해있는지 찾았다. 

여담으로 처음에 `Math.min`을 사용하니까 `NaN`이 뜨길래 왜 그러지? 하니까 `min`함수는 개별 숫자를 받는데 배열을 넣어서 `NaN`이 <a href='https://pythonq.com/so/javascript/1507271'>뜬다고 했다.</a> 해결방법으로는 `spread` 연산자를 넣거나 `Math.min.apply(null, arr)`처럼 `apply`함수를 사용해서 배열 내에서도 `min`값을 찾을 수 있다.

```javascript
// 첫 번째 코드
function solution(arr) {
    let minValue = 9999;

    for (let item of arr) {
        if (minValue > item) {
            minValue = item;
        }
    }

    const filterArr = arr.filter((item) => item !== minValue);

    if (filterArr.length === 0) {
        return [-1];
    } else {
        return filterArr;
    }
}
```

```javascript
// 두 번째 코드
function solution(arr) {
    if (arr.length <= 1){
        return [-1]
    }

    const minTarget = Math.min(...arr)
    arr.splice(arr.indexOf(minTarget), 1)
    return arr
}
```

---
## 📍 프로그래머스 1단계 - 문자열 다루기 기본
<a href='https://programmers.co.kr/learn/courses/30/lessons/12918'>프로그래머스 1단계 - 문자열 다루기 기본</a>

### ⚡️ 나의 풀이

문자열로 받은 값을 숫자로 변환해야하는데 단순 `Number` 함수를 사용하니까 오답판정을 받았다. 곰곰이 생각해보니까 `e`(지수)값과 `.` 소수 값도 `Number`로 통해서 숫자로 치환하기 때문이다. 문제는 숫자로만 구성되어있어야 하므로 `e`, `.`은 문자 그대로를 받아 `false`를 리턴해야한다. 따라서 초기에 `e`를 찾아주는 조건을 넣었고 숫자로 바꿀 때는 `isNaN` 함수를 사용해서 숫자로 바꿀 수 있는지 여부를 확인했다.

```javascript
// 나의 코드
function solution(s) {
    if (s.indexOf('e') > 0){
        return false
    }

    if ((s.length === 4 || s.length === 6) && (isNaN(Number(s)))) === false) {
        return true
    }else{
        return false
    }
}
```

---
## 📍 프로그래머스 1단계 - 짝수와 홀수
<a href='https://programmers.co.kr/learn/courses/30/lessons/12937'>프로그래머스 1단계 - 짝수와 홀수</a>

### ⚡️ 나의 풀이

조건문을 이용해 `if-else`로 나타낼 수 있지만, 삼항연산자를 이용해 더욱 간단하게 작성 할 수도 있다.

```javascript
// 삼항연산자
function solution(num) {
    return (num % 2) ? "Odd" : "Even"
}

// 조건문
function solution(num) {
    if (num % 2 == 1){
        return "Odd"
    }else{
        return "Even"
    }
}
```

---
## 📍 프로그래머스 1단계 - 하샤드 수
<a href='https://programmers.co.kr/learn/courses/30/lessons/12947'>프로그래머스 1단계 - 하샤드 수</a>

### ⚡️ 나의 풀이

`number` 타입으로 주어진 값의 자릿수를 구할 때 `for`문을 사용하고, `JS`의 문자열 특성을 이용해서 구했다.

1. `x`를 `String` 형태로 바꾼다.
2. `for - of` 반복문을 이용해서 `tempSum`을 누적한다. 이때, `JS`에서는 문자열 앞에 `+`를 붙이면 `number`형으로 바뀐다.
3. 삼항연산자를 이용해서 자릿수로 나누어 떨어지면 `true`, 나누어 떨어지지 않으면 `false`를 `return`한다.

```javascript
function solution(x, tempSum = 0) {
    
    for (let digit of String(x)){
        tempSum += (+digit)
    }
    
    return (x % tempSum) ? false : true
}
```

---
## 📍 프로그래머스 1단계 - 평균 구하기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12944'>프로그래머스 1단계 - 평균 구하기</a>

### ⚡️ 나의 풀이
`python`과는 다르게 `JS`에서는 `sum` 함수가 따로 없어서 `reduce` 함수를 이용해서 평균을 구했다. `reduce`는 4개의 인자 `누산기(acc), 현재 값(cur), 현재 인덱스(idx), 원본 배열(src)`을 
가진다. 또, `initialValue` : `callback` 함수를 실행할 때, `accumulator` 의 값( `default` : arr[0], `currentIndex` : 1부터 시작, 가능하면 초기값을 입력하는것을 잊지말자.

```javascript
// 나의 코드
function solution(arr) {
    let sumArr = arr.reduce((acc, cur) => {
        return acc + cur;
    });

    return sumArr / arr.length;
}

// 한 줄 표현
function solution(arr) {
    return arr.reduce((acc, cur) => {return acc + cur}) / arr.length;
}
```

---
## 📍 프로그래머스 1단계 - x만큼 간격이 있는 n개의 숫자
<a href='https://programmers.co.kr/learn/courses/30/lessons/12954'>프로그래머스 1단계 - x만큼 간격이 있는 n개의 숫자</a>

### ⚡️ 나의 풀이
처음 `arr`을 어떻게 0으로 초기화 시켜야 할지 고민을 많이 했다. `python`에서는 단순하게 `[0] * n`을 작성하면 되는데 `JS`에서는 다른 방법을 찾아야 한다. 가독성을 제쳐두고 다음과 같은 방법을 찾았다.

1. `let answer = [...Array(n)].map(() => 0);`
2. `let answer = Array(n).fill(0)`
3. `let answer = Array.apply(null, Array(n)).map(() => 0);`

이 중에서 가독성이 가장 좋은 코드는 2번이었다. 다른사람의 코드에서 `increase`를 사용 할 필요없이 `idx`로 해결하니까 코드가 훨씬 간결해졌다.

1. `n`만큼의 길이를 각각 `x`로 초기화시킨다. (초기값: `[2, 2, 2, 2, 2]`)
2. `map` 함수를 사용하여 `idx`에 1씩 더해준 값에 현재 `val`를 곱하여 반환한다.

```javascript
// 나의 코드
function solution(x, n) {
    let answer = [...Array(n)].map(() => 0);
    let increase = x;
    answer.map((val, idx) => {answer[idx] = increase, increase += x})
    return answer
}

// 나의 코드2
function solution(x, n) {
    let answer = Array.apply(null, Array(n)).map(() => 0);
    let increase = x;
    
    answer.forEach(function(val, idx){
        answer[idx] = increase;
        increase += x;
    })
    
    return answer
}
```

```javascript
// 다른 사람의 코드
function solution(x, n) {
    return Array(n).fill(x).map((v, i) => (i + 1) * v)
}
```

---
## 📍 프로그래머스 1단계 - 행렬의 덧셈
<a href='https://programmers.co.kr/learn/courses/30/lessons/12950'>프로그래머스 1단계 - 행렬의 덧셈</a>

`for`문 대신 `map`을 사용하면 훨씬 가독성이 좋아진다. 또 처음 `map`에서 나온 `item`에 또 `map`을 적용해서 리스트를 벗길 수 있다. 자주 써먹어야겠다. 주의 할 점은 `map`은 배열을 `return`시킨다는 점이다.

```jsx
// 나의 코드
function solution(arr1, arr2, answer = []) {
    const rowLength = arr1.length;
    const columnLength = arr1[0].length;
    
    for (let i = 0; i < rowLength; i++){
        let tmpAnswer = [];
        for (let j = 0; j < columnLength; j++){
            tmpAnswer.push(arr1[i][j] + arr2[i][j])
        }
        answer.push(tmpAnswer)
    }
    return answer
}
```

```javascript
// 수정 코드
function solution(arr1, arr2, answer = []) {
  for (let i = 0; i < arr1.length; i++) {
    answer[i] = [];
    for (let j = 0; j < arr1[i].length; j++) {
      answer[i].push(arr1[i][j] + arr2[i][j]);
    }
  }
  return answer;
}
```

```javascript
// 다른 사람의 코드
function solution(arr1, arr2) {
    return arr1.map((item, i) => item.map((val, j) => val + arr2[i][j]))
  }
```

---
## 📍 프로그래머스 1단계 - 같은 숫자는 싫어
<a href='https://programmers.co.kr/learn/courses/30/lessons/12906'>프로그래머스 1단계 - 같은 숫자는 싫어</a>

### ⚡️ 나의 풀이
맨 마지막 원소를 비교할 때는 `idx+1`이 없기때문에 오류가 나지 않을까 하면서 `filter`를 사용했는데, 마지막 `idx+1`은 `undefined`가 반환돼서 비교가 가능했다. `!=`와 `!==`의 차이는 형 변환(type casting)이후 비교를 하는지 안하는지의 차이인데 여기서는 입력 모두 `Number`형 이기 때문에 `!=`로 작성해도 된다.

```javascript
// filter
function solution(arr){
   return arr.filter((item, idx) => item !== arr[idx+1]);
}

// forEach
function solution2(arr, answer = []){
    arr.forEach((item, idx) => {
    if(item !== arr[idx+1]){
        answer.push(item)}
    })

    return answer;
}
```
