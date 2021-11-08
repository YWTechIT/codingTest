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

---
## 📍 프로그래머스 1단계 - 가운데 글자 가져오기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12903'>프로그래머스 1단계 - 가운데 글자 가져오기</a>

### ⚡️ 나의 풀이

첫번째는 `slice` 문을 이용했고, 두번째는 `slice, splice`문을 이용했는데 `splice`는 `Array` 타입에서만 지원하는 함수여서 `split`으로 `Array`로 바꿔주고 적용햇다. 가독성은 첫번째 코드가 더 좋은것같다. 주의 할 점은 `splice` 문을 사용 할 때 `end`는 포함하지 않는다는 점과 컴퓨터는 `index`를 0부터 세는 부분이다.

```javascript
// slice
function solution(s) {
    return s.length%2 == 1 ? s[s.length/2 | 0] : s.slice(s.length/2 - 1, s.length/2 + 1)
}

// slice, splice
function solution(s) {
    return s.length%2 == 1 ? s[s.length/2 | 0] : s.split("").splice(s.length/2 -1, 2).join('')
}
```

---
## 📍 프로그래머스 1단계 - 정수 제곱근 판별
<a href='https://programmers.co.kr/learn/courses/30/lessons/12934'>프로그래머스 1단계 - 정수 제곱근 판별</a>

### ⚡️ 나의 풀이
제곱근이 아니라면 `sqrt`함수를 사용했을 때 `float`이 나오고, 제곱근이라면 `number`형이 나올것이다. 그래서 `parseInt`와 `parseFloat` 형 비교를 사용했다. 또는 `isInteger` 함수를 사용해서 제곱근이 정수인지 아닌지를 비교해도 된다. `return`문은 삼항연산자를 이용해서 작성했다.

```javascript
function solution(n) {
    return ((parseInt(Math.sqrt(n)) === parseFloat(Math.sqrt(n))) ? Math.pow(Math.sqrt(n)+1, 2) : -1)
}
```

---
## 📍 프로그래머스 1단계 - 직사각형 별찍기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12969'>프로그래머스 1단계 - 직사각형 별찍기</a>

### ⚡️ 나의 풀이
`row`는 `for`문 대신`repeat` 함수를 이용하여 표현했고, `column`은 `for`문을 이용해서 표현했다. 나는 `answer`에 `push`하고나서 `join`으로 문자열로 바꿔줬는데, 그냥 `console.log`해도 정답판정이 나왔다.

```javascript
// 나의 코드
process.stdin.setEncoding('utf8');
process.stdin.on('data', data => {
    const n = data.split(" ");
    const a = Number(n[0]), b = Number(n[1]);

    let answer = [];
    let row = "*".repeat(a);

    for (let i = 0; i < b; i++){
        answer.push(row);
    }
    console.log(answer.join("\n"))
});

// 다른사람의 코드
process.stdin.setEncoding('utf8');
process.stdin.on('data', data => {
    const n = data.split(" ");
    const a = Number(n[0]), b = Number(n[1]);

    let answer = [];
    let row = "*".repeat(a);
    
    for (let i = 0; i < b; i++){
        console.log(row)
    }
});
```

---
## 📍 프로그래머스 2단계 - 짝지어 제거하기
<a href='https://programmers.co.kr/learn/courses/30/lessons/12973'>프로그래머스 2단계 - 짝지어 제거하기</a>

### ⚡️ 나의 풀이
이전에 한 스타트업의 `FE` 코딩테스트를 치뤘을 때 지금 문제와 비슷하게 출제되었다. 이 문제의 핵심은 같은 알파벳이 2개 붙어있는 짝을 어떻게 찾는지가 핵심인데, 결론적으로 스택(`stack`)을 이용해서 짝을 찾았다. 

1. 현재 `stack`이 비어있지 않고, `stack[-1]`이 현재 `x`와 같으면 `stack`의 제일 마지막 원소를 `pop`한다. (짝지어진 문자열이기 때문)
2. 1번 조건에 충족하지 않으면 모두 `stack`에 넣는다.
3. 주어진 문자열을 끝까지 탐색하고 남은 `stack`의 길이가 1보다 크면 짝지어 제거에 실패했기 때문에 `0`을 `stack`의 길이가 0이면 짝지어 제거에 성공했기 때문에 `1`을 리턴한다.

```javascript
function solution(s) {
    let stack = [];
    
    for (let x of s) {
        if (stack && stack[stack.length - 1] === x) {
            stack.pop();
        }else stack.push(x);
    }

  return stack.length >= 1 ? 0 : 1;
}
```

---
## 📍 프로그래머스 2단계 - 프린터
<a href='https://programmers.co.kr/learn/courses/30/lessons/42587'>프로그래머스 2단계 - 프린터</a>

### ⚡️ 나의 풀이
스택/큐를 이용한 문제인데, 중요도에 따라 출력해야하는 문서가 달라지므로 주의한다. `location`과 동일한 `index`를 쉽게 찾기 위해 `index` 배열을 새로 만들어 `priorities.length`만큼 `index`의 값을 주었다.

1. `priorities`의 `max`값을 찾는다.
2. `priorities[0]`값과 `max`가 동일한지 확인한다.(중요도가 가장 높은 문서인지 확인하는 작업) `max`값과 동일하면 `shift`시키는데, 이때 `location`이랑 동일한지도 확인한다.
3. `priorities[0]`값과 `max`가 동일하지 않으면 나머지 목록 중 중요도가 높은 문서가 있으므로 제일 뒤로 보낸다. `arr.push(arr.shift())`

```javascript
function solution(priorities, location){
  let n = priorities.length;
  let index = Array.from({length: n}, (v, k) => k );
  let cnt=1;

  while(priorities.length !== 0){
    let max = Math.max.apply(null, priorities);
    if (max === priorities[0]){
      if (index[0] === location) return cnt;
      else priorities.shift(), index.shift(), cnt++;
    }else{
      priorities.push(priorities.shift());
      index.push(index.shift());
    }
  }
}
```

---
## 📍 프로그래머스 1단계 - 모의고사
<a href='https://programmers.co.kr/learn/courses/30/lessons/42840'>프로그래머스 1단계 - 모의고사</a>

### ⚡️ 나의 풀이
풀이 방식을 떠올리는게 조금 어려웠다. 각각의 수포자들이 찍는 방식에는 일정한 패턴이 있었고, 이 패턴을 어떤 방식으로 활용할지 생각하는게 큰 관건이었다. 결론적으로 `answer`의 `index`와 각각 수포자들의 `i % 패턴.length` 으로 확인했다.

1. 각각의 수포자들의 반복되는 패턴을 `mathGiveUpMethod`에 담아둔다.
2. 가장 많이 문제를 맞힌 사람을 알기 위해 `3`만큼 0으로 배열을 선언한다.
3. `answer` 반복문을 돌면서 현재 `answer[i]`와 각각의 수포자의 패턴을 비교하여 동일한지 다른지 확인한다 여기서 `i%5`, `i%8`, `i%10`을 한 이유는 만약, `answer`의 `length`가 `[0].length`, `[1].length`, `[2].length`보다 길게되면 각각의 `index`를 비교를 할 수 없기 때문에 `answer.length`길이가 크더라도 수포자는 각각 동일한 패턴을 지녔으므로 해당 패턴의 길이만큼 나눈 나머지의 값을 비교해주면 된다.
4. 정답을 제일 많이 맞춘 개수 `max`에 저장한다.
5. 정답이 순서대로 들은 배열과 4번에서 구한 `max`를 비교하면서 `max`와 같은 값의 `index`를 `maxGroup`에 넣는다. (해당 사람이 누구인지 알기 위해)

```javascript
function solution(answers){
  let mathGiveUpMethod = [[1, 2, 3, 4, 5], [2, 1, 2, 3, 2, 4, 2, 5], [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]];
  let cntGroup = Array.from({length: 3}, ()=>0);

  for (let i=0; i<answers.length; i++){
    if (answers[i] === mathGiveUpMethod[0][i%5]) cntGroup[0]++;
    if (answers[i] === mathGiveUpMethod[1][i%8]) cntGroup[1]++;
    if (answers[i] === mathGiveUpMethod[2][i%10]) cntGroup[2]++;
  }
  
  let max = Math.max.apply(null, cntGroup);
  let maxGroup = [];
  
  for (let i=0; i<3; i++){
    if (cntGroup[i]===max) maxGroup.push(i+1);
  }
  
  return maxGroup;
}
```

---
## 📍 프로그래머스 2단계 - 기능개발
<a href='https://programmers.co.kr/learn/courses/30/lessons/42586'>프로그래머스 2단계 - 기능개발</a>

### ⚡️ 나의 풀이
이 문제에서 제일 크게 거쳐야 하는 기능은 2가지로 나뉜다. 첫번째는 `progresses`와 `speeds` 각각의 값을 이용해서 배포가 며칠이 소요되는지 구해야하고, 두번째는 배포 날짜를 모아둔 값에서 제일 처음부터 배포를 할 때 다음값이 현재 배포 일 수보다 작으면 같이 배포되고, 더 크면 나중에 배포되는 `cnt`값을 구해야한다. 내가 풀 때는 첫번째까지는 무난하게 구했는데 두번째 `cnt`를 구하는 방식이 좀 처럼 떠오르지 않았다. 도저히 방법이 떠오르지 않아 다른 사람은 어떻게 풀었는지 봤는데, `for`문 안에 `i`, `j`를 동시에 선언하고 `count`를 한게 너무 신기했다. 거기에 `j`는 `전치연산자`를 사용했는데, `전치연산자`는 예를 들어 현재 `j`값이 1일 때 +1을 더하고 `2`인 상태에서 계산을 하는 방법이다. 이런 계산을 할 때 사용하는 방법을 알았으니 다음에 써먹으면 된다. 참고로 지금 코드가 아닌 이전 코드를 제출 했을 때 테스트케이스 2번에 실패했는데, 그 이유는 `Math.ceil`을 `100-progress`에만 감싸줘서 그렇다. 대신에 전체 `Math.ceil((100-progress) / speeds[idx]))`에 감싸주면 정답처리를 받을 수 있다.

1. `progresses`에 `map`연산자를 사용해 `100-progress`를 `speeds[idx]`로 나눠주었다. `map` 연산자에 파라미터는 첫번째로 `value` 두번째로 `idx`가 오는 특징을 이용했다.
2. 초기 `max`값은 `contributeDays[0]`으로 설정했다. 이렇게 해야 대소비교가 정상적으로 가능하다.
3. `contributeDays`에 반복문을 사용해 현재 값보다 `max`가 더 크면 이전 값들까지 같이 배포 한다. 반대의 경우에는 `max`를 갱신시키고 해당일부터 배포한다. 이때 `j`를 전치연산자로 값을 늘려 새로 `answer`에 1을 추가했다.

```javascript
function solution(progresses, speeds){
  let n = progresses.length;
  let contributeDays = progresses.map((progress, idx) => Math.ceil((100-progress) / speeds[idx]));
  let max = contributeDays[0];
  let answer = [0];

  for (let i=0, j=0; i<n; i++){
    if (max >= contributeDays[i]) answer[j]++;
    else{
      max = contributeDays[i];
      answer[++j] = 1;
    }
  }
  return answer;
}
```

---
## 📍 프로그래머스 2단계 - 다리를 지나는 트럭
<a href='https://programmers.co.kr/learn/courses/30/lessons/42583'>프로그래머스 2단계 - 다리를 지나는 트럭</a>

### ⚡️ 나의 풀이
<a href='https://ywtechit.tistory.com/187'>이전</a>에 `python`으로 풀어본 경험이 있다. 오랜만에 풀어서 이전에 푼 기억은 잘 나지 않았다. 처음에는 조금 헤맸는데 나름의 순서를 그려가며 풀었다. 제일 눈여겨봐야 할 점은 `bridge`는 초마다 항상 `shift()`를 해주고 `weight`는 `bridge`의 `shift()`값을 더해준다는 것과 `bridge`의 초기값은 `bridge_length`만큼 0으로 초기화 해준다. 그래야 트럭이 `bridge_length`만큼 `bridge`에 올라갈 수 있다.

1. `bridge`는 `weight`와 관계없이 초마다 `shift()`한다.
2. `trucks`가 남아있으면 `weight`의 조건을 따진다. 만약, 현재 무게와 다음에 올 트럭의 무게를 더했을 때 `limit`보다 작다면(`weight + trucks[0] <= limit`) `bridge`로 트럭을 이동시킨다. 이후 트럭의 무게만큼 `weight`를 더한다. 현재 무게와 다음에 올 트럭의 무게를 더했을 때 `limit`보다 크다면(`weight + trucks[0] > limit`) 트럭은 이동시키지 않고 다리 위에 있는 트럭만 앞으로 이동시킨다. (`bridge`에는 0을 `push`)
3. `trucks`가 더 이상 남아있지 않다면 `weight`의 조건을 따지지 않고 다리 위에 있는 트럭을 한 칸씩 이동시킨다.
4. `bridge`에 아무것도 남아있지 않으면 반복문을 종료한다.

```javascript
function solution(bridge_length, limit, trucks) {
  var answer = 0;
  let bridge = Array.from({ length: bridge_length }, () => 0);
  let weight = 0;

  while (bridge.length !== 0) {
      weight -= bridge.shift();

      if (trucks.length > 0) {
          let out = trucks[0];
          if (weight + out <= limit) {
              bridge.push(trucks.shift());
              weight += out;
          } else bridge.push(0);
      }
      answer++;
  }

  return answer;
}
```

---
## 📍 프로그래머스 2단계 - 주식가격
<a href='https://programmers.co.kr/learn/courses/30/lessons/42584'>프로그래머스 2단계 - 주식가격</a>

### ⚡️ 나의 풀이
문제를 한참 들여다봐도 도대체 무슨 말인가 하는 생각이 여러번 들어서 풀지 말까하는 생각이 들었지만 <a href='https://programmers.co.kr/questions/20326'>이 글</a>에서 다른 분이 지문을 쉽게 풀어 작성해주셔서 이해가 되었다.

문제를 자바스크립트로 풀고 싶었지만 지원 언어에 포함이 되어있지 않기 때문에 별 수 없이 `python`으로 풀었다. `queue`를 이용해서 풀었고 풀이방법은 다음과 같다.



```python
from collections import deque

def solution(prices):
    prices = deque(prices)
    n = len(prices)
    answer = []

    while prices:
        out = prices.popleft()
        time = 0

        for i in prices:
            time += 1
            if i < out:
                break

        answer.append(time)
    return answer

print(solution(prices))
```

---
## 📍 프로그래머스 2단계 - 오픈채팅방
<a href='https://programmers.co.kr/learn/courses/30/lessons/42888'>프로그래머스 2단계 - 오픈채팅방</a>

### ⚡️ 나의 풀이
처음 문제를 풀기 전 문제분류에 `2019 KAKAO BLIND RECRUITMENT` 라고 되어있어서 카카오문제니까 어렵지 않을까?라고 했는데 어렵지 않았다. 문제의 내용은 길었지만 코드는 짧게 작성할 수 있는 문제였다. 결론적으로 반복문을 2번 사용했는데 처음 닉네임이 변경되는 모든 과정에 반복문을 한번 사용하고, 모든 기록이 처리된 마지막에 반복문을 한번 더 사용했다. 세부과정은 다음과 같다.

1. `idInfo`는 `new Map()`으로 선언하여 `hash`값을 이용했다.
2. `status`가 `Enter` 혹은 `Change`일 때 `idInfo`의 `nickName`을 변경한다.
3. 모든 기록이 처리된 후 채팅방 메시지를 출력한다. `status`가 `Enter` 혹은 `Leave`일 때 메시지를 출력하는데, 이때 `2`번과정을 진행한 `userInfo`의 `nickName`을 출력한다.

```javascript
function solution(records) {
    var answer = [];
    let idInfo = new Map();
    
    // Create or Change id if status Enter or Change
    for (let record of records){
        let [status, userId, nickName] = record.split(" ");
        if ((status === "Enter") || (status === "Change")) idInfo.set(userId, nickName);
    }
    
    // Finally Enter or Leave message after processed
    for (let record of records){
        let [status, userId] = record.split(" ");
        if (status === "Enter") answer.push(`${idInfo.get(userId)}님이 들어왔습니다.`);
        else if (status === "Leave") answer.push(`${idInfo.get(userId)}님이 나갔습니다.`);
    }
    
    return answer;
}
```