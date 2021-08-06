## 📍 백준 1075 - 나누기
<a href='https://www.acmicpc.net/problem/1075'>백준 1075 - 나누기</a>

## 💡 나의 풀이
뒤 두자리를 가능하면 작게 만들려고 한다는 문장에서 `while`문을 사용하여 `1씩` 증가하면서 나누어 떨어지는지 확인하는 로직을 생각했다. 처음 `number`을 초기화 할 때 형을 `string` => `number`로 바꾸는 불 필요한 연산때문에 코드가 괜히 길어보였고 곰곰이 생각해보니까 `number`형으로만 계산해도 됐었다.

`number`은 다음과 같은 방법으로도 초기화 할 수 있다.
1. `let number = +((("" + n/100) | 0) + "00");` // 불 필요한 연산이 많은 코드
2. `let number2 = parseInt(n/100) * 100`  // 가독성이 좋아진 코드

```javascript
// 나의 코드
const fs = require("fs");
const filePath = process.platform === "linux" ? "/dev/stdin" : "./input.txt";
let input = fs.readFileSync(filePath).toString().split("\n");

input = input.map((item) => +item);
solution(input[0], input[1]);

function solution(n, f, answer = 0) {
  let number = ((n/100) | 0) * 100;

  while (true) {
    if (number % f == 0) {
      answer = number;
      break;
    } else {
      number += 1;
    }
  }
  console.log(("" + answer).slice(-2));
}
```

## 📍 백준 2525 - 오븐시계
<a href='https://www.acmicpc.net/problem/2525'>백준 2525 - 오븐시계</a>

## 💡 나의 풀이
현재 시간에서 조리시간만큼 지나면 몇시 몇분이 되는지 구하는 문젠데, 너무 어렵게 풀었다. 다른사람의 코드를 보니까 거의 50% 짧게 써서 놀라웠다.

나는 이렇게 풀었다.
1. 조리에 걸리는시간(`cookTime`)을 60으로 나눈 몫(`/`)은 현재시간(`curHour`)에 더하고, 나머지(`%`)는 현재분(`curMin`)에 더한다.
2. `while`문을 사용하여 현재 시간이 `24`보다 작고 현재분이 `60`보다 작을 때 `while` 문을 탈출하도록 설정했다.
3. 시간, 분 조건을 따로따로 걸어줬다.

그런데 이렇게 안해도, 매 계산마다 `hour`를 비교 할 필요없이 `while`문에 `min`만 넣으면 쉽게 풀 수있다. 즉, `min`이 60보다 작을 때 반복문을 탈출하게 만들고, `min`이 60과 같거나 크다면 `hour += 1, min -= 60`을 해준다. 반복문을 탈출했다면 `hour`은 23보다 클 수 없으므로 `hour %= 24`의 식을 넣어준다. 이렇게 하면 코드를 반으로 줄일 수 있다. 시간문제는 이렇게 풀어야한다는 흐름을 기억하고 있어야겠다.

```javascript
// 나의 코드
const fs = require("fs");
const filePath = process.platform === "linux" ? "/dev/stdin" : "./input.txt";
let input = fs.readFileSync(filePath).toString().split("\n");

let curHour = input[0].split(" ")[0];
let curMin = input[0].split(" ")[1];
let cookTime = input[1];

solution(+curHour, +curMin, +cookTime);

function solution(doneHour, doneMin, cookTime) {
  doneHour += parseInt(cookTime / 60);
  doneMin += cookTime % 60;

  while (true) {
    if (doneHour < 24 && doneMin < 60) {
      break;
    }

    if (doneHour >= 24) {
      doneHour -= 24;
    } else {
      doneMin -= 60;
      doneHour += 1;
    }
  }
  console.log(doneHour, doneMin);
}
```

```javascript
// 최적화 코드
const fs = require("fs");
const filePath = process.platform === "linux" ? "/dev/stdin" : "./input.txt";
let input = fs.readFileSync(filePath).toString().split("\n");

let curHour = input[0].split(" ")[0];
let curMin = input[0].split(" ")[1];
let cookTime = input[1];

solution(+curHour, +curMin, +cookTime);

function solution(doneHour, doneMin, cookTime) {
    doneMin += cookTime;
    
    while (doneMin >= 60){
        doneMin -= 60;
        doneHour += 1;
    }

    doneHour %= 24;
    console.log(doneHour, doneMin);
}
```

