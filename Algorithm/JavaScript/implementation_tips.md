## 💡 implementation_tips

---
## 📍 number 타입 값을 배열에 거꾸로 넣기

```javascript
// 문자열
let number = 12345;
let reverseArr = (""+number).split('').reverse().map((item) => +item);

// 숫자
let number = 12345;
let arr = [];

do {
    arr.push(number%10);
    number = Math.floor(number/10);
} while(number > 0);

👉🏽 [5, 4, 3, 2, 1]  // 결과는 동일
```

---
## 📍 number 함수를 사용하지 않고 값 누적하기
`for`문을 돌고나서 i값이 각각 `0`, `0`, `2`, `0`, `8`일때 이것의 순서를 유지한 상태로 모두 합쳐 자연수로 바꾸면 `208`이 될 것이다. 이때 `parseInt`, `number` 함수를 사용하지 않고 답안과 같이 구현해라.

```javascript
let s = "208";
let answer = 0;

for (let x of s){
    answer = answer*10 + (+x);
}
console.log(answer);
👉🏽 208
```

---
## 📍 자연수의 자릿수 합 구하기
`while`문을 사용하여 `x` 변수 사용시 `x`의 원래 값이 바뀌지 않게 하기위해 임시변수 `temp = x`를 선언한다.

```javascript
let arr = [128, 460, 603, 40, 521, 137, 999];

for (let x of arr){
    let sum = 0;
    let temp = x;

    while(x){
        sum += x % 10;
        x = Math.floor(x / 10);
    }
    console.log(sum)
    👉🏽 11 10 9 4 8 11 27 
}
```