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







