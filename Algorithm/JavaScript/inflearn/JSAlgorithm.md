## 📍 section04 - 1 - 세 수 중 최솟값

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

---
## 📍 19 - 가위 바위 보
경우의수를 잘 따져서 풀어야하는데, `if`문에 `A`가 이긴경우, `else - if`문에 비긴경우, `else`문(`B`가 이긴경우)순서로 작성하면 코드의 양을 줄일 수 있다. 두번째 코드는 `if - else if - else`를 삼항연산자로 압축해서 작성했다.

```javascript
let n = 5;
let a = [2, 3, 3, 1, 3];
let b = [1, 1, 2, 2, 3];

console.log(solution(n, a, b));

// &&
function solution(n, a, b) {
  let scissor = 1, rock = 2, paper = 3;
  let ans = "";

  for (i = 0; i < n; i++) {
    if (
      (a[i] === scissor && b[i] === paper) ||
      (a[i] === rock && b[i] === scissor) ||
      (a[i] === paper && b[i] === rock)
    ) {
      ans += "A ";
    } else if (a[i] === b[i]) {
      ans += "D ";
    } else {
      ans += "B ";
    }
  }
  return ans;
}
```

```javascript
// 삼항연산자
function solution(n, a, b) {
  let scissor = 1,
    rock = 2;
  paper = 3;
  let ans = "";

  for (i = 0; i < n; i++) {
    a[i] === b[i]
      ? (ans += "D ")
      : a[i] === scissor && b[i] === paper
      ? (ans += "A ")
      : a[i] === rock && b[i] === scissor
      ? (ans += "A ")
      : a[i] === paper && b[i] === rock
      ? (ans += "A ")
      : (ans += "B ");
  }
  return ans;
}
```

```javascript
// 모든 경우의 수를 나열한 코드
function solution(n, a, b) {
  let scissor = 1, rock = 2
  let ans = "";

  for (i = 0; i < n; i++) {
    if (a[i] === scissor) {
      if (b[i] === scissor) {
        ans += "D";
      } else if (b[i] === rock) {
        ans += "B";
      } else {
        ans += "A";
      }
    } else if (a[i] === rock) {
      if (b[i] === scissor) {
        ans += "A";
      } else if (b[i] === rock) {
        ans += "D";
      } else {
        ans += "B";
      }
    } else {
      if (b[i] === scissor) {
        ans += "B";
      } else if (b[i] === rock) {
        ans += "A";
      } else {
        ans += "D";
      }
    }
  }
  return ans;
}
```

---
## 📍 20 - 점수 계산
문제의 양은 길지만 조금만 생각하면 금방 풀 수 있다. 여기서 중요한 점은 `가산점`처리인데, 연속으로 맞은 경우에만 `+1`씩 증가하게 작성해야한다.

```javascript
let n = 10;
let scores = [1, 0, 1, 1, 1, 0, 0, 1, 1, 0];
console.log(solution(n, scores));

// 삼항연산자
function solution(n, scores) {
  let extraPoint = 0;
  let cnt = 0;

  for (let score of scores) {
    score === 1 ? (extraPoint++, (cnt += extraPoint)) : (extraPoint = 0);
  }

  return cnt;
}

// if - else
function solution(n, scores) {
  let extraPoint = 0;
  let cnt = 0;

  for (let score of scores) {
    if (score === 1) {
      extraPoint++;
      cnt += extraPoint;
    } else extraPoint = 0;
  }

  return cnt;
}
```

---
## 📍 21 - 등수 구하기
이 문제는<a href='https://www.acmicpc.net/problem/7568'>boj7568 - 덩치</a>와 비슷한 문제다. 등수 구하기 문제가 쉽다면 덩치 문제를 풀어보자. 모든 경우의 수를 찾는 `bruteForce` 방법으로 풀면 되는데, 모든 값을 `1`로 빈 배열을 초기화 시킬 때 `Array.from`을 이용했다. 

```javascript
let n = 5;
let scores = [100, 88, 76, 88, 76];

console.log(solution(n, scores));

function solution(n, scores) {
  let answers = Array.from({ length: n }, () => 1);

  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      if (scores[j] > scores[i]) {
        answers[i]++;
      }
    }
  }
  return answers;
}
```

---
## 📍 22 - 격자판 최대합
`n*n`의 격자판에서 각 행, 각 열, 두 대각선의 합 중 가장 큰 값을 출력하면 되는데, 첫번째로 `row`의 합을 구할때는 반복문을 하나만 선언해서 `reduce`를 이용했고, `column`의 합은 중첩반복문을 선언해서 `i, j`값을 구했다. 대각선은 좌측상단에서 우측하단의 방향의 대각선 `arr[i][i]`과 우측상단에서 좌측하단의 방향의 대각선 `arr[i][n-i-1]`의 방법을 이용해서 구했다.

```javascript
let n = 5;
let arr = [
  [10, 13, 10, 12, 15],
  [12, 39, 30, 23, 11],
  [11, 25, 50, 53, 15],
  [19, 27, 29, 37, 27],
  [19, 13, 30, 13, 19],
];

console.log(solution(n, arr));

// 가로, 세로, 대각선 로직을 각각 작성한 코드
function solution(n, arr) {
  let row = (column = normal = reverse = 0);

  // row
  for (let i = 0; i < n; i++) {
    let rowSum = arr[i].reduce((acc, cur) => acc + cur, 0);
    row = Math.max(row, rowSum);
  }

  // column
  for (let i = 0; i < n; i++) {
    let columnSum = 0;
    for (let j = 0; j < n; j++) {
      columnSum += arr[j][i];
    }
    column = Math.max(column, columnSum);
  }

  // diagonal
  for (let i = 0; i < n; i++) {
    normal += arr[i][i];
    reverse += arr[i][n-i-1];
  }

  return Math.max(row, column, normal, reverse);
}

// 가로 + 세로, 대각선 로직을 작성한 코드
function solution(n, arr) {
  let answer = 0;
  let normal = reverse = 0;

  // row, column
  for (let i = 0; i < n; i++) {
    let row = column = 0;
    for (let j = 0; j < n; j++) {
      row += arr[i][j];
      column += arr[j][i];
    }
    answer = Math.max(row, column);
  }

  // diagonal
  for (let i = 0; i < n; i++) {
    normal += arr[i][i];
    reverse += arr[i][n-i-1];
  }

  answer = Math.max(answer, normal, reverse);
  return answer;
}
```

---
## 📍 23 - 봉우리
자신의 상하좌우 숫자보다 큰 숫자의 개수를 찾으면 되는데, 상하좌우를 판별할때는 `dx, dy`와 같이 방향 벡터를 설정해주면 확인하기 편하다. 

나는 이렇게 풀었다.
1. 상, 하, 좌, 우의 좌표를 하나씩 탐색하고 최대값을 갱신한다.
2. `max`로 갱신된 주변 좌표와 원래 나의 좌표와 비교한다음 원래 나의 좌표가 더 크면 `cnt++` 해준다.

강사님은 이렇게 푸셨다.
1. `flag`를 설정한다.
2. 원래 나의 좌표보다 주변좌표가 크면 `flag`를 0으로 바꾼다.
3. 주변 좌표의 탐색이 끝났는데도 `flag`가 1이면 원래 나의 좌표가 큰것이므로 `cnt++` 해준다.


```javascript
let n = 5;
let arr = [[5, 3, 7, 2, 3], [3, 7, 1, 6, 1], [7, 2, 5, 3, 4], [4, 3, 6, 4, 1], [8, 7, 3, 5, 2]];

console.log(solution(n, arr));

// 나의 코드
function solution(n, arr){
    let cnt = 0;
    let dx = [-1, 0, 1, 0], dy = [0, 1, 0, -1];

    for (let x=0; x<n; x++){
        for(let y=0; y<n; y++){
            let surround = 0;
            for (let i=0; i<4; i++){
                let nx = x + dx[i];
                let ny = y + dy[i];

                if (nx<0 || ny<0 || nx>=n || ny>=n) continue
                if (surround < arr[nx][ny]) surround = arr[nx][ny]
            }
            if (arr[x][y] > surround) cnt++;
        }
    }
    return cnt;
}
```

```javascript
let n = 5;
let arr = [[5, 3, 7, 2, 3], [3, 7, 1, 6, 1], [7, 2, 5, 3, 4], [4, 3, 6, 4, 1], [8, 7, 3, 5, 2]];

console.log(solution(n, arr));

// 강의 코드
function solution(n, arr){
    let cnt = 0;
    let dx = [-1, 0, 1, 0], dy = [0, 1, 0, -1];

    for (let x=0; x<n; x++){
        for(let y=0; y<n; y++){
            let flag = 1;
            for (let i=0; i<4; i++){
                let nx = x + dx[i];
                let ny = y + dy[i];

                if (nx<0 || ny<0 || nx>=n || ny>=n) continue
                if (arr[nx][ny] > arr[x][y]){
                    flag = 0;
                    break;
                }
            }
            if (flag) cnt ++;
        }
    }
    return cnt;
}
```

---
## 📍 24 - 회문 문자열
주어진 문자열이 회문인지 판별하는 문제다. <a href='https://ywtechit.tistory.com/34'>이전</a>에 파이썬 알고리즘 인터뷰에서 한번 풀어본적이 있다.

```javascript
console.log(solution("gooog"));

// split + reverse + join
function solution(str){
    if (str.split('').reverse().join('') !== str) return false;
    return true
}
```

```javascript
console.log(solution("gooog"));

// for
function solution(str){
    str = str.toLowerCase();
    let n = str.length
    
    for (let i=0; i<Math.floor(n/2); i++){
        if (str[i] !== str[n-i-1]) return false
    }
    return true
}
```

```javascript
console.log(solution("gooog"));

// slice
function solution(str){
    str = str.toLowerCase();

    while (str.length > 1){
        if (str.slice(0, 1) === str.slice(-1)) str = str.slice(1, -1);
        else return false;
        console.log(str)
    }
    return true;
}
```

```javascript
console.log(solution("gooog"));

// recursive
function firstCharacter(str){
    return str.slice(0, 1);
}

function midCharacter(str){
    console.log(str.slice(1, -1), str)
    return str.slice(1, -1);
}

function lastCharacter(str){
    return str.slice(-1);
}

function isPalindrome(str){
    if (firstCharacter(str) !== lastCharacter(str)) return false;
    if (midCharacter(str).length <= 1) return true;

    return isPalindrome(midCharacter(str))
}
```

---
## 📍 25 - 유효한 팰린드롬
주어진 문자열이 회문인지 판별하는 문제인데, 추가로 알파벳이외의 문자들은 무시한다. 마찬가지로 <a href='https://ywtechit.tistory.com/34'>이전</a>에 파이썬 알고리즘 인터뷰에서 한번 풀어본적이 있다. 알파벳이외의 값을 제거하는 방법으로 `정규표현식(Reg)`을 이용했다.

```javascript
let s = "found7, time: study; Yduts; emit, 7Dnuof";
console.log(solution(s));

function solution(s){
    s = s.toLowerCase();
    let notIncludeSpecialCharacter = s.replace(/[^a-z]/g, '');
    let compareStr = notIncludeSpecialCharacter.split('').reverse().join('');
    
    if (notIncludeSpecialCharacter === compareStr) return true;
    return false;
}
```

---
## 📍 26 - 숫자만 추출
`문자 + 숫자`가 섞여있는 문자열에서 숫자만 추출하는 문제다. 숫자판별은 `isNaN` 함수를 사용해서 숫자인지 확인하거나, `정규표현식(Reg)`으로 숫자인지 확인하는 방법을 사용했다.

```javascript
let s = "g0en2T0s8eSoft";
// let s = "tge0a1h205er"
// let s = "12a3E4hg5n6vc7x"
console.log(solution(s));

// isNaN
function solution(s) {
  let ans = 0;
  for (let i of s) {
    if (!isNaN(i)) ans = ans * 10 + (+i);
  }
  return +ans;
}

//isNaN
function solution(s) {
  let ans = "";
  for (let i of s) {
    if (!isNaN(i)) ans += i;
  }
  return +ans;
}

//replace + Reg
function solution(s){
    let result = s.replace(/[^0-9]/g, '');
    return +result;
}

//match + Reg
function solution(s){
    let result = s.match(/[0-9]/g).join('');
    return +result
}
```

---
## 📍 27 - 가장 짧은 문자거리
`target`이 문자열 `s`에서 떨어진 최소거리를 출력하는 문제다. 여기서 고려해야하는 점이 있는데, 처음에 `cnt = 0`으로 초기화하고나서 강의를 들어보니까 맨 좌측을 기준으로 판단할때는 맨 좌측에 `target`이 없으므로 `cnt`를 제일 큰 숫자로 초기화해야한다는 것이다. 그렇게해야 `reverse`로 검사할때도 올바른 답을 도출해낼 수 있다. 잘 이해가 되지 않는다면 `테스트 케이스` 입력: `tteachermodett` 출력: `2 1 0 1 2 1 0 1 2 2 1 0 1 2`와 같이 나오는지 확인해보자.

```javascript
let s = "teachermode";
let target = "e";

console.log(solution(s, target));

// 나의코드
function solution(s, target) {
  let n = s.length;
  let cnt = 1000;
  let answer = [];

  for (let i = 0; i < n; i++) {
    if (s[i] === target) cnt = 0;
    else cnt++;

    answer.push(cnt);
    console.log(answer);
  }

  cnt = 1000;

  for (let i = 0; i < n; i++) {
    if (s[n - i - 1] === target) cnt = 0;
    else cnt++;

    answer[n - i - 1] = Math.min(answer[n - i - 1], cnt);
  }

  return answer.join(" ");
}
```

---
## 📍 28 - 문자열 압축
`if-else`문을 이용해서 구현했다.

```javascript
let s = "KKHSSSSSSSE";

console.log(solution(s));

// 나의코드
function solution(s) {
  let cnt = 1;
  let answer = "";

  for (let x of s) {
    if (x === answer[answer.length - 1]) cnt++;
    else {
      if (cnt >= 2) answer += cnt;
      answer += x;
      cnt = 1;
    }
  }
  return answer;
}

// 강사님 코드
function solution(s) {
  let cnt = 1;
  let answer = "";
  s += " ";

  for (let i=0; i<s.length-1; i++) {
    if (s[i] === s[i+1]) cnt++;
    else{
        answer += s[i];
        if(cnt>1) answer+=cnt
        cnt = 1
    }
}
  return answer;
}
```

---
## 📍 section04 - 1 - 자릿수의 합
자릿수의 합을 구하고 그 합이 최대인것까지는 잘 구할 수 있었는데, 자릿수의 합이 같을 때 원래 숫자를 비교하여 더 큰 숫자를 리턴하는 방법이 명확하게 떠오르지 않았다. 어렵게 생각 할 필요 없이 처음 자릿수의 합을 비교할 때 자릿수의 합만 저장하는것이 아니라 변수를 따로 만들어서 원래 숫자까지 저장하는 방법을 쓰면 된다. 이후에 자릿수의 합이 동일한 값이 나오면 원래 숫자와 비교해서 더 큰 값으로 갱신해주면 된다.

```javascript
let n = 7;
let arr = [133, 532, 701, 1001, 145];

console.log(solution(n, arr));

// 나의 코드
function solution(n, arr) {
  let max = Number.MIN_SAFE_INTEGER;
  let answer;

  for (let x of arr) {
    let sum = 0;
    let temp = x;

    do {
      sum += temp % 10;
      temp = Math.floor(temp / 10);
    } while (temp !== 0);

    if (max < sum){
        max = sum;
        answer = x;
    }
    else if (max === sum) {
        if (answer < x) answer = x;
    }
  }

  return answer;
}
```

```javascript
let n = 7;
let arr = [133, 532, 701, 1001, 145];

// 강사님 코드
function solution(n, arr) {
  let answer;
  let max = 0;

  for (let x of arr) {
    let temp = x;
    let sum = 0;

    while (temp) {
      sum += temp % 10;
      temp = Math.floor(temp / 10);
    }

    if (sum > max) {
      max = sum;
      ans = x;
    } else if (sum === max) {
      if (x > ans) ans = x;
    }
  }

  return answer;
}
```

---
## 📍 section04 - 2 - 뒤집은 소수
자연수를 뒤집을 때 `string`형을 사용하는 대신 `number`형 그대로 뒤집는 방법을 알면 좋을것 같다. 그리고 소수를 판별 할 때는 반복문의 범위를 `i<=Math.floor(n**0.5)`까지만 설정해주면 더 적은 시간에 소수를 판별 할 수 있다. 코드의 가독성을 높이기 위해 자연수를 뒤집는 로직과 소수를 판별하는 로직을 나눠서 하는 편도 좋다. 소수 판별 문제는 <a href='https://ywtechit.tistory.com/13'>이전</a>에도 종종 풀었다.

```javascript
// 나의 코드
let n = 9;
let arr = [32, 55, 62, 20, 250, 370, 200, 30, 100];

console.log(solution(n, arr));

function solution(n, arr) {
  let answer = "";

  for (let number of arr) {
    let sum = 0;
    let flag = true;

    do {
      sum = sum * 10 + number % 10;
      number = Math.floor(number / 10);
    } while (number > 1);

    if (sum > 1) {
      for (let i = 2; i <= Math.floor(sum ** 0.5); i++) {
        if (sum % i === 0) {
          flag = false;
          break;
        }
      }
      if (flag) answer += `${sum} `;
    }
  }
  return answer.slice(0, -1);
}
```

```javascript
// 강사님 코드
let n = 9;
let arr = [32, 55, 62, 20, 250, 370, 200, 30, 100];

console.log(solution(n, arr));

function isPrime(n) {
  if (n < 2) return false;

  for (let i = 2; i <= Math.floor(n ** 0.5); i++) {
    if (n % i === 0) return false;
  }
  return true;
}

function solution(n, arr) {
  let ans = "";

  for (let number of arr) {
    let sum = 0;
    do {
      sum = sum * 10 + (number % 10);
      number = Math.floor(number / 10);
    } while (number > 1);

    if (isPrime(sum)) ans += `${sum} `;
  }
  
  return ans.slice(0, -1);
}
```

---
## 📍 section04 - 3 - 멘토링
조금 어려운 문제였다. `bruteForce`로 풀어야하는것은 알고있었지만, 어떤 흐름으로 문제를 풀어야할지 고민이 많았다. 강의를 봤는데도 이해가 잘 안돼서 복습을 여러번했다.

결과적으로 이 문제의 핵심은 `n`명의 학생이 각각의 경우에 `m`번의 수학성적 모두 `mento`와 `mentee`가 될 수 있는 조건이 맞는지 찾아야 하고, 그 안에서 수학등수를 나타내는 `idx`를 고려해서 `mentoIdx < menteeIdx`인 조건을 찾을 수 있는지 물어보는 문제인것 같다. 또, `mento`와 `mentee`는 같은 학생일때는 성립하지 않음을 알아야한다.

강의에서 4중반복문으로 풀었는데, 반복문의 개수가 많다보니까 헷갈려서 수학성적이 `m`개가 아닌 딱 1개만 주어졌을때를 가정하고 풀어봤다. 다음의 사진처럼 경우의 수를 모두 구해보고 코드를 작성하니까 조금 이해가 됐다.

![](https://images.velog.io/images/abcd8637/post/6344fd46-0881-4884-9f27-774c7664eb3b/KakaoTalk_Photo_2021-08-21-09-43-51.jpeg)

```javascript
let arr = [3, 4, 1, 2];
let n = 4;
let m = 1;
let cnt = 0;

for (let x = 1; x <= n; x++) {
  for (let y = 1; y <= n; y++) {
    let mentoIdx = menteeIdx = 0;
    for (let i = 0; i < n; i++) {
      if (x === y) continue;
      if (arr[i] === x) mentoIdx = i;
      if (arr[i] === y) menteeIdx = i;
    }
    if (mentoIdx < menteeIdx) {
        cnt++; 
        console.log(x, y);
    }
  }
}
console.log(cnt);
👉🏽 
1 2
3 1
3 2
3 4
4 1
4 2

6
```

수학성적에 2차원 배열이 들어갔을 때도 위에서 작성한 코드에서 크게 벗어나지 않는다. 다만, `mento`, `mentee`의 관계가 성립하려면 모든 수학성적에서 `mento`가 더 앞서야하므로 `cnt`가 `m`과 동일하다는 조건을 걸어줘야한다. 전체 코드는 다음과 같다.

```javascript
let arr = [[3, 4, 1, 2], [4, 3, 2, 1], [3, 1, 4, 2]];
let n = 4;
let m = 3;

console.log(solution(n, m, arr));

function solution(n, m, arr){
    let ans = 0;
    for (let x=1; x<=n; x++){
        for (let y=1; y<=n; y++){
            let cnt = 0;
            for (let i=0; i<m; i++){
                let mento = mentee = 0;
                for (let j=0; j<n; j++){
                    if (x===y) continue;
                    if (arr[i][j] === x) mento = j;
                    if (arr[i][j] === y) mentee = j;  
                }
                if (mento < mentee) cnt++;
            }
            if (cnt === m) ans++;
        }
    }
    return ans;
}
```

---
## 📍 section04 - 4 - 졸업선물
상품을 최대한 많이 사야하는 문제는 비용이 적게드는 상품부터 포함하면 최대한 많이 살 수 있다는 점을 알고 이 문제를 풀자. 그리고 최대 몇 명의 학생들에게 사줄 수 있는지 보려면 경우의 수를 하나씩 따져가며 검사를 다 해야하기 때문에 `bruteForce`를 이용하자. 이중 반복문을 돌면서 맨 처음 상품은 50% 할인 쿠폰을 사용하고 나머지 상품을 구매 할 때는 그냥 더해주면 된다. 동일한 학생이 없으므로 `i !== j`인 조건을 추가하는 것도 잊지 말자.

```javascript
// 나의 코드
let n = 5;
let m = 28;
let cost = [[6, 6], [2, 2], [4, 3], [4, 5], [10, 3]];

console.log(solution(n, m, cost));

function solution(n, m, cost) {
  let max = Number.MIN_SAFE_INTEGER;

  cost.sort((a, b) => a[0] + a[1] - (b[0] + b[1]));

  for (let i = 0; i < n; i++) {
    let budget = m - (cost[i][0] / 2 + cost[i][1]);
    let cnt = 1;

    for (let j = 0; j < n; j++) {
      if (i === j) continue;
      if (budget - (cost[j][0] + cost[j][1]) >= 0) {
        budget -= cost[j][0] + cost[j][1];
        cnt++;
      } else {
        break;
      }
    }
    max = Math.max(max, cnt);
  }
  return max;
}

```

```javascript
// 강사님 코드
let n = 5;
let budget = 28;

let arr = [[6, 6], [2, 2], [4, 3], [4, 5], [10, 3]];

console.log(solution(n, budget, arr))

function solution(n, budget, arr){
    let ans = Number.MIN_SAFE_INTEGER;
    arr.sort((a, b) => a[0] + a[1] - (b[0] + b[1]));

    for (let i=0; i<n; i++){
        let cnt = 1;
        let changeBudget = budget - (arr[i][0]/2 + arr[i][1]);
        for (let j=0; j<n; j++){
            if (i === j) continue;

            if (arr[j][0] + arr[j][1] <= changeBudget){
                changeBudget -= arr[j][0] + arr[j][1];
                cnt++
                console.log(arr[j][0] + arr[j][1], changeBudget, cnt)
            }else break;
        }
        ans = Math.max(ans, cnt);
    }
}
```

---
## 📍 section04 - 5 - K번째 큰 수
100장의 카드 중 3장을 뽑는 모든 경우의 수는 `100C3`이므로 `161,700`이다. 여기서 3장을 뽑아 각 카드의 적힌수를 합하려면 3중반복문으로 `bruteForce`로 모든 경우의 수를 돌려보면 된다. 여기서 시간복잡도는 다항시간인 `O(N^3)`이지만 `N=100`일때 최대 `1,000,000`번 수행하므로 시간초과에 걸리지 않는다. (보통 반복문을 돌 때 1초당 최대 `10^8` (약 1억번) 돌 수 있으므로, `N=100`일때는 `O(N^4)`까지는 커버가능하다.) 또, 강의에서는 3중 반복문의 `i, j, k`의 범위를 모두 `n`까지로 설정했는데, 맨 마지막에서 `k`가 `n`을 벗어나면 반복문에 들지 않고, 마찬가지로 `j`가 `n`의 범위를 벗어나도 반복문에 들지 않기 때문에 자동적으로 종료된다고 말씀하셨다. 나는 조금이라도 불 필요한 연산을 줄이기 위해 반복문의 범위를 `n-2`, `n-1`, `n`까지로 설정했다.

```javascript
// 나의 코드
let arr = [13, 15, 34, 23, 45, 65, 33, 11, 26, 42];
let target = 3;
let n = 10;

console.log(solution(n, target, arr))

function solution(n, target, arr){
    let answer = [...new Set([])];

    for (let i=0; i<n-2; i++){
        for (let j=i+1; j<n-1; j++){
            for (let k=j+1; k<n; k++){
                answer.push(arr[i] + arr[j] + arr[k]);
            }
        }
    }
    answer = answer.sort((a, b) => b - a);
    return answer[target-1];
}
```

```javascript
// 강사님 코드
let arr = [13, 15, 34, 23, 45, 65, 33, 11, 26, 42];
let target = 3;
let n = 10;

console.log(solution(n, target, arr))

function solution(n, k, arr) {
    let ans = new Set();
    
    for (let i = 0; i < n - 2; i++) {
      for (let j = i + 1; j < n - 1; j++) {
        for (let k = j + 1; k < n; k++) {
          ans.add(arr[i] + arr[j] + arr[k]);
        }
      }
    }
    ans = Array.from(ans).sort((a, b) => b - a);
    return ans[k - 1];
  }
```

---
## 📍 section05 - 1 - 두 배열 합치기
오름차순으로 정렬된 배열을 합치는 문제인데, 저번에 병합정렬(mergeSort) 연습하다가 이 문제와 비슷한 로직인것 같아서 그대로 적용했다. 강사님 코드는 나의코드와 조금 비슷하면서 달랐다. 또, 문제에서 `n`의 범위가 `100`까지기 때문에 시간복잡도를 `다항시간(O(N^2) 이상)`내로 풀어도 되지만, 범위가 큰 경우를 대비해서 `TwoPointer`를 사용하여 `O(N)`으로 풀었다. 똑같이 풀 수 있는데 왜 `twoPointer`를 선택했냐고 묻는다면 만약, 실무에서 `O(N^2)` 코드와 `O(N)`코드가 있을 때 `O(N)`코드를 선택 할 것임은 자명하다. 

강사님은 `후치연산자(postfix form)`를 사용하셨는데, 후치연산자의 특징은 연산자가 변수 뒤에 올때 값을 먼저 계산하고 `증가/감소`가 이루어지는 형태다. 코드를 간략하게 쓸 때 좋은것 같다. 또 `while`문의 조건을 `&&`로 해줘야 둘 중 하나가 `false` 일 때 전체 반복문이 `false`가 되는것도 잊지말자.

```javascript
// 나의코드
let n = 4;
let arr1 = [1, 10, 20, 50];
let m = 5;
let arr2 = [3, 6, 10, 20, 25];

console.log(solution(n, arr1, m, arr2));

function solution(n, nArr, m, mArr) {
  let p1 = p2 = 0;
  let answer = [];

  while (n<p1 && m<p2) {
    if (nArr[p1] < mArr[p1]) {
      answer.push(nArr[p1]);
      p1++;
    } else {
      answer.push(mArr[p2]);
      p2++;
    }
  }

  return answer.concat(nArr.slice(p1), mArr.slice(p2));
}
```

```javascript
// 강사님 코드
let n = 4;
let arr1 = [1, 10, 20, 50];
let m = 5;
let arr2 = [3, 6, 10, 20, 25];

console.log(solution(n, arr1, m, arr2));

function solution(n, arr1, m, arr2){
	let p1 = p2 = 0;
	let answer = [];

	while (p1<n && p2<m){
		if (arr1[p1] < arr2[p2]) answer.push(arr1[p1++]);
		else answer.push(arr2[p2++]);
	}

	while (p1<n) answer.push(arr1[p1++]);
	while (p2<m) answer.push(arr2[p2++]);

	return answer;
}
```

---
## 📍 section05 - 2 - 공통 원소 구하기
`A, B` 두 개의 집합이 주어질 때 공통 원소를 추출하여 오름차순으로 출력하는 문제다. 투 포인터를 사용해야하는 이유는 `N`의 크기가 `30,000`인데, 이를 `O(N^2)`으로 풀게 되면 최악의 경우 1초당 `9억`번의 연산을 해야하기때문에 시간초과가 난다. 따라서, `O(N^2)`보다 작은 시간복잡도로 계산해야 한다. 만약, `N`의 범위가 `30,000`보다 더 작다면 `O(N^2)`으로 `bruteForce`로도 풀 수 있다.`bruteForce`의 장점은 모든 경우의 수를 검사하기 때문에 정확한 결과값이 나온다는 점이다.

```javascript
//O(N^2), bruteForce
let n = 5;
let arr1 = [1, 3, 9, 5, 2];

let m = 5;
let arr2 = [3, 2, 5, 7, 8];

console.log(solution(n, arr1, m, arr2));

function solution(n, arr1, m, arr2) {
  let ans = [];

  for (let i = 0; i < n; i++) {
    let target = arr1[i];
    for (let j = 0; j < m; j++) {
      if (target === arr2[j]) ans.push(target);
    }
  }

  ans.sort((a, b) => a - b);
  return ans;
}
```

하지만, 이번 섹션이 `효율성`을 고려하는 문제인만큼 투 포인터로 풀어보자. 투 포인터를 사용하면 `NlogN+N+M` 즉, `O(NlogN)`에 풀 수 있는데, 시간 내에 들어 올 수 있다. 풀이방법은 다음과 같다.

1. 두 배열을 각각 `sort(nlogn)`한다.
2. 투 포인터 인덱스를 가리키는 `p1`, `p2`를 0으로 선언한다.
3. 만약, `p2`가 가르키는 값이 `p1`보다 크면 현재 `p2` 뒤로는 `p1`보다 같거나 작은값이 없다. 왜냐하면 배열은 이미 오름차순으로 정렬되어있기 때문이다. 따라서 `p1++`을 해준다.
4. `p1===p2`이면 `ans`에 넣고 다음 숫자를 검사하기 위해 `p1++`, `p2++` 해준다.
5. `p1>p2`인 상황이면 `p2++`를 해준다.
6. `p1` 혹은 `p2`가 `n`보다 커지면 반복문을 종료한다.(한쪽 탐색이 먼저 끝나면 다른쪽은 탐색 할 필요가 없기 때문이다.)

```javascript
// O(NlogN + N + M), Two Pointer
let n = 5;
let arr1 = [1, 3, 9, 5, 2];

let m = 5;
let arr2 = [3, 2, 5, 7, 8];

console.log(solution(n, arr1, m, arr2));

function solution(n, arr1, m, arr2) {
  let ans = [];
  let p1 = (p2 = 0);
  arr1.sort((a, b) => a - b);
  arr2.sort((a, b) => a - b);

  while (p1 < n && p2 < m) {
    if (arr1[p1] === arr2[p2]) {
      ans.push(arr1[p1++]);
      p2++;
    } else if (arr1[p1] < arr2[p2]) p1++;
    else p2++;
  }

  return ans;
}
```

---
## 📍 section05 - 3 - 연속 부분수열1
`N`개의 수가 있을 때, 연속부분수열의 합이 `target`과 동일한 경우가 몇 번있는지 찾는 문제다. 이전까지는 이와 비슷한 유형의 문제를 풀어본 경험이 없기 때문에 어려웠다. `N<=100,000` 일 때 최대 `O(nlogn)`의 시간복잡도를 만족해야 시간초과를 받지 않는다. 즉, `bruteForce(O(N^2))` 대신 다른 방법을 사용해야 한다. 

코드에서는 `while + while`문을 사용했는데, 반복문을 2개 사용하면 무조건 `O(N^2))`이 되는게 아닌가요?라고 할 수도 있다. 결론적으로는 그렇지 않다. 이중 반복문을 사용하더라도 그 안에서 어떤 연산을 했느냐에 따라 다른데, 현재 코드에서는 안쪽 루프가 도는 총 횟수를 다 합했을 때 꼭 `O(N)`이 되지 않는다. 왜냐하면 안쪽 루프의 조건을 보면 `sum>=m` 인데, 만약, 현재 조건이 `sum<m`이라면 안쪽 루프는 실행되지 않을 것이기 때문이다. 
 
1. 투 포인터 변수인 `lt=rt=0`으로 초기화한다.
2. `sum` 변수에 `arr[rt]` 값을 더한다.
3. `sum === target` 이면, `cnt++`해준다.
4. 만약, `sum>target`이면, `lt`를 증가해서 `sum<=target`이 될 때까지 빼줘야 한다.
5. `while`문 안에서 `lt`를 빼줬을 때도 `3`번 과정을 거친다. (여기서 알아두어야 하는점은 `sum===target`이어도 `lt`를 빼줘야 다음 `rt`를 증가시킬 수 있다.)

```javascript
// 나의 코드
let n = 8;
let target = 6;
let arr = [1, 2, 1, 3, 1, 1, 1, 2];

console.log(solution(n, target, arr));

function solution(n, target, arr) {
  let lt = (rt = cnt = sum = 0);

  while (rt < n) {
    sum += arr[rt++];
    if (sum === m) cnt++;
    while (sum >= m) {
      sum -= arr[lt++];
      if (sum === m) cnt++;
    }
  }

  return cnt;
}
```

```javascript
// 강의 코드
let n = 8;
let target = 6;
let arr = [1, 2, 1, 3, 1, 1, 1, 2];

console.log(solution(n, target, arr));

function solution(n, target, arr) {
  let lt = (cnt = sum = 0);

  for (let rt = 0; rt < n; rt++) {
    sum += arr[rt];
    if (sum === target) cnt++;
    while (sum >= target) {
      sum -= arr[lt++];
      if (sum === target) cnt++;
    }
  }
  return cnt;
}
```

---
## 📍 section05 - 4 - 연속 부분수열2
<a href='https://ywtechit.tistory.com/277'>연속 부분수열1</a>보다 약간 더 어려운 문제였다. 이전 문제는 다음 `rt` 포인터가 기준보다 커지면 `arr[lt++]`처리를 해줬는데, 이 문제는 특정 기준 값 이하인 경우 새로운 숫자가 포함된 연속부분수열을 구해주면 된다. 그럼 이전 숫자는 안구하는지 궁금 할 수 있는데, 이전 숫자가 끝에 있으면서 연속수열인 값은 이전과정에서 구했기 때문에, 새로운 경우의 수만 누적 해주면 된다. 

1. 반복문을 따라 `sum+=arr[rt]`를 누적한다.
2. 만약, `sum>target`이면 `sum<=target`이 될 때 까지 `sum`을 빼준다.(`lt`)
3. 마지막에 부분수열이 몇개있는지 계산해주면 된다. (경우의 수를 구할때는 `rt-lt+1`을 해주면 된다.)

![](https://images.velog.io/images/abcd8637/post/1c359b1a-5762-4e26-b222-70a2ab01a219/KakaoTalk_Photo_2021-08-27-18-11-11.jpeg)

```javascript
let n = 5;
let target = 5;
let arr = [1, 3, 1, 2, 3];

console.log(solution(n, target, arr));

function solution(n, target, arr) {
  let lt = sum = ans = 0;

  for (let rt = 0; rt < n; rt++) {
    sum += arr[rt];

    while (sum > target) {
      sum -= arr[lt++];
    }
    ans += rt - lt + 1;
  }
  return ans;
}
```

---
## 📍 section05 - 5 - 최대 매출
연속된 `K`일 동안의 최대 매출액을 구하는 `slidingWindow` 문제인데 여기서 문제인건 `slidingWindow`을 처음 배운것이다. `twoPointer`를 배웠다면 범위를 많이 벗어나지 않아서 다행이었다. `N`의 범위는 `100,000`까지인데, 만약, 시간복잡도가 `O(N^2)`이었다면 시간초과 판정을 받았을 것이다. 되도록 `O(nlogn)`이내로 끊자.

이 문제의 핵심요지는 `연속된 3일간`인데, 나는 `while`문으로 투 포인터를 사용하면서 `rt-lt+1===k`을 지키는 선에서 최대매출을 계산했다. 그와 비슷하게 강사님은 `for`문으로 푸셨는데, 이전에 `k`번째까지의 합을 구해놓고, `sum`을 누적하면서 `k`번째 이전의 인덱스를 계속 빼줬다. 즉, 이전단계+현재단계에 중복되는 수는 연산에서 제외시키고 다음 `sum`에 누적될 새로운 값과 `k`번째 이전의 값만 연산에 포함시키는 것이다. `k`번째 이전의 인덱스만 빼주는 이유는 이전 `index`와 현재 `index`는 중복되기 때문인데, 만약 `bruteForce`로 풀었다면 중복값을 고려하지 않기때문에 이중반복문을 사용했을 것이다.

`bruteForce`로도 풀어봤고 `slidingWindow`로도 풀었다.

![](https://images.velog.io/images/abcd8637/post/56ebbb4f-7fac-4108-a6de-8f00227b6c0e/KakaoTalk_Photo_2021-08-25-09-39-21.jpeg)

```javascript
// bruteForce
let n = 10;
let k = 3;
let arr = [12, 15, 11, 20, 25, 10, 20, 19, 13, 15];

for (let i=0; i<n-k+1; i++){
    let max = 0;
    for (let j=i; j<i+k; j++){
        max += arr[j]
    }
    console.log(max)
}
```

```javascript
let n = 10;
let k = 3;
let arr = [12, 15, 11, 20, 25, 10, 20, 19, 13, 15];

// sliding window1 나의 코드
function solution(n, k, arr) {
  let lt = rt = currentSum = 0;
  let max = Number.MIN_SAFE_INTEGER;

  while (rt < n) {
    currentSum += arr[rt];
    if (rt-lt+1 === k) {
      max = Math.max(max, currentSum);
      currentSum -= arr[lt++];
    }
    rt++;
  }
  return max;
}

// sliding window2 강의 코드
function solution(n, k, arr) {
  let lt = rt = currentSum = 0;
  let max = Number.MIN_SAFE_INTEGER;
  let answer;

 for (let i=0; i<k; i++) currentSum+=arr[i];
 answer = currentSum;

 for (let i=k; i<n; i++){
     currentSum+=(arr[i] - arr[i-k])
		 answer = Math.max(answer, currentSum);
 }
return answer;
}
```

---
## 📍 section05 - 6 - 학급회장
투표 용지를 보고 어떤 기호의 후보가 학급회장이 되었는지 출력하는 문제이다. 이런 유형은 해쉬(`hash`)로 풀면된다. `JS`에서 `hash` 문제는 `key:value` 형태인 `object`로 풀면 될 줄 알았는데, `ES6` 문법에 새로운 자료구조인 `Map` 형으로 푸는것이 더 쉬웠다. 기본적으로 `object`의 `key`는 `string | symbol`형만 가능하지만 `Map`의 `key`는 함수, 객체, 모든 기본요소를 포함할 수 있다. 또한 `object`는 `nonIterable`이라서 `for`문 대신 `Object.entries() | Object.keys() | Object.values()`를 사용했지만 `Map`은 `iterable` 하기 때문에 `for`문을 사용할 수 있다. 또한, `object`의 순서는 `random`이지만, `Map`의 순서는 `sequence`하다. `Map`과 `object`의 차이를 더 보고싶다면 <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map'>`MDN`</a>을 참고하자. 알고리즘에서 `Map`처럼 `key:value`형을 `iterable`할 수 있다는 특징만으로도 충분히 사용가치가 있다고 생각한다.

1. 투표용지를 `hash`값으로 각각 저장한다.
2. 반복문으로 `key, value`를 순회하면서 가장 많은 투표 수를 가진 후보를 최대 후보로 갱신시킨다.

```javascript
let n = 15;
let votes = "BACBACCACCBDEDE";

console.log(solution(n, votes));

function solution(n, votes){
  let vote = new Map();
  let maxVote = Number.MIN_SAFE_INTEGER;
  let maxCandidate;

  for (let x of votes){
    if (vote.has(x)) vote.set(x, vote.get(x)+1);
    else vote.set(x, 1);
  }

  vote.forEach((numberOfVote, candidate) => {
    if(numberOfVote>maxVote) maxVote=numberOfVote, maxCandidate=candidate;
  })
  return maxCandidate;
}
```

---
## 📍 section05 - 7 - 아나그램
`Anagram`은 두 문자열이 알파벳의 나열 순서를 다르지만 그 구성이 일치하면 두 단어를 아나그램이라고 한다. 이 문제를 `hash`로 풀면 `O(N)`으로 간단하게 풀 수 있다. 여기서 아나그램이 성립하지 않는 경우를 생각하면 편하다.

1. 문자열 `s1`의 원소를 `hash`값으로 만든다.
2. 비교할 문자열 `s2`를 반복문으로 순회하면서 아나그램이 되지 않는 경우를 찾는다.(아나그램이 성립하지 않는 경우: `s2`의 값이 `hash`값에 존재하지 않는경우, `hash`값의 `value`가 1보다 작은경우)
3. 조건문밖에는 `hash`의 `key`값을 `-1`씩 빼준다.

```javascript
let s1 = "AbaAeCe";
let s2 = "baeeACA";
let s1H = new Map();

console.log(solution(s1, s2));

function solution(s1, s2) {
  for (let x of s1) {
    if (s1H.has(x)) s1H.set(x, s1H.get(x) + 1);
    else s1H.set(x, 1);
  }

  console.log(s1H)

  for (let x of s2) {
    if (!s1H.has(x) | (s1H.get(x) < 1)) return "NO";
    s1H.set(x, s1H.get(x) - 1);
    console.log(x, s1H)
  }
  return "YES";
}
```

---
## 📍 section05 - 8 - 모든 아나그램 찾기
`S` 문자열에서 `T`문자열과 아나그램이 되는 `S`의 부분 문자열의 개수를 구하는 문제이다. 문제가 조금 어려울 수 있는데, 요구사항을 하나씩 구현하면 된다. 이전까지 아나그램 문제를 풀 때는 `hash`의 특징을 사용했고, 부분 문자열을 구하는 방식은 `slidingWindow`을 이용하여 풀었다. 여기에 인덱스를 따로 설정하게 `twoPointer` 방식만 적용해주면 된다.

나는 `while`문을 사용해서 풀었는데, 올바른 방향으로 풀었는지 궁금해서 <a href='https://www.inflearn.com/questions/294479'>질문</a>을 남겼더니 선생님께서 칭찬해주셨다.(☺️ ☺️ ) 이것보다 더 짧은 코드로 짜고 싶다는 생각이 들었다.

![](https://images.velog.io/images/abcd8637/post/0d6bfe86-c373-4b59-af30-8855e50ac38a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-30%2011.43.24.png)

나의 방법은 다음과 같다.
1. 투 포인터를 사용해 `rt++`가 되면서 `sum`을 구한다. 
2. `sum`의 길이가 `m`과 동일하면 여기서 `hash`값을 구한다.
3. `sHash`값과 `t`를 비교하여 `anagram`이 맞는지 검사하고 `flag`를 통해 결과를 저장한다. `true | false`
4. `flag`가 `true`면 `cnt++`
5. `sum`의 길이가 `t.length`보다 커지면 그때 `lt`의 값을 빼준다.(빼주는 과정은 `slice`를 이용함)

코드를 짜고 보니까 `while`문 마다 `for`문이 두 번 돌고 `slice`과정까지 거치므로 시간복잡도가 꽤 나올것 같았다. 그럼, `while`문 밖에서 미리 `hash`값을 선언하면 어떨까?

선생님께서는 이렇게 푸셨다.
1. `for` 전에 `m-1`까지 `sum`을 구한다.(이후 `while`문에서 `sum` 값을 구함)
2. `for` 전에 `t`의 `hash`값을 구한다.
3. `rt`를 돌면서 현재 `hash`값을 구한다.
4. `compareAnagram` 함수를 돌면서 `anagram`이 맞는지 검사한다.
5. 이후 `lt`값의 `value`를 1씩 빼주고, 만약 `tH.get(value) === 0`이면, `delete(key)` 해준다. 0이 될때 `key`는 더 이상 필요가 없기 때문이다. (현재 `lt`는 `t.length-3`번째 위치한다.)

```javascript
let s = "bacaAacba";
let t = "abc";

console.log(solution(s, t));

// 내 코드
function solution(s, t) {
  let n = s.length;
  let m = t.length;

  let sum = "";
  let lt = rt = cnt = 0;

  while (rt < n) {
    sum += s[rt];

    if (rt - lt + 1 >= m) {
      let sH = new Map();
      let temp = sum;
      let flag = true;

      for (let x of temp) {
        if (sH.has(x)) sH.set(x, sH.get(x) + 1);
        else sH.set(x, 1);
      }

      for (x of t) {
        if (!sH.has(x) || sH.get(x) === 0) flag = false;
        sH.set(x, sH.get(x) - 1);
      }

      if (flag) cnt++;
      sum = sum.slice(1);
      lt++;
    }
    rt++;
  }
  return cnt;
}
```

```javascript
// 강의코드
let s = "bacaAacba";
let t = "abc"

function compareAnagram(sH, tH) {
  if (sH.size !== tH.size) return false;

  for (let [key, value] of tH) {
    if (!sH.has(key)) return false;
    if (sH.get(key) !== value) return false;
  }
  return true;
}

console.log(solution(s, t));

function solution(s, t) {
  let n = s.length;
  let m = t.length;
  let cnt = lt = 0;

  let sH = new Map();
  let tH = new Map();

  for (let i = 0; i < m - 1; i++) {
    if (sH.has(s[i])) sH.set(s[i], sH.get(s[i]) + 1);
    else sH.set(s[i], 1);
  }

  for (let x of t) {
    if (tH.has(x)) tH.set(x, tH.get(x) + 1);
    else tH.set(x, 1);
  }

  for (let rt = m - 1; rt < n; rt++) {
    if (sH.has(s[rt])) sH.set(s[rt], sH.get(s[rt]) + 1);
    else sH.set(s[rt], 1);

    if (compareAnagram(sH, tH)) cnt++;

    sH.set(s[lt], sH.get(s[lt]) - 1);
    if (sH.get(s[lt]) === 0) sH.delete(s[lt]);
    lt++;
  }
  return cnt;
}
```

---
## 📍 section06 - 1 - 올바른 괄호
이번 섹션은 `stack`과 `queue` 자료구조를 배운다. 이 문제를 풀고나서 <a href='https://www.acmicpc.net/problem/9012'>백준9012 - 괄호</a>를 푸는것을 추천한다.

풀이방법은 다음과 같다. 입력 값은 오직 `(`, `)`만 있다는 것을 알면 조금 더 쉽게 풀 수 있다.
 
1. `(`가 나오면 `stack`에 `push`한다.
2. `)`가 나왔을 때 `stack`이 비어있다면 짝을 지을 괄호가 없기 때문에 `false`를 `return`하면 되고, `stack`이 비어있지 않다면 `(`만 있을것이기 때문에 `stack.pop()`을 해준다.
3. 반복문이 모두 종료된 이후 `stack`을 봤을 때 한개라도 남아있다면 올바른 괄호가 매칭되지 않았기 때문에 `false` 한개라도 없으면 `true`를 리턴해준다.

```javascript
let s = ")())"

console.log(solution(s));

function solution(s) {
  let stack = [];

  for (let x of s) {
    if (x === "(") stack.push(x);
    else {
      if (stack.length===0) return "NO";
      stack.pop()
    }
  }
  if(stack.length>0) return "NO";
  return "YES";
}
```

---
## 📍 section06 - 2 - 괄호 문자 제거
소괄호`()` 사이의 모든 문제를 제외하고 남은 문자만 출력하는 문제다. 나의 풀이방법은 다음과 같다.

1. 반복문을 선언하고 현재 값이 문자인지 아닌지 검사한다.(정규식) 이때, `stack`에 아무것도 없다면 `answer`에 값을 더해준다.
2. 현재값이 `(`면 모두 `stack`에 넣는다.
3. 현재값이 `)`인데, 만약 `stack[-1]`이 `(`면 `stack.pop`을 해준다.

선생님은 조금 더 간단하게 푸셨다.
1. `(`와 문자는 모두 `stack.push`한다.
2. `)`가 나오면 `(`가 나올때까지 모두 `pop`해준다.

```javascript
let s = "(A(BC)D)EF(G(H)(IJ)K)LM(N)";
// let s = "(AB(A))B(A)";

console.log(solution(s));

// 나의코드
function solution(s) {
  let stack = [];
  let answer = "";

  for (let x of s) {
    if (stack.length===0 && /[A-Z]/.test(x)) answer+=x;

    if (x === "(") stack.push(x);
    else if(x === ")") if (stack[stack.length - 1] === "(") stack.pop();
  }
  return answer;
}

// 강의코드
function solution(s){
    let stack = [];

    for (let x of s){
        if (x === ")") while(stack.pop() !== "(");
        else stack.push(x)
    }
    return stack.join("");
}
```

---
## 📍 section06 - 3 - 크레인 인형뽑기(카카오 기출)
<a href='https://programmers.co.kr/learn/courses/30/lessons/64061'>프로그래머스</a>에도 나와있는 문제다. 한창 `python`으로 풀때는 끝까지 풀지 못했는데 지금 와서 `JS`로 풀어보니까 정답판정을 받았다. 지금도 생각나는것이 집게가 위에서부터 내려오게되면 2차원배열에서는 `arr[row][column]`가 아니라 `arr[column][row]`로 놓고 풀었어야하는데, 왜 그렇게 풀어야되는지 몰랐고, 집게로 인형을 뽑고 난 이후에 해당 값을 0으로 바꿔줘야 또 집게가 내려오면 다음 인형을 뽑을 수 있는데 이 과정을 이해하지 못했었다.

풀이 방법은 다음과 같다.
1. `move`는 배열의 인덱스를 건드려야하므로 각각 1씩 빼주고 계산해야한다.
2. 집게가 내려오는 `column`에 값이 있으면 인형을 뽑아 `basket`으로 옮긴다. 만약, 현재 집게의 인형과 `basket` 마지막 인형이 같으면 없애주고 `cnt+=2`를 해준다.
3. 현재 집게가 집고있는 인형과 `basket[-1]`이 다르면 `basket`에 넣어주고, 집게를 집은 위치를 0으로 바꿔준다.
4. 인형을 뽑았으면 현재 `move`는 종료하고 다음 `move`로 넘어간다.

```javascript
let boards = [
  [0, 0, 0, 0, 0],
  [0, 0, 1, 0, 3],
  [0, 2, 5, 0, 1],
  [4, 2, 4, 4, 2],
  [3, 5, 1, 3, 1],
];
let moves = [1, 5, 3, 5, 1, 2, 1, 4];

console.log(solution(boards, moves));

function solution(boards, moves) {
  let n = boards.length;
  let basket = [];
  let cnt = 0;

  for (let idx of moves) {
    let move = idx - 1;
    for (let i = 0; i < n; i++) {
      if (boards[i][move]) {
        if (basket[basket.length - 1] === boards[i][move]) basket.pop(), cnt += 2;
        else basket.push(boards[i][move]);
        boards[i][move] = 0;
        break;
      }
    }
  }
  return cnt;
}
```

---
## 📍 section06 - 4 - 후위식 연산(postfix)
간단하게 후위식연산에 대해서 알아보자면, 우리가 일반적으로 사용하는 사칙연산 `7+7`은 중위표기식이라고 한다. (숫자 사이에 `+-*/`가 들어감.) 후위표기식은 주로 컴퓨터가 많이 사용하는 방법으로 괄호가 없어도 우선순위를 정확하게 알 수 있다는 점에서 `S/W`에서 널리 쓰인다.

1. 숫자를 만나면 `stack`에 담는다.
2. 연산자를 만나면 `stack`에서 2개의 값을 꺼내 계산한다.
3. 계산한 값을 다시 `stack`에 넣는다.
4. `stack`에 값이 1개면 계산이 끝난다.

나는 이렇게 풀었다.
1. 숫자는 모두 `stack`에 넣는다.
2. 연산자를 만났을 때 `stack`에서 값 2개를 빼고 `getCalculator` 함수에 넣는다.
3. 연산이 끝나면 다시 `stack`에 넣는다.

선생님은 이렇게 푸셨다.
1. `isNaN`이 `false`면 숫자이므로 해당 값을 `stack`에 넣는다.
2. 숫자가 아닌 값(연산자)은 `stack`에서 `pop`을 2번 진행하여 `lt, rt`로 선언한다.
3. 연산 이후 다시 `stack`에 넣는다.

```javascript
// 나의 코드
let postFix = "352+*9-";

console.log(solution(postFix));

function getCalculator(operator, lt, rt) {
  switch (operator) {
    case "+":
      return lt + rt;
    case "-":
      return lt - rt;
    case "*":
      return lt * rt;
    case "/":
      return lt / rt;
  }
}

function solution(postFix) {
  let stack = [];
  for (let x of postFix) {
    if (/[0-9]/.test(x)) stack.push(+x);
    else {
      let operator = x;
      let rt = stack.pop();
      let lt = stack.pop();
      stack.push(getCalculator(operator, lt, rt));
    }
  }
  return +stack;
}
```

```javascript
// 강의 코드
let postFix = "352+*9-";

function solution(s){
    let stack = [];
    for (let x of s){
        if(!isNaN(x)) stack.push(+x);
        else{
            let rt = stack.pop();
            let lt = stack.pop();
            if (x==="+") stack.push(lt+rt);
            else if (x==="-") stack.push(lt-rt);
            else if (x==="*") stack.push(lt*rt);
            else if (x==="/") stack.push(lt/rt);
        }
    }
    return +stack;
}
```

---
## 📍 section06 - 5 - 쇠막대기
<a href='https://ywtechit.tistory.com/198'>이전</a>에 풀어봤던 문제다. 당시 처음 풀 때는 이 문제를 왜 `stack`으로 푸는지 이해가 안됐는데, 다시 보니까 조금이나마 이해가 된다. 이전 `stack` 유형과는 달리 `stack[-1]`값을 비교하는것이 아니라 주어진 문자열 `s[i-1]`을 기준으로 비교하기 때문에 그 부분을 잘 캐치해야 문제를 풀 수 있다. 그리고 레이저를 만났을 때 `cnt`를 계산하는 방법이 조금 어려울 수 있는데, 레이저를 만나게 되면 지금까지 `stack`에 들어가있는 `(`길이만큼 누적해주면 된다. `(`는 쇠막대기를 의미함. 레이저를 만나지 않고 쇠막대기 `(`를 만나게 되면 `cnt++`을 해주면 된다.

1. `(`는 무조건 `stack`에 넣는다.
2. `)`를 만날 때 `stack.pop()`을 하는데, 여기서 `s[i-1]`값이 `(`이라면 레이저(왜냐하면 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 즉, `()`형태로만 주어지기 때문)기 때문에 `stack`길이 만큼 `cnt`에 누적해주고 `s[i-1]` 값이 `)`라면 쇠막대기이므로 `cnt++`을 해준다.
3. 반복문이 끝나면 쇠막대기의 개수 `cnt`를 `return`한다.

```javascript
let s = "()(((()())(())()))(())"

console.log(solution(s));

function solution(s){
  let n = s.length;
  let stack = [];
  let cnt = 0;
  
  for (let i = 0; i < n; i++) {
    if (s[i] === "(") stack.push(s[i]);
    else {
      stack.pop();
      if (s[i - 1] === "(") cnt += stack.length;
      else cnt++;
    }
  }
  return cnt;
}
```

---
## 📍 section06 - 6 - 공주구하기
공주 구하기 문제는 <a href='https://ywtechit.tistory.com/94'>이전</a>에 풀었던 요세푸스 문제와 동일하다. 요세푸스문제는 `큐(queue)` 자료구조를 사용하면 풀 수 있다. 선생님께서는 이렇게 설명 해주셨다. 

1. `arr`에 `length`가 1개일때까지 반복한다.
2. `for`문을 사용해 `k-1`번 돌린다. `arr[0]`을 맨 뒤로 넣는다.
3. `k`번째 사람이 제외되어야 하므로 다음 값은 `shift()`한다.

```javascript
// 강의 코드
let n = 8;
let k = 3;

console.log(solution(n, k));

function solution(n, k){
  let arr = Array.from({length: n}, (v, i) => i+1);

  while(arr.length>=2){
      for (let i=0; i<k-1; i++) arr.push(arr.shift());
      arr.shift();
  }
  return +arr;
}
```

```javascript
// 나의 코드
let n = 8;
let k = 3;

console.log(solution(n, k));

function solution(n, k) {
  let princes = Array.from({ length: n }, (value, idx) => idx + 1);
  let cnt = 0;

  while (princes.length >= 2) {
    if (cnt === k - 1) princes.splice(0, 1), (cnt = 0);
    else princes.push(princes.shift()), cnt++;
  }

  return +princes;
}
```

```javascript
// 나의 코드2
let n = 8;
let k = 3;

console.log(solution(n, k));

function solution(n, k) {
  let princes = Array.from({ length: n }, (value, idx) => idx + 1);
  let cnt = 0;

  while (princes.length >= 2) {
    cnt = (cnt + k - 1) % princes.length;
    princes.splice(cnt, 1);
  }

  return +princes;
}
```

---
## 📍 section06 - 7 - 교육과정 설계
현수가 짠 수업설계도가 주어진 수업계획표와 맞는지 검증하는 문제다. 마찬가지로 `queue` 자료구조를 사용하면 되는데, 현수의 수업 설계도를 앞에서부터 하나씩 꺼내서 비교해야한다. 그런데 `while`문 보다는 `for`문을 사용해야하는데 만약, 수업계획표가 수업설계도에 하나도 포함이 되어있지 않으면 `while`문이 멈추지 않는다. 따라서 `for`문을 사용해 수업설계도에 하나씩 접근하면서 수업 계획표가 있는지 살펴보는 방법이 괜찮은 접근 방법일 것이다.

나는 이렇게 풀었다.
1. 수업 설계도를 배열로 만든다.
2. 수업 계획표(target)를 하나씩 돌면서 수업 설계도(s)도 한번씩 돈다.
3. 수업 설계도의 맨 앞과 수업 계획표의 맨 앞이 똑같으면 `cnt++`하고 `s[0]`를 꺼낸다. 여기서 `s`는 문자열이기때문에 `splice`를 사용했다. 수업 설계도의 맨 앞과 수업 계획표의 맨 앞이 같지 않으면 제일 수업 설계도의 맨 앞을 맨 뒤로 보낸다.
4. 수업 계획표(`CBA`)의 `length` 만큼 반복

선생님은 이것보다 더 간단하게 푸셨다.
1. 수업 설계도를 `for`문으로 한바퀴 돈다.
2. 만약, `x`가 수업 계획표에 포함(`includes`)이 되어있는지 확인한다.
3. 참이면 만약, `x`와 `queue.shift()`를 비교하고 같지 않으면 `return "NO"`를 하고, 같으면 `shift()`한다.
4. 마지막에 `queue`의 길이를 확인해서 0보다 크면 수업 설계가 잘못된 것이므로 `NO`, 0이면 `YES`를 출력한다.

```javascript
// 나의 코드
let s = "CBDAGE";
let target = "CBA";

console.log(solution(s, target));

function solution(s, target){
    let cnt = 0;
    s = s.split("");

    for (let x of target){
        for (let y of s){
            if (s[0] === x){
                cnt++;
                s.splice(0, 1);
                break;
            }else s.push(s.shift());
        }
    }
    return cnt === target.length ? "YES" : "NO";
}
```

```javascript
// 강의 코드
let s = "CBDAGE";
let target = "CBA";

console.log(solution(s, target));

function solution(s, target) {
  let cnt = 0;
  let queue = target.split('');

  for (let x of s){
      console.log(s, x, queue)
      if (queue.includes(x)){
          if (x !== queue.shift()) return "NO";
      }
  }
  
  return queue.length>0 ? "NO" : "YES";
}
```

---
## 📍 section07 - 1 - 선택정렬
이번 섹션부터는 정렬(sort), 그리디(greedy), 결정알고리즘에 대해서 배운다. 블로그에 따로 게시하진 않았지만 이전에 종종 `삽입정렬`, `선택정렬`, `병합정렬`, `버블정렬`, `퀵정렬` 코드 구현까지 공부했는데, 항상 정렬 문제를 풀 때마다 알맞는 정렬 코드를 구현할려고 하면 까먹는다. 😅 😅 이번 섹션을 풀면서 언제 어떤 정렬을 사용해야하는지 잘 알아둬야겠다.

선택정렬에 관한 짧은 영상은 <a href='https://www.youtube.com/watch?v=jtxwQ7ChiII'>선택정렬 5분만에 이해하기 - 코딩하는거니</a> 개인적으로 이 분 영상이 길지 않고 핵심만 가르쳐주는 영상이어서 좋았다.

선택정렬은 가장 작은 숫자를 차례대로 탐색하여 가장 왼쪽 자리부터 `swap` 하는 정렬이다. 이중 반복문으로 전체 원소를 탐색하고 나보다 작은 값이 있으면 두 개의 위치를 서로 바꾸는 정렬이다. 시간복잡도는 `O(N^2)`이고, 최적의 경우(정렬되어있는 경우)에도 상관없이 원소를 모두 비교하므로 마찬가지로 O(N^2)의 시간 복잡도를 나타낸다.

![](https://images.velog.io/images/abcd8637/post/2a5d340e-ac88-4eda-8518-10697e1c138a/insertion-sort.gif)

(출처: <a href='https://visualgo.net/en/sorting'>VisuAlgo</a>)

```javascript
// 나의 코드(j번 모두 바꾸는 방법)ㄴ
let n = 6;
let arr = [6, 5, 4, 3, 2, 1];

console.log(solution(n, arr));

function solution(n, arr) {
  for (let i=0; i<n-1; i++) {
    for (let j=i+1; j<n; j++) {
      if (arr[i]>arr[j]) {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }
  return arr;
}
```

```javascript
// 강의 코드(j번 안에서 idx를 갱신하여 한번에 바꾸는 방법)
let n = 6;
let arr = [6, 5, 4, 3, 2, 1];

console.log(solution(n, arr));

function solution(n, arr) {
    for (let i=0; i<n-1; i++) {
        let idx=i;
        for (let j=i+1; j<n; j++) {
            if (arr[i] > arr[j]) idx = i;
        }
        [arr[i], arr[idx]] = [arr[idx], arr[i]];
    }
    return arr;
}
```

---
## 📍 section07 - 2 - 버블정렬
구현하기 쉬운 정렬 중 한개다. 데이터가 정렬되는 모습이 버블같아서 붙여진 이름이다. (데이터가 왼쪽으로 이동하는 모습이 거품이 올라오는 모습 같은가?)

![](https://images.velog.io/images/abcd8637/post/584f7e86-8f33-45a9-aec2-65866dacdfcb/bubble-srot.gif)

버블정렬은 다른 정렬에 비해 구현이 쉽다는 장점을 가지고있다.(이중 반복문) 하지만, 시간복잡도는 `O(N^2)`가 걸리므로 실제 많이 쓰이지는 않는다. (이미 정렬이 되어있는 최적화의 경우에는 `O(N)` 걸린다.)

1. `j`가 돌 때마다 `j+1`과 매번 비교한다.(실행횟수가 많다.)
2. `i`가 한바퀴 돌고 난 이후 다음 `j`번을 돌 때 `i`의 맨 마지막 값이 하나 줄어든 범위까지만 탐색한다. (`1번`을 거치면서 제일 큰 값은 맨 뒤로 가있다라고 확정을 짓는다.)

```javascript
let n = 6;
let arr = [13, 5, 11, 7, 23, 15];

console.log(solution(n, arr));

function solution(n, arr) {
    for (let i = 0; i < n - 1; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        }
    }
    return arr;
}
```

---
## 📍 section07 - 3 - Special Sort(구글 인터뷰)
문제: 음의 정수는 앞쪽에 양의정수는 뒤쪽에 있어야 한다. 이때, 양의정수와 음의정수의 순서는 변함이 없어야한다. <a href='https://www.geeksforgeeks.org/move-negative-numbers-beginning-positive-end-constant-extra-space/'>GeeksforGeeks</a>에서 관련 문제를 가져왔다. 영어로 풀고 싶으면 사이트에 들어가서 푸는것을 권장한다.

이 문제를 풀때 2가지 방법이 떠올랐다. 

1. 한개는 `for`문을 돌면서 음수 먼저 `answer`에 `push`하고 또 `for`문을 돌면서 양수를 `answer`에 `push` 하는 방법
2. 버블정렬 방식의 일부를 가져와서 `j`가 음수이고 `j+1`이 양수면 `swap`하는 방법

시간복잡도는 1번(`O(N)`)으로 더 빠르지만 만약, 코딩인터뷰를 할 때 정렬을 이용해서 풀어보라고 할 때는 2번(`O(N^2)`)을 이용하면 된다.

```javascript
// 1번 방법
let n = 8;
let arr = [1, 2, 3, -3, -2, 5, 6, -6];

console.log(solution(n, arr));
👉🏽 [ -3, -2, -6, 1, 2, 3, 5, 6 ]

function solution(n, arr){
    let answer = [];
    
    for (let x of arr){
        if (x<0) answer.push(x);
    }
    
    for (let x of arr){
        if (x>0) answer.push(x);
    }
    return answer
}
```

```javascript
// 2번 방법
let n = 8;
let arr = [1, 2, 3, -3, -2, 5, 6, -6];

console.log(solution(n, arr));
👉🏽 [ -3, -2, -6, 1, 2, 3, 5, 6 ]

function solution(n, arr){
    for (let i=0; i<n-1; i++){
        for (let j=0; j<n-i-1; j++){
            if (arr[j]>0 && arr[j+1]<0) [arr[j], arr[j+1]] = [arr[j+1], arr[j]]
        }
    }
    return arr;
}
```

---
## 📍 section07 - 4 - 삽입 정렬
삽입정렬은 <a href='https://ywtechit.tistory.com/293?category=958175'>선택정렬</a>과 비슷하지만 조금은 다른 방식이다. 삽입정렬의 간략한 소개는 <a href='https://www.youtube.com/watch?v=iqf96rVQ8fY'>삽입정렬 5분만에 이해하기 - Gunny</a>의 영상을 확인하자. 

삽입정렬은 선택정렬보다 시간복잡도면에서 효과적인 알고리즘인데 만약, 데이터가 거의 정렬되어있다고 가정하면 `while`문을 거의 수행하지 않으므로 `O(N)`의 시간복잡도를 보여준다. 하지만 데이터가 역정렬(반대로 정렬)되어있다면 `index` 끝까지 `while`문을 수행하므로 최악의 경우인 `O(N^2)`을 나타낸다.

![](https://images.velog.io/images/abcd8637/post/7e6ffe29-3984-4d6b-8c44-c5328158bd41/insertion-sort.gif)

1. `i`가 1부터 시작하여 `n`까지 탐색한다. (`left` 인덱스 사용으로 인해 0부터 시작을 하지 않음)
2. `temp`에 `arr[i]`를 선언한다. (나중에 덮어씌운 값 맨 앞에 넣을 예정)
3. `left`가 0보다 크거나 && 나보다 좌측에 작은 값이 있을 때만 우측값에 현재값을 덮어씌운다.
4. `while`문이 거짓이 되면 제일 마지막으로 움직인 `left+1` 값에 `temp`를 넣는다. 

![](https://images.velog.io/images/abcd8637/post/48a62463-78ff-4322-89fb-2187eaa46fe7/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-09%2011.31.41.png)

```javascript
let n = 6;
let arr = [11, 7, 5, 6, 10, 9];

console.log(solution(n, arr));

// 나의 코드
function solution(n, arr) {
    for (let i = 1; i < n; i++) {
        let cur = arr[i];
        let left = i - 1;

        while (left >= 0 && arr[left] > cur) {
            arr[left + 1] = arr[left];
            left--;
        }
        arr[left + 1] = cur;
    }
    return arr;
}

// 강의 코드
function solution(n, arr) {
    for (let i=0; i<n; i++){
        let tmp = arr[i]
        let j;
        for (j=i-1; j>=0; j--){
            if (arr[j] > tmp) arr[j+1] = arr[j];
            else break;
        }
        arr[j+1] = tmp;
    }
    return arr;
}
```

---
## 📍 section07 - 5 - Least Recently Used(카카오 캐시 문제 변형)
간략한 문제 설명: `LRU` 알고리즘은 가장 최근에 사용되지 않은 것의 의미를 가지고 있다. 만약, `Cache Miss`일 땐 다음 `task`가 `cache`의 맨 앞에 오고 모든 작업이 뒤로 밀리고, `Cache Hit` 일 땐 다음 `task`와 동일한 `cache`안에 있는 값을 맨 앞으로 당겨오고 나머지는 한 칸씩 뒤로 미루는 문제이다. 예를 들어 현재 `cache`가 `[1, 2, 3, 0, 0]`이고 다음 `task`는 `2`라면 `[2, 1, 3, 0, 0, 0]`이 된다.

이 문제는 삽입정렬의 특징인 `target`을 `temp`에 저장하고 `temp`보다 `arr[i]=arr[i-1]`처럼 덮어씌우는 방식을 이용하면 풀 수 있는 문제이다. 중요한것은 실행속도를 얼마냐 빨리하느냐인데, 내가 작성한 코드는 3중 반복문이었고, 강의코드는 2중 반복문이었다. 이 문제를 풀 수 있는 방법은 4가지인데, 자신의 입맛대로 풀면 된다. 

첫번째 방법은 `hit | miss` 일때 모두 한칸씩 앞으로 밀거나 당기는 방법인데 썩 와닿지 않아서 직접 그려봤다. 다른 방법들에 비해 코드가 짧은것이 장점이다. 그리고 <a href='https://ywtechit.tistory.com/169'>저번</a>에 풀었던 <a href='https://www.acmicpc.net/problem/16935'>배열돌리기3</a> 문제처럼 지금과 같이 `target`을 `temp`로 빼두고 덮어씌우다가 제일 마지막 `index`에 할당해주는 방법을 종종 사용했었다.(잊지않으려고 <a href='https://ywtechit.tistory.com/212'>글</a>까지 적었는데.. 이제는 까먹지말고 제때 사용하자!!)

![](https://images.velog.io/images/abcd8637/post/208a2fa7-d351-4859-a375-5d6025c299cb/KakaoTalk_Photo_2021-09-10-11-46-07.jpeg)

1. `hit`, `miss` 둘 다 반복문을 이용해서 한칸씩 밀거나 당기고 마지막에 `cache[0]=x`를 넣는다.
2. `hit`일때 `for`문을 거꾸로 덮어씌우고, `miss` 일 때 `unshift`를 이용한다.
3. `hit`일때 `while`문을 거꾸로 덮어씌우고, `miss` 일 때 `unshift`를 이용한다.
4. `hit`일때 `splice(pos,1)`으로 해당 원소만 빼내어 맨 앞에 `unshift`해주고, `miss` 일 때 `unshift`를 이용한다.

```javascript
// 방법1
let s = 5;
let n = 9;
let order = [1, 2, 3, 2, 6, 2, 3, 5, 7];

console.log(solution(s, n, order));

function solution(s, n, order){
    let cache = Array.from({length: s}, () => 0);

    for (let x of order){
        let pos=-1;
        for(let i=0; i<s; i++) if (cache[i] === x) pos=i;
        if (pos === -1){
            for(let i=s-1; i>=1; i--) cache[i]=cache[i-1]
        }else{
            for(let i=pos; i>=1; i--) cache[i]=cache[i-1]
        }
        cache[0]=x
    }
    return cache.join(" ");
}
```

```javascript
// 방법2
let s = 5;
let n = 9;
let order = [1, 2, 3, 2, 6, 2, 3, 5, 7];

console.log(solution(s, n, order));

function solution(s, n, order){
    let cache = Array.from({length: s}, () => 0);
    for (let x of order){
        let pos=-1;
        for (let i=0; i<n; i++){
            if (cache[i]===x) pos=i
        }
        if (pos === -1){
             cache.unshift(x);
             if (cache.length > s) cache.pop();
        }
        else{
            let temp = cache[pos];
            for (let i=pos; i>=0; i--) cache[i] = cache[i-1];
            cache[0] = temp;
        }
    }
    return cache.join(" ");
}
```

```javascript
// 방법3
let s = 5;
let n = 9;
let order = [1, 2, 3, 2, 6, 2, 3, 5, 7];

console.log(solution(s, n, order));

function solution(s, n, order){
    let cache = Array.from({length: s}, () => 0);

    for (let x of order){
        let pos=-1;
        for (let i=0; i<n; i++){
            if (cache[i]===x) pos=i
        }
    
        if (pos === -1){
            cache.unshift(x);
            if (cache.length > s) cache.pop();
        }
        else{
            let temp = cache[pos];
            let left = pos-1;
            while(left>=0) {
                cache[left+1] = cache[left];
                left--;
            }
            cache[0] = temp;
        }
    }
    return cache.join(" ");
}
```

```javascript
// 방법4
let s = 5;
let n = 9;
let order = [1, 2, 3, 2, 6, 2, 3, 5, 7];

console.log(solution(s, n, order));

function solution(s, n, order){
    order.forEach((val) => {
        let pos = -1;
        for (let i=0; i<s; i++) if (cache[i] === val) pos = i;
        if (pos === -1) {
            cache.unshift(val);
            if(cache.length>s) cache.pop();
        } else {
            cache.splice(pos, 1);
            cache.unshift(val)
        }
        return cache.join(" ");
    });
}
```

---
## 📍 section07 - 6 - 장난꾸러기 현수
여러 학생들 사이에서 자리를 바꾼 현수와 짝꿍의 번호를 출력하는 문제다. `sort`를 사용하지 않고 앞 뒤 `index`를 비교하여 감소하는 `index`면 서로 자리를 바꿨다라고 판단할 수 있지만, 앞 뒤 `index`가 동일할 때는 어느번호가 현수, 짝궁인지 모르기 때문에 `sort`를 사용했다. `arr`과 `copyArr`을 비교한 다음, `value`가 다른 `index`를 답으로 리턴했다.

```javascript
// let arr = [120, 125, 152, 130, 135, 135, 143, 127, 160];
let arr = [120, 130, 150, 150, 130 ,150]

console.log(solution(arr));

function solution(arr) {
    let sortArr = [...arr];
    let ans = [];
    sortArr.sort((a, b) => a - b);

    arr.forEach((val, idx) => {
        if (val !== sortArr[idx]) {
            ans.push(idx+1)
        }
    });

    return ans.join(" ");
}
```

---
## 📍 section07 - 7 - 좌표정렬
평면상의 좌표(x, y)가 주어질 때 모든 좌표를 오름차순으로 정렬하는데 만약, `x`값이 같으면 `y`을 기준으로 정렬하는 문제다. <a href='https://ywtechit.tistory.com/269?category=960739'>이전</a>글도 참고하자.

```javascript
// let arr = [120, 125, 152, 130, 135, 135, 143, 127, 160];
let arr = [120, 130, 150, 150, 130 ,150]

console.log(solution(arr));

function solution(arr) {
    let sortArr = [...arr];
    let ans = [];
    sortArr.sort((a, b) => a - b);

    arr.forEach((val, idx) => {
        if (val !== sortArr[idx]) {
            ans.push(idx+1)
        }
    });

    return ans.join(" ");
}
```

---
## 📍 section07 - 8 - 회의실 배정(greedy)
이번 문제는 `greedy` 문제다. `greedy`가 무엇인지 궁금하다면 <a href='https://velog.io/@abcd8637/%EC%9D%B4%EA%B2%83%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%8B%A4-8%EC%9D%BC%EC%B0%A8'>이전</a>에 작성한 글을 참고하자. 보통 정렬문제와 자주 짝을지어 출제되는데 강의선생님께서 정렬 이후 순서대로 하나씩 처리하는 로직이나 우선순위큐를 사용하는 로직은 보통 그리디로 풀면 된다고 하셨다.

![](https://images.velog.io/images/abcd8637/post/d7369608-f49f-4e0e-90de-fdda7ab912ce/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-11%2010.23.55.png)

문제에서 회의가 겹치지 않으면서 회의실을 사용할 수 있는 최대수의 회의를 찾으라고 했는데, 최대한 많이 회의를 하려면 끝나는 시간이 짧은 순서대로 풀어야한다. 끝나는 시간이 긴 시간부터 풀게 되면 만약, 해당 시간이 끝나기 전에 2개의 회의를 진행할 수 있다면 손해기 때문이다.

1. 끝나는 회의 순으로 오름차순 정렬한다.
2. 이전 회의 종료시간 `eT(endTime)=0`으로 초기화 한다.
3. 현재 회의 시작시간과 이전 회의 종료시간을 비교하여 현재 회의시작시간이 이전 회의종료시간보다 크거나 같으면 회의를 진행한다. (`x[0]`: 현재 회의시작시간, `eT`: 이전회의 종료시간) 이후 `cnt++`
4. 현재 `eT`에는 `x[1]`(현재 회의종료시간)을 할당한다.
5. 반복문 끝까지 비교한다.

![](https://images.velog.io/images/abcd8637/post/cb3914a9-32d0-4931-97e3-eccc7150c92d/KakaoTalk_Photo_2021-09-11-10-29-55.jpeg)

```javascript
let n = 5;
let arr = [[1, 4], [2, 3], [3, 5], [4, 6], [5, 7]];

console.log(solution(n, arr));

function solution(n, arr) {
    arr.sort((a, b) => {
        if (a[1] === b[1]) return a[0] - b[0];
        else return a[1] - b[1];
    });

    let eT = 0;
    let cnt = 0;

    for (let x of arr) {
        if (eT <= x[0]) {
            eT = x[1];
            cnt++;
        }
    }

    return cnt;
}
```

---
## 📍 section07 - 9 - 결혼식
피로연 장소에 동시에 존재하는 최대 인원수를 구하여 그 인원을 수용할 수 있는 장소를 빌리려고 한다. 만약, 입력이 13 15라면 13시 정작에 피로연장에 존재하고 15시에는 존재하지 않는문제다. 첫째 줄에 피로연장에 동시에 존재하는 최대 인원을 출력하는 문제다.

이 문제도 `greedy`로 풀 수 있는 문제인데, <a href='https://ywtechit.tistory.com/302'>회의실 배정</a>처럼 입력을 정렬을 하되, 정렬 기준을 `결혼식에 등장하는 시간(s)`, `결혼식장에서 나가는 시간(e)`으로 나눠서 오름차순으로 정렬을 해야한다. 입력을 타임라인형식으로 그려보면 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/d47c5608-2d56-43c7-8936-417cc1e0338d/KakaoTalk_Photo_2021-09-11-09-20-45.jpeg)

여기서 주의할 점은 `나간시간(e)`은 포함하지 않으므로 오름차순으로 정렬할 때 `들어오는시간(s)`과 `나가는시간(e)`이 동일하면 `e`가 먼저 오게 설정한다. 

1. 피로연에 등장하는 시간과 나가는 시간을 나눈다.
2. 시간을 오름차순으로 정렬하는데 시간이 같다면 나간시간을 먼저 앞에 세운다. (나간시간은 정각에 존재하지 않기 때문)
3. 반복문을 돌면서 `s`를 만나면 `cnt++`을 해주고, `e`를 만나면 `cnt--`를 해준다.
4. `cnt`의 최대값을 갱신한다.

여담이지만, 문자를 기준으로 정렬하고 싶으면 `charCodeAt()` 함수를 사용해 비교문자를 `ASCII` 코드로 바꾸어 준 다음, 값을 비교해주면 된다. 여기선 `s`의 `ASCII`코드는 `115`이고, `e`는 `101`이므로 `e`가 더 작다.

```javascript
let n = 5;
let arr = [[14, 18], [12, 15], [15, 20], [20, 30], [5, 14]];

console.log(solution(n, arr));

function solution(n, arr) {
    let tL = [];

    for (let x of arr) {
        tL.push([x[0], "s"]);
        tL.push([x[1], "e"]);
    }

    tL.sort((a, b) => {
        if (a[0] === b[0]) return a[1].charCodeAt() - b[1].charCodeAt();
        else return a[0] - b[0];
    });

    let cnt = 0;
    let answer = 0;

    for (let x of tL) {
        if (x[1] === "s") cnt++;
        else cnt--;
        answer = Math.max(answer, cnt);
    }
    return answer;
}
```

---
## 📍 section07 - 10 - 이분검색
이분검색은 시간복잡도가 `O(logN)`으로 선형검색인 `O(N)`보다 빠른 특징을 가지고 있다. 대량의 데이터를 탐색할 때 효과적인데, 예를 들어 `1,000,000`개의 데이터에서 특정 값을 찾는다고 가정하면, 반복문을 사용해 선형적으로 탐색하면 최악의 경우 `백만번`을 돌아야하지만 `이진탐색(binarySearch)`을 이용하면 최대 `11`번까지 돌면 된다. 하지만, 이진탐색은 `오름차순` 혹은 `내림차순`으로 정렬되어있어야 찾을 수 있는 전제조건이 있다.

1. `while`문의 범위는 `lt<=rt`인데, `lt`와 `rt`가 같을 때 까지 돌고 그 `lt`가 `rt`보다 커질 경우는 탐색을 종료한다.
2. `mid`값을 갱신한다. 
3. `target`이 `arr[mid]`보다 왼쪽에 있을 경우 현재 `mid` 오른쪽에는 내가 찾으려는 값이 없으므로 다음 `rt`를 `mid-1`로 재설정한다.
4. `target`이 `arr[mid]`보다 오른쪽에 있을 경우 현재 `mid` 왼쪽에는 내가 찾으려는 값이 없으므로 `lt`를 `mid+1`로 재설정한다.

```javascript
let arr = [23, 87, 65, 12, 57, 32, 99, 81];
let m = 32;

console.log(binarySearch(arr, m));
👉🏽 3

function binarySearch(arr, target){ 
    let lt = 0;
    let rt = arr.length - 1;
    arr.sort((a, b) => a - b);

    while (lt <= rt) {
        let mid = Math.floor((lt + rt) / 2);

        if (arr[mid] === target) return mid + 1;
        else if (arr[mid] > target) rt = mid-1;
        else lt = mid+1;
    }
}
```

---
## 📍 section07 - 11 - 뮤직비디오(결정 알고리즘)
<a href='https://velog.io/@abcd8637/%EC%9D%B4%EA%B2%83%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%8B%A4-20%EC%9D%BC%EC%B0%A8'>이분탐색</a> 알고리즘을 응용해서 푸는 문제다. 보통 이분탐색을 이용한 문제는 `파라메트릭서치(Parametric Search)` 알고리즘의 방법으로 풀게 되는데, 이는 값의 최대값 혹은 최소값을 구하여 결정문제로 바꾸어 풀 수 있다. 결정알고리즘과 같은 문제는 탐색 범위가 큰 상황에서의 탐색을 가정하는 경우가 많으므로 탐색 범위가 `20,000,000(이천만)`을 넘어가면 이진탐색으로 접근해보자. 범위가 `10,000,000(천만)` 이상으로 넘어가면 이진 탐색처럼 `O(logN)`의 속도를 내야 하는 알고리즘을 떠올려야 풀 수 있는 경우가 많다.

파라메트릭서치의 주요 특징은 범위 내에서 조건을 만족하는 값이 있더라도 거기서 끝나는것이 아니라 그것보다 더 좋은 최적의 답이 있는지 탐색한다는 것이다. 미세팁을 말하자면 `흑백논리(?)`를 떠올리면 쉽게 풀 수 있다. 예를 들어 나이가 입력된 배열이 오름차순으로 정렬되어 있을 때 `19살` 보다 크지만 `19살`과 제일 가까운 사람을 찾는다고 가정해보자. 다음 사진처럼 현재 `mid`값이 `target`보다 왼쪽에 있으면 `mid`의 좌측은 답이 될 수 없다는 결론이 나온다. 그렇기 때문에 `mid`를 우측으로 이동하여 탐색을 계속하다보면 최적의 답을 찾을 수 있다. 

![](https://images.velog.io/images/abcd8637/post/f17429c6-bd14-43c2-97ab-92ec7b9b234f/KakaoTalk_Photo_2021-09-14-12-20-59.jpeg)

자, 이제 문제를 풀어보자.

문제: `DVD` 녹화시에는 순서가 그대로 유지되어야 한다. 1번 노래와 5번노래를 같은 `DVD` 에 녹화하기 위해서는 1번과 5번 사이의 모든 노래도 같은 DVD에 녹화 되어야 한다. 한 노래를 쪼개서 두 개의 `DVD`로 녹화할 수 없다. `M`개의 `DVD`에 모든 동영상을 녹화하기로 했다. DVD의 크기를 최소로 하려고한다. M개의 DVD는 모두 같은 크기여야 제조원가가 적게들기 때문에 꼭 같은 크기로 하자.

문제의 설명이 조금 어려울 수 있지만 결론적으로 `M`개의 `DVD`에 음악을 모두 같은 크기로 담아야하는데, 그 크기가 가장 최소가 되는 값을 찾는 문제다. 최적의 값을 찾아야 하기 때문에 이분탐색을 이용한 `파라메트릭 서치` 알고리즘을 사용하면 된다. 여기서 `lt`는 주어진 값의 제일 작은 값(`1`) 혹은 제일 큰 값(`9`)을 선언 할 수 있는데, `1`은 최적의 답과 근접하지 않으므로 제일 큰 값인 `9`를 주었다. `rt`는 `arr`을 모두 더한 값을 줬는데, 이는 한 `DVD`에 저장 할 수 있는 음악의 크기를 모두 더한 값이다. 혹은 부른 곡의 길이가 `10,000분`이하이므로 최대로 나올 수 있는 값인 `n*10000`을 줘도 된다. 지금까지 읽은 내용이 잘 이해가 되지 않으면 다음의 풀이과정을 살펴보자.

![](https://images.velog.io/images/abcd8637/post/b71d48e8-6e4e-479b-a2e3-498e26d9c207/KakaoTalk_Photo_2021-09-11-10-08-03.jpeg)

```javascript
let n = 9;
let m = 3;
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(solution(n, m, arr));
// let rt = n * 10_000;

function solution(n, m, arr){
    let lt = Math.max(...arr);
    let rt = 45;
    let answer;

    while (lt<=rt){
        let mid = Math.floor((lt+rt)/2);
        console.log(`lt=${lt}, rt=${rt}, mid=${mid}`)
        let cnt=1;
        let sum=0;

        for (let x of arr){
            if(sum+x>mid){
                cnt++;
                sum=x;
            }else sum+=x;
        }

        if (cnt <= m) answer=mid, rt=mid-1;
        else lt=mid+1;
    }
    console.log(answer)
}
```

---
## 📍 section07 - 12 - 마구간 정하기(결정 알고리즘)
문제: `N`개의 마구간이 수직선상에 있다. 각 마구간은 `x1, x2, x3, ..., xN` 의 좌표를 가지며 마구간간에 좌표가 중복되는 일은 없다. 현수는 `C`마리의 말을 가지고 있는데, 이 말들은 서로 가까이 있는것을 좋아하지 않는다. 가장 가까운 두 말의 거리가 최대가 되게 말을 마구간에 배치하고 싶다.

입력: 첫째줄에 자연수 `N`과 `C`의 공백을 사이에 두고 주어지고 둘째줄에 마구간의 좌표가 차례로 주어진다.

```javascript
5 3
1 2 8 4 9
```

이 문제를 `Parametric Search`를 이용하는 문제인데, 왜 이용해야하는지를 생각해보면, 가까운 두 말의 거리가 최대가 될 때까지 최적의 해를 계속 찾아야 하기 때문이다. 예를 들어 두 말의 거리(출력)가 `2`라고 가정하면, `C`마리의 말을 마구간의 좌표 내에 모두 배치 할 수 있다. 하지만, 이것이 최적의 답인가?를 고민하면 그렇지 않다. 왜냐면 `3`도 마구간의 좌표 내에 모두 배치 할 수 있음과 동시에 가장 가까운 두 말의 거리가 최대가 되기 때문이다. 하지만, `4`가 되면 수직선 상에 최대 2마리까지 밖에 배치 할 수 없다. 이처럼 더 이상 해를 찾을 수 없을 때까지 계속 최적의 해를 갱신해야하므로 `Parametric Search`를 이용해야한다. 보통 범위 내 조건을 만족하는 `최소 / 최대` 값을 찾는 문제거나, `n`의 값이 너무 크고 정렬을 통해 답을 찾는다면 `Parametric Search`를 이용하면 된다. 로직은 다음과 같다.

1. 가장 가까운 말의 거리를 찾을 때까지 최적의 해를 계속 갱신하는 방법
2. 주어진 좌표는 오름차순으로 정렬되어 있어야 말 사이의 거리를 구할 수 있다.
3. `lt`와 `rt`는 말 사이의 거리인데 `lt`는 말의 최소거리인 1이고, `rt`는 말의 최대거리인 `arr[arr.length-1]`이다.
4. 말 사이의 거리 (`mid`)가 가까울수록 말을 더 많이 배치할 수 있고 이때 `cnt(거리에 따라 배치한 말의 수)`가 달라지게 되는데, 이때 `c`보다 같거나 크면 주어진 수직선 상에서도 말을 더 많이 배치할 수 있기 때문에 답이 될 수 있다. 하지만 `c`와 같지 않기 때문에 거리를 조금씩 늘린다.(`lt=mid+1`) 반대로, `cnt<c`일 때는 말 사이의 거리를 너무 크게 잡아서 수직선 상에 말을 배치 할 수 없기때문에 거리를 좁혀야 한다. (`rt=mid-1`)
5. 거리를 더 이상 좁히거나 넓힐 수 없을 때 반복문을 종료한다.

![](https://images.velog.io/images/abcd8637/post/e746906c-ad0d-4fb2-83fe-193e1e972376/KakaoTalk_Photo_2021-09-13-07-56-48.jpeg)

```javascript
let n = 5;
let c = 3;
let arr = [1, 2, 4, 8, 9];

console.log(solution(n, c, arr));

function solution(n, c, arr){
    arr.sort((a, b) => a-b);
    let lt = 1;
    let rt = arr[arr.length-1];
    let answer;
    
    while (lt <= rt){
        let mid = Math.floor((lt+rt)/2);
        let cnt=1;
        let endPoint = arr[0]
        
        for (let i=1; i<n; i++){
            if (arr[i]-endPoint >= mid){
                cnt++;
                endPoint=arr[i]
            }
        }

        if (cnt >= c){
            answer=mid;
            lt=mid+1;
        }else rt=mid-1

    }
    return answer;
}
```

---
## 📍 section08 - 1 - 재귀함수
이번 섹션은 재귀함수와 완전탐색(깊이우선탐색: DFS)을 배운다. 이전부터 재귀파트는 어려움을 많이 호소했는데, 이번 섹션을 통해 감을 되찾았으면 좋겠다. 첫번째 문제는 자연수 `N`이 입력됐을 때 재귀함수를 이용하여 `1부터 N까지` 출력하는 문제다. <a href='https://ywtechit.tistory.com/48'>이전</a>에 <a href='https://codeup.kr/problem.php?id=1901'>코드업</a>에서 `python`으로 한번 풀어본 문제다. 예전에 재귀문제를 풀었을 때는 하단 `before` 방법처럼 호출된 재귀함수를 적고 `return`이 나오면 다시 올라가는 방법을 사용했는데, 이것의 단점은 재귀가 깊어지면 어떤 코드에서부터 다시 진행해야하는지 헷갈려서 많은 어려움을 겪었다. 하지만 강의선생님께서 `after` 방법처럼 현재 호출된 재귀 함수와 호출된 코드라인을 적어두면 다시 돌아왔을 때 어디서부터 진행되는지 바로 확인 할 수 있어 헷갈릴 일이 없다고 하셨다. 이 섹션을 풀면서 손으로 그릴 때는 `after` 방법처럼 해야겠다.

![](https://images.velog.io/images/abcd8637/post/99a1adf5-e41a-4345-9fee-0add9706042b/KakaoTalk_Photo_2021-09-15-11-14-27.jpeg)

1. `DFS`를 실행하면 `L-1` 함수를 호출한다.
2. 계속해서 `L-1`함수를 호출하다 `L`이 1보다 작으면 `return`하고 `stack`에 저장한 함수를 불러오면서 `console.log`를 실행한다.

```javascript
let n = 10;

solution(n);

function solution(n){
  function DFS(L) {
      if (L < 1) return;
      DFS(L - 1);
      console.log(L);
  }

  DFS(n);
}
```

---
## 📍 section08 - 2 - 재귀함수를 이용한 이진수 출력
10진수 `N`을 2진수로 변환하는 문제이다. <a href='https://ywtechit.tistory.com/307'>저번</a>에 풀었던 재귀함수에서 조금 응용하면 쉽게 풀 수 있는 문제다. 비록 재귀를 사용하진 않았지만 <a href='https://ywtechit.tistory.com/109'>이진수</a>와 관련한 문제는 <a href='https://www.acmicpc.net/problem/3460'>백준 3460 - 이진수</a>문제도 풀었다. 재귀를 이용할 때 초보자는 `if-else`문을 사용하는것이 더 이해하기 쉽다고 선생님께서 말씀하셨다. 이진수를 출력하려면 어떤 수를 몫이 `0`이 될 때까지 `2`로 계속 나누면서 나머지를 누적하는데 이때, 나머지를 거꾸로 누적해야 이진수가 된다. 예를 들어 `11`을 이진수로 표현한다고 가정하면 다음과 같이 계산하면 된다. 

![](https://images.velog.io/images/abcd8637/post/92d73fff-2e9b-4c2f-ad90-dfb21247f52a/KakaoTalk_Photo_2021-09-16-11-42-35.jpeg)

그리고 `answer`코드를 `DFS` 함수 위에 선언하냐 밑에 선언하냐에 따라 값이 달라지는데 `DFS` 위에 선언하게 되면 나머지가 반대방향으로 출력되는것을 알아두자.

1. `level(L)`이 `0`이 될때까지 재귀함수를 돌린다. `0`이면 `return`한다.
2. `0`이 아니면 재귀함수를 돌리는데, 인자는 `2`로 나눈 몫을 넣는다.
3. 모든 재귀함수를 들려서 나올차례가 되면 나오면서 나머지를 `answer`에 넣는다.

```javascript
let n = 11;

console.log(solution(n));

function solution(n){
  let answer="";
  function DFS(L){
    if (L === 0) return;
    else {
      DFS(Math.floor(L/2));
      answer+=(L%2)
    }  
  }
  DFS(n)
  return answer;
}
```

---
## 📍 section08 - 3 - 이진트리 순회(깊이우선탐색)
이진트리 순회가 무엇인지 모르는 사람은 어려울 수 있는 문제다. 여기서 <a href='https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%ED%8A%B8%EB%A6%AC'>이진트리</a>란 나무를 뒤집어 놓은 모양으로 한개의 부모 노드와 2개의 자식노드를 갖고 있는 트리구조를 일컫는다. 

![](https://images.velog.io/images/abcd8637/post/2d3cbd02-2fe2-4870-8a1b-809dad5c1a6d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-13%2011.02.11.png)

이진트리를 순회할 때는 3가지 방법이 있다. `전위순회(preOrder)`, `중위순회(inOrder)`, `후위순회(postOrder)`가 있는데 어떻게 순회하는지 간략하게 알아보자.

첫번째로 `전위순회(preOrder)`는 부모 → 왼쪽자식 → 오른쪽 자식순으로 탐색한다. 위 사진의 순회결과는 `1-2-4-5-3-6-7`가 된다. 두번째로 `중위순회(inOrder)`는 왼쪽자식 → 부모 → 오른쪽 자식순으로 탐색한다. 이때 주의할점은 더 이상 자식이 없을 때까지 내려간 다음 왼쪽자식을 탐색하는 것이다. 위 사진의 순회 결과는 `4-2-5-1-6-3-7`가 된다. 마지막으로 `후위순회(postOrder)`는 왼쪽자식 → 오른쪽자식 → 부모 순으로 탐색하는데 중위순회와 마찬가지로 더 이상 자식이 없을 때까지 내려간 다음 오른쪽자식을 탐색한다. 위 사진의 순회결과는 `4-5-2-6-7-3-1`가 된다.

사실 이렇게 이론으로 어떻게 순회하는지 배워도 막상 코드로 구현하려니까 손이 잘 움직이지 않았다. 이진트리를 배열로 구현하지 않고 `DFS`로 구현하는 이유는 간단했는데, 노드의 위치를 쉽게 접근(`indexing`)할 수 있으나 기억 공간의 낭비가 심하다는 단점이 있다고 말씀하셨다. 만약, 4개의 `data`를 배열로 이진트리처럼 표현하면 사용하지 않는 11개의 공간이 낭비된다고 하셨다.

![](https://images.velog.io/images/abcd8637/post/6b280e53-1c12-45f8-bae9-fd9bd29185e3/KakaoTalk_Photo_2021-09-16-12-09-20.jpeg)

강의 선생님께서 이 문제를 풀 때 왼쪽 자식은 현재 `L(level)`의 `2배`이고, 오른쪽 자식은 현재 `L(level)`의 `2배+1`이라는 성질을 이용해서 풀어보라고 하셨다. 결론적으로 코드는 다음과 같았는데, 신기한 점은 `console.log` 코드의 위치만 위 아래로 달라졌을 뿐인데 결과가 다르게 나온것이다. 

```javascript
// 전위순회(preOrder)
function solution1(v){
  function preOrder(v){
    if(v>7) return;
    else{
      console.log(v);
      preOrder(v*2);
      preOrder(v*2+1);
    }
  }
  preOrder(v);
}

solution1(1)
👉🏽 1 2 4 5 3 6 7

// 중위순회(inOrder)
function solution2(v){
  function inOrder(v){
    if(v>7) return;
    else{
      inOrder(v*2);
      console.log(v);
      inOrder(v*2+1);
    }
  }
  inOrder(v);
}

solution2(1)
👉🏽 4 2 5 1 6 3 7

// 후위순회(postOrder)
function solution3(v){
  function postOrder(v){
    if(v>7) return;
    else{
      postOrder(v*2);
      console.log(v);
      postOrder(v*2+1);
    }
  }
  postOrder(v);
}

solution3(1)
👉🏽 4 5 2 6 7 3 1
```

---
## 📍 section08 - 4 - 부분집합 구하기(DFS)
자연수 `n`이 주어지면 `1부터 N까지`의 원소를 갖는 집합의 부분집합을 모두 구하여 출력예제와 같은 순서로 출력하는데 공집합은 출력하지 않는 문제다. `N`의 범위는 `1<=N<=10`인데 만약, `N`이 10개라면 내가 구해야 할 부분집합의 개수는 `2^10-1 = 1,024-1(공집합)= 1,023`개이다. 재귀적인 방법으로 부분집합을 찾아 갈 때 다음처럼 그림을 그리면 이해하기가 쉽다.

```
// 입력
3

// 출력
1 2 3
1 2
1 3
1
2 3
2
3
```

![](https://images.velog.io/images/abcd8637/post/adf9747e-8e96-4dc3-a273-95cd1632a8bd/KakaoTalk_Photo_2021-09-17-10-20-00.jpeg)

1. 길이 `N`만큼 빈 배열을 0으로 선언한다. (마지막에 `index`를 출력하면 그것이 부분집합이 된다.)
2. 현재 `L`레벨 일 때, `visit[v] = 1`로 선언하여 재귀적으로 순회하고 `visit[v] = 0`로 선언하여 재귀적으로 순회한다.
3. 한 가지가 끝나면 값을 출력한다.

```javascript
let n = 3;

console.log(solution(3));

function solution(n) {
    let visit = Array.from({ length: n + 1 }, () => 0); // n번까지 idx가 생겨야하므로
    let answer = [];

    function DFS(v) {
        if (v === n + 1) {  // DFS가 1부터 시작하므로 v가 n+1일때까지 순회해야 정상적으로 index가 출력된다.
            let temp = "";
            for (let i = 0; i < visit.length; i++) {
                if (visit[i]) temp += (i + " ");
            }
            answer.push(temp.trim());
        } else {
            visit[v] = 1;
            DFS(v + 1);
            visit[v] = 0;
            DFS(v + 1);
        }
    }
    DFS(1);
    return answer.join("\n");
}
👉🏽 
1 2 3
1 2 
1 3
1 
2 3
2
3
```

---
## 📍 section08 - 5 - 합이 같은 부분집합(DFS: 아마존 인터뷰)
`N`개의 원소로 구성된 자연수 집합이 주어지면, 이 집합을 두 개의 부분집합으로 나눌 때 두 부분집합의 원소의 합이 서로 같은 경우면 YES, 그렇지 않으면 NO 를 출력하는 프로그램을 작성하는 문제다. 마찬가지로 순서도를 그려서 이해하는것이 가장 빠르나, 입력예제가 `n=6`이므로(총 64개의 가지를 그려야함) 따로 순서도를 그리지 않고 이런 방법으로 그리면 된다.

1. 어떤 부분집합의 합이 같은지를 찾으려면 부분집합이 나올 수 있는 경우의 수를 모두 구한다. `n=6`이므로 총 부분집합의 개수는 `2^6=64`가 나온다.
2. 합이 같은 부분집합을 찾을 때, A, B 부분집합을 모두 구하지 않고 한 부분집합만 구하고나서 `sum(배열) - aSum(한 부분집합) = aSum`이면 `aSum = bSum`이 된다.
3. 11번째 코드에 `edgeCut` 방식을 적용했는데, `edgeCut`이란 문제에서 주어진 출력을 만족하여 더 이상 계산 할 필요 없을 때 남은 재귀를 거치지 않고 `return`하여 출력하는 방식이다. 불 필요한 계산을 줄여 시간을 조금이나마 더 단축 할 수 있는 장점이 있다.

```javascript
let n = 6;
let arr = [1, 3, 5, 6, 7, 10];

console.log(solution(n, arr));

function solution(n, arr){
  let total = arr.reduce((prev, cur) => prev+cur);
  let flag = false;
  
  function DFS(L, sum){
    if (flag) return;  // edge cut
    if (L === n){
      if (total-sum===sum) flag = true
    }else{
      DFS(L+1, sum+arr[L]);
      DFS(L+1, sum);
    }
  }

  DFS(0, 0);
  return flag ? "YES" : "NO";
}
```

---
## 📍 section08 - 6 - 바둑이 승차(DFS)
문제: 철수는 `C`를 넘지 않으면서 그의 바둑이들을 가장 무겁게 태우고 싶다고 한다. `N`마리의 바둑이와 각 바둑이의 무게 `W`가 주어지면, 철수가 트럭에 태울 수 있는 가장 무거운 무게는 무엇일까요?

1. 부분집합을 이용한 문제다. 
2. 주어진 배열에서 부분집합을 구한 후 `weight`보다 작은 값 중 최대값을 갱신시키는 방법으로 푼다.
3. `DFS` 의 인자를 2개로 설정한 다음 `weight` 값을 누적시키거나 누적시키지 않는 방법을 사용한다.

```javascript
let weight = 259;
let n = 5;
let arr = [81, 58, 42, 33, 61];

console.log(solution(weight, n, arr));

function solution(weight, n, arr){
  let answer = Number.MIN_SAFE_INTEGER;
  arr.sort((a,b)=>b-a);

  function DFS(L, sum){
    if (sum > weight) return;
    if (L === n){
      answer = Math.max(answer, sum)
    }else{
      DFS(L+1, sum+arr[L]);
      DFS(L+1, sum);
    }
  }
  DFS(0, 0);
  return answer;
}
```

---
## 📍 section08 - 7 - 최대점수 구하기(DFS)
제한시간 `M`안에 `N`개의 문제 중 최대점수를 얻을 수 있도록 구하는 문제다. 처음 문제를 봤을 때 <a href='https://ywtechit.tistory.com/302'>회의실 배정</a>문제와 비슷한 줄 알았는데, 그리디로는 풀 수 없었다. 점수를 높은 순으로 `정렬(sort)`한 다음 순서대로 풀면 제한시간안에 최대 점수를 얻을 수 있지 않나? 라고 생각했는데 그것보다, 모든 경우의 수(`부분집합`)를 구해서 `M`보다 작으면서 동시에 최대 점수를 갱신하면 되는 문제였다. 여기서 모든 경우의 수를 구하지 않고 `edgeCut(가지치기)`을 이용했는데 현재까지 누적된 시간이 `M`보다 크다면 더 이상 계산 할 필요 없이 `return`하는 코드를 추가했다. 종료조건은 `L===n`인데, 문제는 한 유형당 한 개씩만 풀 수 있기 때문에 하나씩 모두 사용했을 때 최대 `L(level)`은 `N`이 되기때문이다. 하단의 `DFS`의 그림을 참고하자. 모든 경우의 수를 그리진 않고, 이렇게 문제와 점수를 누적해간다는것을 표현했다.

![](https://images.velog.io/images/abcd8637/post/05f886c8-a3d4-446f-bd06-478f1522112f/KakaoTalk_Photo_2021-09-23-10-56-01.jpeg)

```javascript
let n = 5;
let m = 20;
let arr = [[10, 5], [25, 12], [15, 8], [6, 3], [7, 4]];

console.log(solution(n, m, arr));

function solution(n, m, arr){
  let answer=Number.MIN_SAFE_INTEGER;

  function DFS(L, sum, time){
    if (time > m) return;
    if (L === n){
      answer = Math.max(answer, sum);
    }else{
      DFS(L+1, sum+arr[L][0], time+arr[L][1]);
      DFS(L+1, sum, time);
    }
  }
  DFS(0, 0, 0);
  return answer;
}
```

---
## 📍 section08 - 8 - 중복순열 구하기
1부터 `N`까지 적힌 구슬이 있는데, 중복을 허락하여 `M`번을 뽑아 일렬로 나열하는 방법을 모두 출력하라.

```js
// 입력
3 2

// 출력
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
9
```

입력으로 주어진 중복순열의 모든 경우의 수는 `n*n` 즉, 9가 된다. 그런데, 이런 중복순열 문제는 다음과 같이 `for`문으로 풀면 더 간단하지 않을까?

```javascript
let n = 3;
let m = 2;

for (let i=1 ; i<=n; i++){
  for (let j=1; j<=n; j++){
    console.log(i, j)
  }
}

👉🏽
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

물론, 지금과 같은 입력에서는 답은 잘 나온다. 만약, `m`이 `3`일때(3개 중 3개를 뽑는 경우의 수)는 어떻게 구할까? 결론적으로 말하고 싶은것은 `m`이 늘어날 때마다 반복문의 개수도 늘어나야하는데, 일일이 `m`개씩 반복문을 작성하게 되면 상당히 비효율적인 코드가 된다. 코딩테스트처럼 입력이 여러개인 경우 이렇게 하드코딩을 할 수도 없다. 이럴때 재귀를 사용하여 `m`번 만큼 반복문을 돌면 편하게 구할 수 있다. `m`값이 바뀌면 `m`레벨만큼 재귀를 사용해 구하면 된다.

```javascript
// 하드코딩
let n = 3;
let m = 3;

for (let i=1 ; i<=n; i++){
  for (let j=1; j<=n; j++){
    for (let k=1; k<=n; k++){
      console.log(i, j, k)
    }
  }
}

👉🏽
1 1 1
1 1 2
1 1 3
1 2 1
1 2 2
1 2 3
1 3 1
1 3 2
1 3 3
2 1 1
2 1 2
2 1 3
2 2 1
2 2 2
2 2 3
2 3 1
2 3 2
2 3 3
3 1 1
3 1 2
3 1 3
3 2 1
3 2 2
3 2 3
3 3 1
3 3 2
3 3 3
```

재귀로 풀 때 주의할 점은 재귀로 돌고나서 나온 `arr`의 값이 마지막 값만 참조하므로 얕은복사(`slice`)를 이용해 `answer`에 `push`해주자.

```javascript
// 정답
let n = 3;
let m = 2;

console.log(solution(n, m));

function solution(n, m){
  let arr = Array.from({length: m}, () => 0);
  let cnt=0;
  let answer = [];
  function DFS(L){
    if (L === m){
      answer.push(arr.slice());
      cnt++;
    }else{
      for (let i=1; i<=n; i++){
        arr[L] = i;
        DFS(L+1)
      }   
    }
  }
  DFS(0)
  return [answer, cnt];
}
```

---
## 📍 section08 - 9 - 동전교환
다음과 같이 여러 단위의 동전들이 있을 때 거스름돈을 가장 적은 수의 동전으로 교환하려면 어떻게 할까? 각 단위의 동전은 무한정 쓸 수 있다.

```js
// 입력
3
1 2 5
15

// 출력
// (5, 5, 5) 동전 3개로 거슬러 줄 수 있다.
3
```

거스름돈 문제는 <a href='https://velog.io/@abcd8637/%EC%9D%B4%EA%B2%83%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8%EB%8B%A4-8%EC%9D%BC%EC%B0%A8'>그리디</a>로 풀어본적 있다. 하지만, 이 문제는 그리디로는 풀 수 없다. 왜냐하면 동전의 단위가 서로 배수 형태가 아니라 무작위로 주어진 경우기 때문이다. 이럴 땐 `DFS` 혹은 `DP`를 이용하면 된다. 만약, 동전이 `[500, 100, 50, 10]`처럼 배수형태로 나오면 그리디로 풀 수 있다. 또, 앞서 배운 <a href='https://ywtechit.tistory.com/310'>부분집합</a>으로는 이 문제를 풀 수 없는데, 왜냐하면 동전을 각 한번씩 쓰는것이 아니고 거스름돈이 더 이상 없어질 때까지 무한정으로 쓸 수 있기 때문이다. 그러나 동전의 개수가 커질수록 계산하는 가짓수도 늘어나기 때문에 `edgeCut`을 이용했는데, `11`, `12`번 라인처럼 조건을 걸어주면 연산횟수를 대폭 낮출 수 있다. 약간의 팁을 추가하자면 `coin`을 내림차순으로 정렬을 하고나서 `DFS`로 들어가는 것인데, 정렬하는데 시간이 조금 들더라도(`O(NlogN)`) 거스름돈은 동전의 큰 단위를 먼저 주는것이 횟수를 낮출 수 있기 때문이다.

거스름돈을 큰 단위부터 바꿔줄 때 재귀 흐름도는 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/4c3adf06-1626-472c-8f19-2a6bde2cb838/KakaoTalk_Photo_2021-09-26-08-03-19.jpeg)

```javascript
let n = 3;
let coin = [1, 2, 5];
let change = 15;

console.log(solution(n, coin, change));

function solution(n, coin, change) {
    let answer = Number.MAX_SAFE_INTEGER;
    coin.sort((a, b) => b - a);  // 거스름돈을 큰 단위부터 바꿔주면서 시간을 단축시킨다.

    function DFS(L, sum) {
        if (sum > change) return;    // change보다 sum이 크면 더 이상 계산 할 필요가 없음.
        if (answer <= L) return;    // answer보다 작은 값을 구해야하는데 L이 더 크면 가지치기를 더 이상 할 필요가 없음.
        if (sum === change) {
            answer = Math.min(answer, L);
        } else {
            for (let i = 0; i < n; i++) {
                DFS(L + 1, sum + coin[i]);
            }
        }
    }

    DFS(0, 0);
    return answer;
}
```

---
## 📍 section08 - 10 - 순열구하기
문제: 10이하의 `N`개의 자연수가 주어지면 이 중 `M`개를 뽑아 일렬로 나열하는 방법을 모두 출력하라.(중복은 허락하지 않는다.)
```js
// 입력
3 2
3 6 9

// 출력
3 6
3 9
6 3
6 9
9 3
9 6
```

<a href='https://ywtechit.tistory.com/314?category=958175'>이전</a>에 풀었던 중복을 허락하여 순열구하기와 비슷한 문제이지만 이번엔 중복을 허락하지 않는 조건에서 푸는 문제다. 중복을 허락하지 않았을 때 나올 수 있는 전체 경우의 수는 `3*2=6`이다. 코드 또한 비슷하지만, `visited` 배열을 선언하여 이전에 방문했던 `index`는 제외하고 방문하면 중복되지 않은 값이 나온다. 중요한 `point`는 방문하고 다시 올라갈 때 `visited`를 0으로 바꿔줘야 다음 `L`에서 `index`를 순서대로 방문한다는 점이다. `visited`를 0으로 바꿔주지 않으면 출력이 `[3, 6], [3, 9]`으로만 나온다.
마지막에 출력할 때는 `answer`에 얕은복사`slice`로 `push`했다.

![](https://images.velog.io/images/abcd8637/post/8ca46b17-bc60-48e9-ac32-3d06569ca3c3/KakaoTalk_Photo_2021-09-26-08-49-57.jpeg)

```javascript
let n = 3;
let m = 2;
let arr = [3, 6, 9];

console.log(solution(n, m, arr));

function solution(n, m, arr){
  let temp = Array.from({length: m}, ()=>0);
  let visited = Array.from({length: n}, ()=>0);
  let answer = [];

  function DFS(L){
    if (L === m){
      answer.push(temp.slice());
    }else{
      for (let i=0; i<n; i++){
        if (!visited[i]){
          visited[i] = 1  // 방문처리
          temp[L] = arr[i];
          DFS(L+1);
          visited[i] = 0  // 방문 후 다시 올라갈 때 원상복구
        }
      }
    }
  } 

  DFS(0)
  return answer;
}
```

---
## 📍 section08 - 11 - 팩토리얼
자연수 `N`이 주어지면 `N!` 값을 구하는 문제다. 재귀함수를 통해서 풀 수 있는데 종료조건은 `N`이 1일 때 `return 1`을 선언해주고, 나머지는 `return n * factorial(n-1)`을 해준다. 흐름은 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/f8902729-49a9-4e08-beb6-eb456b4cdf51/KakaoTalk_Photo_2021-09-27-11-54-01.jpeg)

```javascript
let n = 5;
console.log(solution(n));

function solution(n) {
    let answer;

    function factorial(n) {
        if (n === 1) return 1;
        else return n * factorial(n - 1);
    }

    answer = factorial(n);
    return answer;
}
```

---
## 📍 section08 - 12 - 조합의 경우수 (메모이제이션)
다음 공식을 사용하여 재귀를 이용해 조합수를 구하는 프로그램을 작성하세요. 

![](https://images.velog.io/images/abcd8637/post/34ce387e-5e20-4223-be49-cb878d34541a/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-28%2010.25.44.png)

조합의 경우의 수를 구하는 문제는 `n`의 범위가 `20`정도 넘으면 메모이제이션으로 풀어야 한다. 왜냐하면 연산시간이 오래걸리기 때문이다. 메모이제이션을 하는 이유는 동일한 계산을 반복하지 않기 위함인데, 이전에 한창 지식인 <a href='https://kin.naver.com/qna/detail.nhn?d1id=1&dirId=10402&docId=381493087&page=1#answer3'>답변</a> 활동을 했을 때 피보나치 수열의 합계를 구하는 질문에서 답했었다. 문제에 주어진 공식으로 풀 때 메모이제이션을 적용하는 이유도 마찬가지다. 그런데 기존에 알던 공식을 사용해도 되는데 새로운 공식을 사용하는 이유는 뭘까?(이 공식을 나는 처음봤다 😅 😅) 예를 들어 `5[1, 2, 3, 4, 5]개` 중 3개를 뽑는 경우의 수`(5C3)`를 구한다고 했을 때 다음과 같이 풀 수 있다. 

1. 자신은 현재 뽑는 값에 포함하고, 나머지 값에서 `r-1`개를 뽑는 방법(이미 내가 뽑혔으니 나머지 2개를 뽑아야 한다.)
2. 자신은 현재 뽑는 값에 제외시키고, 나머지 값에서 `r`개를 뽑는 방법(나는 안 뽑힌다고 가정하고 나머지 값들 중에서 3개를 뽑는다.)

이렇게 재귀적으로 쭉 이어서 나가는데, 종료조건은 `n===r || r===0`일 때 `1`을 리턴한다. `n`과 `r`이 같다면 숫자에 상관없이 `1` 이고(`1C1=1`) `r`이 0이면 `1`(`1C0=1`)이기 때문이다. 메모이제이션으로 풀 때는 2차원 배열을 선언하는데 다음과 같이 저장된다. (코드에서는 `memo` 변수에 할당)

![](https://images.velog.io/images/abcd8637/post/6a411c9a-d6f2-4748-beae-5ef855e6e4eb/KakaoTalk_Photo_2021-09-27-11-54-06.jpeg)

문제의 흐름을 그림으로 그렸다.

![](https://images.velog.io/images/abcd8637/post/5f57e296-379d-4e4f-8c69-35b11ee785c8/KakaoTalk_Photo_2021-09-28-10-33-11.jpeg)

코드는 다음과 같다. 

```javascript
let n = 5;
let r = 3;

console.log(solution(n, r));

function solution(n, r){
  let answer;
  let memo = Array.from(Array(35), () => Array(35).fill(0));

  function DFS(n, r){ 
    if (memo[n][r]) return memo[n][r];
    if (n === r || r === 0) return 1;
    else return memo[n][r] = DFS(n-1, r-1) + DFS(n-1, r);
  }

  answer = DFS(n, r);
  return answer;
}
```

여담으로 `memoization`을 사용했을 때와 사용하지 않았을 때의 실행시간을 비교했는데 `memo`를 사용할때는 `0.003초`, `memo`를 사용하지 않았을 때는 `3.3초`가 걸렸다.

![](https://images.velog.io/images/abcd8637/post/1363a2be-3df6-446d-b4fa-b0253160beeb/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-28%2010.45.36.png)

```javascript
let n = 33;
let r = 19;

// 메모이제이션 사용 코드
let memo = Array.from(Array(35), ()=> (Array(35).fill(0)));

function DFS(n, r){
  if (memo[n][r]) return memo[n][r];
  if (n === r || r === 1) return 1;
  else return memo[n][r] = DFS1(n-1, r-1) + DFS1(n-1, r); 
}

console.log(DFS(n,r));
👉🏽 471435600

// 메모이제이션 미사용 코드
function DFS(n, r){
    if (n === r || r === 1) return 1;
    else return DFS(n-1, r-1) + DFS(n-1, r); 
  }

console.log(DFS(n, r));
👉🏽 471435600
```

---
## 📍 section08 - 13 - 수열 추측하기
문제는 다음과 같다. 가장 윗줄에 1부터 `N`까지의 숫자가 한 개씩 적혀 있다. 파스칼의 삼각형을 예로 들어 `N`이 4이고 가장 윗 줄에 `3 1 2 4`가 있다고 할 때 다음 그림과 같이 그려진다.

![](https://images.velog.io/images/abcd8637/post/dd386a50-2f60-40a7-951a-56167980a020/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-28%2011.01.07.png)

`N`과 가장 밑에 있는 숫자가 주여져 있을 때 가장 윗줄에 있는 숫자를 구하는 프로그램을 작성하시오. 여러가지 답이 나오면 사전순으로 가장 앞에 오는것을 출력한다.
```
// 입력
4 16

// 출력
3 1 2 4
```

문제만 봐서는 조금 어렵다고 생각했는데, 어떻게 풀어야 할지 순서를 나누니까 괜찮았다. 여기서 파스칼의 삼각형 공식을 알아야하는데, 조합이 사용된다. 예를 들어 `1 2 3 4`가 주어진다고 할 때 모든 수를 차례로 더하면 다음과 같은 결과가 나온다.

![](https://images.velog.io/images/abcd8637/post/a86a0cdc-0d71-4997-8701-a1621b811aae/KakaoTalk_Photo_2021-09-28-11-09-10.jpeg)

사진 제일 하단에 있는 `1+2+2+2+3+3+3+4`의 값을 자세히 살펴보니 1은 `1번`, 2는 `3번`, 3은 `3번`, 4는 `1번`이 사용됐다. 입력이 `1 2 3 4`가 아니어도 4개의 숫자를 방금처럼 구하면 사용된 갯수는 `1 3 3 1`로 동일하다. 5개의 숫자는 `1 4 6 4 1`번씩 쓰인다. 이를 조합으로 나타낼 수 있는데, `1 3 3 1`은 `3C0, 3C1, 3C2, 3C3`으로 나타낼 수 있고 `n`개 일때는 `n-1C0, n-1C1, ..., n-1Cn-2, n-1Cn-1`으로 나타낼 수 있다. 다시 문제로 돌아가서 파스칼 삼각형에서 가장 윗줄에 있는 숫자를 맞춰야 하는데, 정확하게 어떤 수가 `target`과 동일한지 모르니까 1부터 `N`까지 일렬로 나열하는 모든 경우의 수(중복을 허락하지 않는 순열, 여기서는 `4*3*2*1=24`)를 찾고 해당 수를 파스칼의 공식 `1 3 3 1`을 이용하여 하나씩 곱해서 모두 더한 값이 `target`과 같은지 확인하면 된다. 중복을 허락하지 않는 순열은 `visited` 배열을 사용하여 체크해주면 된다. 순열을 구하는 방법을 잘 모르겠다면 <a href='https://ywtechit.tistory.com/316'>다음</a>을 참고하자. 내가 풀었을 때는 조합(1 3 3 1)을 한번에 구해놓고 종료조건에 도달했을 때 `index`끼리 곱했는데 선생님은 아예 `DFS` 함수 인자에 `sum`을 넣어 재귀를 계산할 때마다 더하는 방법을 사용했다. 이렇게 계산하면 전자보다 연산속도가 빨라지는 장점이 있다.

1. 1부터 `N`까지 중복을 허락하지 않고 일렬로 나열하는 방법(중복을 허락하지 않는 순열)을 구한다.
2. `n-1C0 ~ n-1Cn-1`까지 경우의 수를 구한다.(이때, 연산속도를 낮추기 위해 메모이제이션을 사용)
3. 1번에서 구한 값을 각각의 `index`에 맞게 2번 값을 곱한다. (DFS함수의 인자로 넘겨 재귀가 뻗어나갈 때마다 계산한다.)
4. 3번에서 구한 값을 모두 더해 `target`과 같은 값인지 확인한다.
5. 처음으로 결과가 되는 값을 출력한다. (`flag=true`로 바꿔 그 다음 불 필요한 연산을 줄인다.)

```javascript
let n = 4;
let target = 16;

console.log(solution(n, target));

function solution(n, target){
  let memo = Array.from(Array(11), () => Array(11).fill(0));
  let visited = Array.from({length: n+1}, () => 0);
  let arr = Array.from({length: n}, () => 0);
  let combi = Array.from({length: n}, () => 0);
  let answer;
  
  function pascal(n, r){
    if (memo[n][r]) return memo[n][r];
    if (n===r || r===0) return 1;
    else return memo[n][r] = pascal(n-1, r-1) + pascal(n-1, r);
  }

  for (let i=0; i<n; i++) combi[i] = pascal(n-1, i);

  let flag = false;

  function DFS(L, sum){
    if (flag) return;
    if (L === n && sum === target){
      answer = arr.slice();
      flag = true;
    }else{
      for (let i=1; i<=n; i++){
        if (visited[i] === 0){
          visited[i] = 1;
          arr[L] = i;
          DFS(L+1, sum+(arr[L]*combi[L]));
          visited[i]=0;
        }
      }
    }
  }
  
  DFS(0, 0)
  return answer;
}
👉🏽 3 1 2 4
```

---
## 📍 section08 - 14 - 조합 구하기
1부터 `N`까지 번호가 적힌 구슬이 있다. 이 중 `M`개를 뽑는 방법의 수를 출력하는 프로그램을 작성하세요

```js
// 입력
4 2

// 출력
1 2
1 3
1 4
2 3
2 4
3 4
6
```

조합을 구하는 문제인데, 이전에 배웠던 순열과는 조금 다른방식으로 풀어야 한다. 중복을 허용하지 않는 순열을 구현할 때 배웠던 것처럼 `visited` 배열로 재귀가 돌아올 때 `visited[i]=0`을 해주는 방법으로는 풀 수 없고 대신 반복문의 `i`값을 조금 다르게 `i+1`을 계속 넘겨줘야 한다. `arr`값이 따로 주어져있으면 `i`는 0부터 시작하는데, 이 문제는 `arr`이 주어져 있지않고 현재 인덱스가 값으로 들어가므로 `s` 인자는 1로 초기화하여 넘긴다.

![](https://images.velog.io/images/abcd8637/post/7e317436-777c-46f9-a960-a969f691421f/KakaoTalk_Photo_2021-09-28-09-49-45.jpeg)

```javascript
let n = 4;
let m = 2;

console.log(solution(n, m));

function solution(n, m){
  let arr = Array.from({length: m}, () => 0);
  let answer = [];

  function DFS(L, S){
    if (L === m){
      answer.push(arr.slice());
    }else{  
      for (let i=S; i<=n; i++){
        arr[L] = i;
        DFS(L+1, i+1);
      }
    }
  }

  DFS(0, 1);
  return answer;
}

👉🏽 [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ], [ 2, 3 ], [ 2, 4 ], [ 3, 4 ] ]
```

---
## 📍 section09 - 1 - 그래프와 인접행렬
이번 섹션은 `그래프와 탐색(DFS, BFS)`에 대해서 배운다. 지금은 문제를 풀지 않고 그래프에 대해 간단하게 알아보는 시간을 가져보자.

그래프는 다음과 같이 이루어진다. 
1. Vertex: 정점, 노드
2. Edge: 노드와 노드를 연결하는 간선
3. graph: 2차원 배열에서는 `index`가 정점(vertex)번호다.

그래프의 종류는 3가지가 있다. 입력이 주어질 때 `graph`별로 어떻게 입력하는지 코드로 나타냈다. (여기서는 인접행렬로 표현함)

1. 무방향 그래프(unDirected Graph): 방향이 없는 그래프 즉, 양방향인 그래프다. 입력은 보통 `[a, b]` 형태로 주어지는데 여기서 `graph[a][b]=1, graph[b][a]=1`을 모두 수행한다.

![](https://images.velog.io/images/abcd8637/post/7e9cf708-c704-4492-a71f-1f4e50e83674/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-29%2007.55.11.png)

```javascript
// 인접행렬
let node = 5;
let edge = 5;

console.log(unDirectedGraph(node, edge));

function unDirectedGraph(node, edge){
  let graph = Array.from(Array(node+1), () => Array(edge+1).fill(0));
  let input = [[1, 2], [1, 3], [2, 4], [3, 4], [2, 5]];
  
  for (let [a, b] of input){
    graph[a][b] = 1;
    graph[b][a] = 1;
  }

  return graph;
}

👉🏽 [
  [ 0, 0, 0, 0, 0, 0 ],
  [ 0, 0, 1, 1, 0, 0 ],
  [ 0, 1, 0, 0, 1, 1 ],
  [ 0, 1, 0, 0, 1, 0 ],
  [ 0, 0, 1, 1, 0, 0 ],
  [ 0, 0, 1, 0, 0, 0 ]
]
```


2. 방향 그래프(directed Graph): 방향이 정해져 있는 그래프다. 무방향 그래프와는 달리 정점이 가리키는 방향만 `graph`에 입력한다.

![](https://images.velog.io/images/abcd8637/post/2ccd11c0-ec7b-492d-8859-abc6ac25045b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-09-29%2007.59.00.png)

```javascript
// 인접행렬
console.log(directedGraph(node, edge));

function directedGraph(node, edge){
  let graph = Array.from(Array(node+1), () => Array(edge+1).fill(0));
  let input = [[1, 2], [1, 3], [2, 4], [3, 4], [2, 5]];
  
  for (let [a, b] of input){
    graph[a][b] = 1;
  }

  return graph;
}

👉🏽 [
  [ 0, 0, 0, 0, 0, 0 ],
  [ 0, 0, 1, 1, 0, 0 ],
  [ 0, 0, 0, 0, 1, 1 ],
  [ 0, 0, 0, 0, 1, 0 ],
  [ 0, 0, 0, 0, 0, 0 ],
  [ 0, 0, 0, 0, 0, 0 ]
]
```

3. 가중치 방향그래프(weighted directed Graph): 방향그래프이면서 가중치도 같이 나타낸 그래프이다. 한 도시에서 다른 도시로 이동할 때 드는 비용과 같은 문제에서 등장한다. 입력을 `a, b, c`로 받아 `graph[a][b]=c` 처럼 비용까지 같이 `graph`에 입력해야한다.

![](https://images.velog.io/images/abcd8637/post/d978f470-d4e8-40b7-8374-0f7858f8993e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-10-06%2011.44.21.png)

```javascript
// 인접행렬
console.log(weightedDirectedGraph(node, edge));

function weightedDirectedGraph(node, edge){
  let graph = Array.from(Array(node+1), () => Array(edge+1).fill(0));
  let input = [[1, 2, 2], [2, 5, 5], [3, 4, 5], [1, 3, 4], [4, 2, 2]];
  
  for (let [a, b, c] of input){
    graph[a][b] = c;
  }

  return graph;
}

👉🏽 [
  [ 0, 0, 0, 0, 0, 0 ],
  [ 0, 0, 2, 4, 0, 0 ],
  [ 0, 0, 0, 0, 0, 5 ],
  [ 0, 0, 0, 0, 5, 0 ],
  [ 0, 0, 2, 0, 0, 0 ],
  [ 0, 0, 0, 0, 0, 0 ]
]
```

위에서는 인접행렬로 나타냈는데, 그래프의 값을 나타낼때는 인접행렬과 인접리스트의 방식이 있다. 각각의 특징은 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/26658153-61cf-4a03-8722-04a290979fe1/KakaoTalk_Photo_2021-09-30-09-13-03.jpeg)

1. 인접행렬(adjacency-matrix): 노드와 간선의 정보를 행렬로 표현하는 방법, 간선의 갯수와 상관없이 모든 정점을 표현해야하기 때문에 정점의 갯수가 많을수록 메모리 사용량이 줄어든다. 가중치를 방향그래프는 인접행렬로 나타낸다. 무방향, 방향성그래프 문제를 풀 때 정점의 갯수가 `10,000` 이하라면 인접행렬로 풀자.

```javascript
// graph에 값을 입력하는 방법
let n = 5;
let m = 9;
let arr = [[1, 2], [1, 3], [1, 4], [2, 1], [2, 3], [2, 5], [3, 4], [4, 2], [4, 5]];
let graph = Array.from(Array(n+1), () => Array(n+1).fill(0));

// 무방향 그래프
for (let [a, b] of arr){
	graph[a][b]=1;
	graph[b][a]=1;
}

// 방향 그래프
for (let [a, b] of arr){
	graph[a][b]=1;
}

// 가중치 방향 그래프
let graph = [[1, 2, 2], [2, 5, 5], [3, 4, 5], [1, 3, 4], [4, 2, 2]];

for (let [a, b, c] of arr){
	graph[a][b]=c;
}
```
   
2. 인접리스트(adjacency-list): 노드와 간선의 정보를 리스트 형태로 표현하는 방법, 연결된 간선만 표시하기 때문에 인접행렬보다 비교적 간단하다. 정점의 순서는 꼭 오름차순이 아니어도 상관없다. 인접리스트로 문제를 풀 때는 정점의 갯수만큼 반복문을 돌리는것이 아니라 간선의 갯수 `graph[v].length` 만큼 반복문을 돌려야 실행속도를 높일 수 있다. 인접리스트에 있는 정점은 필수로 한번씩 들려야하는 정점이므로 (왜냐하면 이미 연결되어있는 정점만 표시하기 때문) 조건문에 `graph[v][i]`로 값을 확인하는 대신 `visited` 여부만 확인해주면 된다. 정점의 갯수가 `10,000` 이상일때는 인접리스트를 사용하자.

```javascript
// graph에 값을 입력하는 방법
let n = 5;
let m = 9;
let arr = [[1, 2], [1, 3], [1, 4], [2, 1], [2, 3], [2, 5], [3, 4], [4, 2], [4, 5]];
let graph = Array.from(Array(n+1), () => Array());

// 방향 그래프
for (let [a, b] of arr){
	graph[a].push(b);
}

console.log(graph)
👉🏽 [ [], [ 2, 3, 4 ], [ 1, 3, 5 ], [ 4 ], [ 2, 5 ], [] ]
```

---
## 📍 section09 - 2 - 경로 탐색(인접행렬)
방향그래프가 주어지면 1번 정점에서 `N`번 정점으로 가는 모든 경로의 가지 수를 출력하는 프로그램을 작성하는 문제다. 예를 들어 1번 정점에서 5번 정점으로 가는 가지 수는 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/56e32c7e-850d-4d12-937b-eeae6dc8a3d4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-10-06%2011.54.32.png)

```
1 2 3 4 5
1 2 5
1 3 4 2 5
1 3 4 5
1 4 2 5
1 4 5
```

이 문제는 `DFS`를 이용해서 풀 수 있다. 경로의 가짓수만 출력하는 것이 아니라 올바르게 이동했는지 알기위해 `path` 변수를 추가했다.

1. 2차원 배열의 `graph`를 선언하여 정점과 간선의 정보를 넣는다.
2. `visited` 배열을 선언하여 이미 지나온 곳은 건너뛰고 진행한다.
3. `DFS`의 종료조건은 `v`가 `n`과 같을 때이다.
4. 인접행렬이므로 반복문으로 모든 정점을 탐색해야한다.
5. `DFS` 함수를 돌리기 전 1번 정점에서 시작하므로 `visited[1]=1`을 선언한다. 그렇지 않으면 1번 정점에 중복 방문한다.

![](https://images.velog.io/images/abcd8637/post/f9ccdfa2-5bc2-4751-ba11-357bf9d05ec3/KakaoTalk_Photo_2021-10-06-09-59-13.jpeg)

```javascript
let n = 5;
let m = 9;
let arr = [
    [1, 2],
    [1, 3],
    [1, 4],
    [2, 1],
    [2, 3],
    [2, 5],
    [3, 4],
    [4, 2],
    [4, 5],
];

console.log(solution(n, m, arr));

function solution(n, m, arr){
  let visited = Array.from({length: n+1});
  let graph = Array.from(Array(n+1), () => Array(n+1).fill(0));
  let path = []
  let cnt=0;

  for (let [a, b] of arr) graph[a][b] = 1;  // graph에 값 넣기

  function DFS(v){
    if (v === n){
      console.log(path);  // 경로 출력
      cnt++;  // 경로의 가짓 수 출력
    }else{
      for (let i=1; i<=n; i++){
        if (!visited[i] && graph[v][i]){
          visited[i] = 1;
          path.push(i)
          DFS(i);
          visited[i] = 0;
          path.pop()
        }
      }
    }
  }

  path.push(1);
  visited[1]=1;
  DFS(1);
  return cnt;
}

👉🏽
[ 1, 2, 3, 4, 5 ]
[ 1, 2, 5 ]
[ 1, 3, 4, 2, 5 ]
[ 1, 3, 4, 5 ]
[ 1, 4, 2, 5 ]
[ 1, 4, 5 ]
6
```

---
## 📍 section09 - 3 - 경로 탐색(인접리스트)
방향그래프가 주어지면 1번 정점에서 `N`번 정점으로 가는 모든 경로의 가지 수를 출력하는 프로그램을 작성하는 문제다. 예를 들어 1번 정점에서 5번 정점으로 가는 가지 수는 다음과 같다.

![](https://images.velog.io/images/abcd8637/post/56e32c7e-850d-4d12-937b-eeae6dc8a3d4/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-10-06%2011.54.32.png)

```
1 2 3 4 5
1 2 5
1 3 4 2 5
1 3 4 5
1 4 2 5
1 4 5
```

이전과 동일한 문제지만 이번에는 인접리스트를 활용해서 푸는 문제다. 만약에 그래프를 이용한 문제에서 정점의 개수가 `10,000`개 이상이라면 인접리스트를 사용하자.(인접 행렬은 정점의 개수만큼 반복문을 돌아야하기 때문에 비효율적이다.) 이 문제도 마찬가지로 `DFS`를 이용해서 풀 수 있다. 경로의 가짓수만 출력하는 것이 아니라 올바르게 이동했는지 알기위해 `path` 변수를 추가했다.

1. 인접리스트의 반복문의 범위는 `graph[v].length`까지
2. 인접행렬처럼 정점끼리 연결되어 있는지 확인하는 작업(`graph[v][i]===1`)이 필요없다. 왜냐하면 인접리스트는 정점끼리 이미 연결된 값만 넣기 때문이다. 대신 `visited` 배열로 방문했는지 여부만 조건에 걸어주면 된다.
3. 다음 DFS함수를 실행할 때는 `DFS(graph[v][i])`를 넣어줘야 한다.

![](https://images.velog.io/images/abcd8637/post/6b8c4443-645c-40af-8841-b736771f137a/KakaoTalk_Photo_2021-10-06-10-26-05.jpeg)

```javascript
let n = 5;
let m = 9;
let arr = [
    [1, 2],
    [1, 3],
    [1, 4],
    [2, 1],
    [2, 3],
    [2, 5],
    [3, 4],
    [4, 2],
    [4, 5],
];

console.log(solution(n, m, arr));

function solution(n, m, arr){
  let graph = Array.from(Array(n+1), () => Array());
  let visited = Array.from({length: n+1}, () => 0);
  let cnt=0;
  let path=[];

  for (let [a, b] of arr) graph[a].push(b);  // 인접 리스트 만들기

  function dfs(v){
    if (v === n){
      console.log(path);
      cnt++;
    }else{
      for (let i=0; i<graph[v].length; i++){
        if (!visited[graph[v][i]]){
          visited[graph[v][i]]=1;
          path.push(graph[v][i])
          dfs(graph[v][i]);
          visited[graph[v][i]]=0;
          path.pop()
        }
      }
    }
  }

  path.push(1);
  visited[1]=1;
  dfs(1);
  return cnt;
}

👉🏽
[ 1, 2, 3, 4, 5 ]
[ 1, 2, 5 ]
[ 1, 3, 4, 2, 5 ]
[ 1, 3, 4, 5 ]
[ 1, 4, 2, 5 ]
[ 1, 4, 5 ]
6
```

