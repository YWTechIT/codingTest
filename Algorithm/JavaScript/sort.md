## 📍 프로그래머스 1단계 - K번째 수
<a href='https://programmers.co.kr/learn/courses/30/lessons/42748'>프로그래머스 1단계 - K번째 수</a>

### ⚡️ 나의 풀이

`JS`로는 처음 풀어본 문제인데, 나는 단순 `for`문으로 풀었지만 `for ~ of`로 풀면 조금 더 깔끔하게 풀 수 있었다.

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