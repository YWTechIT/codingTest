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









