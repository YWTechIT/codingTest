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