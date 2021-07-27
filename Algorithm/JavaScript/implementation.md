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