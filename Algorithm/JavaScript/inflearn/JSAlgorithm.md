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