## 📍 01 - 세 수 중 최솟값

3개의 입력 중 가장 작은 수를 구하는 문제다. 먼저, 제일 작은 값을 `a`라고 가정한 다음, `a`와 `b`의 대소관계를 비교하고, `c`와의 대소관계를 비교한 다음 `answer`를 `return` 해줬다.

```javascript
// 나의 코드
console.log(solution(6, 5, 22));

function solution(a, b, c) {
  let answer = a;

  if (answer > b) {
    answer = b;
  } else if (answer > c) {
    answer = c;
  }

  return answer;
}
```

---
## 📍 02 - 삼각형 판별하기

`c`의 길이가 가장 클 때, `a + b > c`를 만족하면 삼각형을 만들 수 있는 조건이 충족된다. 하지만, 입력에서 매번 같은 자리에 `max`길이가 들어오는것이 아니므로, 어떤 위치에서 변수의 길이가 가장 긴지 확인해야한다. 이전에 풀었던 `세 수 중 최솟값` 문제에서 `min`의 값을 추렸다면, 이번엔 반대로 `max`의 값을 찾아야한다. 이후 `max`의 값을 찾았다면, `1번 코드`처럼 각각의 조건을 달아 하드코딩해도 되지만, `2번 코드`처럼 `a + b + c`에서 `max`를 뺀 값이 `max`보다 크면 삼각형이 성립하기 때문에 더욱 간단하게 작성 할 수 있다.

```javascript
// 1번 코드
console.log(solution(6, 7, 11));

function solution(a, b, c) {
  let max = a;
  let sum = a + b + c;

  if (max < b) max = b;
  else if (max < c) max = c;

  if (sum - max > max)


  if (max === a) {
    if (b + c > a) {
      return "YES";
    }
  } else if (max === b) {
    if (a + c > b) {
      return "YES";
    }
  } else {
    if (a + b > c) {
      return "YES";
    }
  }

  return "NO";
}
```

```javascript
// 2번 코드
console.log(solution(6, 7, 11));

function solution(a, b, c) {
  let max = a;
  let sum = a + b + c;

  if (max < b) max = b;
  else if (max < c) max = c;

  if (sum - max > max) return "YES"
  return "NO";
}
```

---
## 📍 03 - 연필개수

1다스는 12자루씩들어가므로 12자리로 나눴을 때 나머지가 있다면 몫에 `+1`을 하는 방법도 있지만, 그보다 간편하게 `Math.ceil` 함수로 몫에 소수점이 있으면 +1 시켜줄 수 있다. `python`에서는 `Math` 라이브러리를 호출해야됐는데 `JS`에서는 `import`없이 사용가능해서 편하다. 처음에는 음수 `floor`를 이용해서 풀었다.

```javascript
console.log(solution(25));

// 음수 floor
function solution(n) {
    return -(Math.floor(-n / 12));
}

// Math.ceil
function solution1(n){
    return Math.ceil(n / 12);
}
```

---
## 📍 04 - 1부터 N까지 합 출력하기

단순하게 값을 누적하는 문제다. `sum` 공식을 사용하거나 `반복문`을 사용했다.

```javascript
console.log(solution(6));

// sum공식
function solution(n) {
  return (n * (n + 1)) / 2;
}

// 반복문
function solution(n) {
  let answer = 0;

  for (let i = 1; i <= n; i++) {
    answer += i;
  }

  return answer;
}
```

---
## 📍 05 - 최솟값 구하기

가장 작은 수를 구하는 문젠데, 배열로 주어졌을 때는 `Math.min` 함수에 단독으로 배열을 넘겨주면 `NaN`값이 반환되므로 `spreadOperator(...)`를 사용해서 `iterable`한 값 중에서 `Math.min`을 구하거나 `apply` 함수를 이용하면 된다. 마지막 반복문을 이용하는 방법은 초기 `min`값을 `JS`에서 안정적으로 높은 값인 `MAX_SAFE_INTEGER`으로 할당하고 그보다 낮은 값을 보면 낮은 값을 할당하는 방법도 있다.

```javascript
console.log(solution([5, 3, 7, 11, 2, 15, 17]));

// apply
function solution(...arr){
    return Math.min.apply(null, arr);
}

// Math.min
function solution(arr){
    console.log(Math.min(...arr));
}

// 반복문
function solution(...arr) {
  let min = Number.MAX_SAFE_INTEGER;

  arr.forEach((element) => {
    if (element < min) {
      min = element;
    }
  });

  return min;
}
```

---
## 📍 05 - 홀수
짝수와 홀수가 섞인 배열에서 홀수를 고를 때는 `filter`를 이용해서 걸렀고, 홀수들 중 최소값은 `Math.min` 함수를 이용했다. 마지막으로 홀수끼리의 합은 `reduce`를 이용했다.

```javascript
solution([12, 77, 38, 41, 53, 92, 85]);

function solution(arr){
    let OddArr = arr.filter((item) => item % 2 !== 0);
    let sumOddArr = OddArr.reduce((acc, cur) => {return acc + cur}, 0);

    console.log(sumOddArr);
    console.log(Math.min(...OddArr));
}
```

---
## 📍 06 - 10부제
배열의 일의 자리 숫자가 `day`와 같은 값이 총 몇개인지 세는 문제인데, `filter`를 이용하면 금방 찾을 수 있다. 여기서 알아두면 좋은 점은 어떤 값을 `10`으로 나눈 나머지는 일의자리 수가 나온다는 점이다.

```javascript
let day = 3;
let cars = [12, 20, 54, 30, 87, 91, 30];

console.log(solution(day, cars));

function solution(day, cars){
    let violateCar = cars.filter((car) => car % 10 === day);
    return violateCar.length;
};
```

---
## 📍 07 - 일곱난쟁이

이 문제는 `python`을 이용해서 <a href='https://www.acmicpc.net/problem/2309'>백준</a>에서 풀어봤던 <a href='https://ywtechit.tistory.com/133'>문제</a>다. `JS`로 한번 풀어봤다.

핵심 로직을 찾는 부분에서 시간이 조금 걸렸는데, 결론적으로 9개 중 2개의 값을 뺐을 때 100이되는 경우의 수를 모두 구하면 되고, `bruteForce`를 이용하면 된다. 또, 지금 생각났지만 처음 풀 때 `python`으로 `slice`를 이용했지만 실패했었다. 왜냐하면 앞 `index`부터 `slice`를 하게되면 전체 배열의 길이가 줄어들기 때문에 `error`가 나기 때문이다. 따라서, 앞보다는 뒤에서부터 `slice`를 이용해서 풀면 된다. (`j` 인덱스는 `i`인덱스보다 항상 +1 많기 때문에 오류가 나지 않는다.)

여담으로 백준 코드를 제출 할 때 자꾸 오답판정을 받았는데 결론적으로 `trim()`을 안해줘서 공백도 같이 포함됐었다. 여러 줄을 입력받을 때는 `trim()`을 꼭 써주자... 😅 😅 이번에는 강의에서 나온 코드 대신 백준 코드를 올렸다.

![](https://images.velog.io/images/abcd8637/post/5a31c795-8658-4a78-b5b4-3247e12ebb09/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-11%2011.16.28.png)

```javascript
const fs = require("fs");
const filePath = process.platform === "linux" ? "/dev/stdin" : "./input.txt";
let input = fs.readFileSync(filePath).toString().trim().split("\n");

input = input.map((item) => +item);

function solution(arr){
  let sum = arr.reduce((acc, cur) => {return acc + cur}, 0);
  arr.sort((a, b) => a - b);

  for (let i = 0; i < 8; i++){
    for (let j = i+1; j < 9; j++){
      if ((sum - (arr[i] + arr[j])) === 100){
        arr.splice(j, 1);
        arr.splice(i, 1);
        return arr;
      }
    }
  }
}

const ans = solution(input);
console.log(ans.join("\n"));
```

---
## 📍 08 - A를 #으로
`A`를 모두 `#`으로 바꾸기만 하면 되는데, 3가지 방법으로 풀었다.

1. `split()` + `map()`
2. `for - of`
3. `replace` + `reg`

마지막에 정규식의 `/A/g`는 대문자 `A`를 모두(`g`) `#`으로 바꿔달라는 의미다.

```javascript
console.log(solution("BANANA"));

// 1. split() + map()
function solution(s){
    s = s.split("").map((item) => item === "A" ? "#" : item)
    return s.join("");
}

// 2. for - of
function solution(s){
    let answer = "";
    for (let i of s){
        if (i === "A") answer += "#"
        else answer += i
    }

    return answer;
}

// 3. replace + reg
function solution(s){
    let answer = s;
    answer = answer.replace(/A/g, "#");

    return answer;
}
```

---
## 📍 09 - 문자 찾기
특정문자를 찾을 때 `for`문을 사용해도 되고 아니면 `split(target)`을 타겟기준으로 나눈 다음 `-1`을 해줘도 된다. 만약 `target`이 제일 마지막에 있으면 어떻게 될까? 마지막에 공백이 추가되기 때문에 마찬가지로 `-1`을 해주면 된다.

```javascript
console.log(solution("COMPUTERPROGRAMMING", "G"));

// for - of
function solution(s, target){
    let cnt = 0;
    for (let i of s){
        if (i === target) cnt += 1
    }
    return cnt;
}

// split
function solution(s, target){
    let answer = s.split(target);
    return answer.length - 1 ;
}
```

---
## 📍 10 - 대문자 찾기
대문자를 찾으려면 `toUpperCase()`로 현재 값이 대문자인지 확인하는 방법이 있고, `ASCII` 코드를 이용해서 찾는 방법이 있다.

```javascript
console.log(solution("KoreaTimeGood"));

// toUpperCase
function solution(s) {
  let cnt = 0;

  for (let i of s) {
    if (i === i.toUpperCase()) cnt += 1;
  }

  return cnt;
}

// ASCII
function solution(s){
    let cnt = 0;

    for (let i of s){
        let num = i.charCodeAt();
        if (num >= 65 && num <=90) cnt++;
    }

  return cnt;
}
```

---
## 📍 11 - 대문자로 통일

앞서 푼 문제와 동일한 방식으로 풀면 된다.

```javascript
console.log(solution("ItisTimeToStudy"));

// ASCII
function solution(s) {
    let ans = "";

    for(let x of s){
        let num = x.charCodeAt();
        if (num>=97 && num<=122) ans+=String.fromCharCode(num-32);
        else ans+=x
    }

    return ans;
}

// toLowerCase, toUpperCase
function solution(s){
    let ans = "";
    for (let string of s){
        if(string === string.toLowerCase()) ans += string.toUpperCase();
        else ans += string;
    }
    return ans;
}
```

---
## 📍 12 - 대소문자 변환
대문자일때 소문자로 소문자일때는 대문자로 변환시키는데 `ASCII` 방법과 `toUpperCase, toLowerCase` 방법으로 나누어 풀었다.

```javascript
console.log(solution("StuDY"));

function solution(s) {
    let ans = "";

    for(let x of s){
        let num = x.charCodeAt();

        if(num>=65 && num<=91) ans+=String.fromCharCode(num+32);
        else ans+=String.fromCharCode(num-32);
    }
  return ans;
}

function solution(s) {
    let ans = "";

    for(let x of s){
        if (x === x.toUpperCase()) ans+=x.toLowerCase();
        else ans += x.toUpperCase();
    }
  return ans;
}
```

---
## 📍 13 - 가장 긴 문자열
가장 긴 문자열을 찾아야하기 때문에 초기값은 제일 작은 값으로 설정해줘야하는데, `Number.MIN_SAFE_INTEGER`로 초기화하면 제일 작은 안전한 값으로 줄 수 있다.(`Number.MIN_SAFE_INTEGER` 값을 콘솔로 찍어보면 `-9007199254740991`가 나온다.) 

```javascript
// 가장 긴 문자열
console.log(solution(5, ["teacher", "time", "student", "beautiful", "good"]));

function solution(n, arr) {
    let ans, max = Number.MIN_SAFE_INTEGER;

    for (str of arr){
        if (str.length > max){
            max = str.length
            ans = str
        }
    }
    return ans;
}
```

---
## 📍 14 - 가운데 문자 출력
<a href='https://programmers.co.kr/learn/courses/30/lessons/12903'>프로그래머스 - 가운데 글자 가져오기</a>와 비슷한 문제이다. 가운데를 정하는 `mid` 변수를 먼저 할당해주고 `slice`를 이용해 구했다.

```javascript
console.log(solution("good"));

// 삼항연산자
function solution(s) {
    let mid = Math.floor(s.length / 2);
    return s.length % 2 == 1 ? s[mid] : s.slice(mid-1, mid+1);
}
```

---
## 📍 15 - 중복 문자 제거 / 중복된 문자 찾기
중복되는 문자를 제거하려면 `set`의 특징인 중복 값 제거를 이용하면 쉽게 풀 수 있다. 강의에서는 `indexOf`를 사용했는데, 처음 배우는 방법이라 신기했다. 현재 `index`와 `indexOf`로 찾은 값이 다르면 중복된 문자, 같으면 처음보는 문자로 판단하는 로직이다. 강의 마지막에 중복된 문자를 찾는 방법도 알려주셨는데 `indexOf`과 `while`을 통해 찾을 수 있었다. 여기서 참고할 점은 `indexOf(searchElement[, fromIndex])`인데, `indexOf`를 사용 할 때 `인자(parameter)`를 하나 더 넘기면 해당 `index`부터 `target`를 찾는다. `while`을 사용해서 `-1`이 나오면 찾는 글자가 없기때문에 `break`하는 방법을 이용했다.

```javascript
// 중복문자제거
console.log(isDuplicate("1234"));

// set
function solution(s) {
    return [...new Set(s)].join('');
}

// indexOf
function solution(s) {
  let answer = "";
  for (let i = 0; i < s.length; i++) {
    if (i === s.indexOf(s[i])) answer += s[i];
  }
  return answer;
}
```

```javascript
// 중복된 문자 찾기
console.log(solution("algorithmic", "i"));

function solution(s, target) {
  let cnt = 0;
  let duplicatedIndex = s.indexOf(target);

  while (duplicatedIndex !== -1) {
    cnt++;
    duplicatedIndex = s.indexOf(target, duplicatedIndex + 1);
  }

  return cnt;
}
```

---
## 📍 16 - 중복 단어 제거

<a href='https://ywtechit.tistory.com/249'>중복 문자 제거</a>와 같은 로직으로 풀었는데 이번엔 배열 안에 문자가 들어가있는 문제다. `set`, `indexOf`, `indexOf + filter`를 사용했다.

```javascript
solution(5, ["good", "time", "good", "time", "student"]);

// set
function solution(s) {
  return [...new Set(s)].join("\n");
}

// indexOf
function solution(n, words) {
    for (let i = 0; i < n; i++){
        if(words.indexOf(words[i]) === i){
            console.log(words[i])
        }
    }
}

// filter + indexOf
function solution(n, words) {
  let ans = words.filter((item, idx) => words.indexOf(item) === idx);
  console.log(ans.join("\n"));
}
```

---
## 📍 17 - 큰 수 출력하기
자신의 바로 앞의 값만 비교한다는 점을 고려해서 `reduce` 함수를 사용했다. `reduce`함수의 인자로 넘겨줄 `acc, cur`에서 `acc`를 이전단계의 `cur`로 `return`해주면 바로 이전 `index`와 비교하게 된다. 맨 처음에는 `0`을 넘겨주자.

`for`문으로 풀 때는 그다지 어렵지 않았는데, 맨 앞의 값을 비교할때는 이전 값이 없기때문에 `0`을 추가해줬다. (혹은 `Number.MIN_SAFE_INTEGER`을 할당해줘도 된다.)

```javascript
console.log(solution([7, 3, 9, 5, 6, 12]));

// reduce
function solution(arr) {
  let answer = [];
  arr.reduce((acc, cur) => {
    if (cur > acc) {
      answer.push(cur);
    }
    return cur;
  }, 0);

  return answer.join(' ');
}

// for
function solution(arr){
    let answer = [];
    arr = [0, ...arr];

    for (let i=1; i < arr.length; i++){
        if (arr[i] > arr[i-1]){
            answer.push(arr[i])
        }
    }
    return answer.join(' ');
}

// for2
function solution(arr){
    let answer = [];
    answer.push(arr[0]);

    for (let i=1; i < arr.length; i++){
        if (arr[i] > arr[i-1]){
            answer.push(arr[i])
        }
    }
    return answer.join(' ');
}
```

---
## 📍 18 - 보이는 학생
이 문제를 보자마자 <a href='https://www.acmicpc.net/problem/2493'>boj2493 - 탑</a>과 유사하다는 생각이 들었다. (비록 <a href='https://ywtechit.tistory.com/204'>python</a>으로 풀긴했지만..) `보이는 학생` 문제는 그다지 어렵지 않았다. 대신 주의할 점은 이전 `index`의 값을 알고있어야 대소관계를 알 수 있는데, 제일 첫번째 학생은 비교 대상이 없기 때문에 `stack`에 넣고 시작하면 된다. 강의영상에서는 값을 누적하는 대신 할당하는것으로 풀었는데, 굳이 빈 배열에 `push` 하지 않고도 값을 갱신하는것이 불필요한 `push`가 없어서 괜찮았다.

```javascript
console.log(solution([130, 135, 148, 140, 145, 150, 150, 153]));

// 나의 코드
function solution(students) {
  let stack = [];
  let cnt = 1;

  stack.push(students[0]);

  for (let i = 1; i < students.length; i++) {
    if (students[i] > stack[stack.length - 1]) {
      stack.push(students[i]);
      cnt += 1;
    }
  }
  return cnt;
}

// 강의
function solution(students) {
  let maxHeight = students[0];
  let cnt = 1;

  for (let i = 1; i < students.length; i++) {
    if (students[i] > maxHeight) {
      maxHeight = students[i];
      cnt += 1;
    }
  }
  return cnt;
}
```