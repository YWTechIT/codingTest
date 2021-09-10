## 💡 implementation_tips

---
## 📍 number 타입 값을 배열에 거꾸로 넣기
`number`의 값을 거꾸로 집어 넣을 때 `reverse` 함수를 사용하여 넘길 수도 있지만, 숫자의 특성을 이용해서 넣을 수도 있다.

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
`for`문을 돌고나서 i값이 각각 `0`, `0`, `2`, `0`, `8`일때 이것의 순서를 유지한 상태로 모두 합쳐 자연수로 바꾸어 뒤집으면 `208`이 될 것이다. 이때 `parseInt`, `number` 함수를 사용하지 않고 답안과 같이 구현 할 때는 다음과 같은 방법으로 생각하자.

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

---
## 📍 string함수 사용하지 않고 자연수 거꾸로 뒤집기
```javascript
let n = 23;
let sum = 0;

// do - while문
do{
    sum = sum * 10 + n % 10;
    n = Math.floor(n / 10);
}while(n);

console.log(sum)
👉🏽 32

// while문
while(n){
    sum = sum * 10 + n % 10;
    n = Math.floor(n/10);
}
```

---
## 📍 2차원 행렬 sort
2차원 행렬 각각의 두 값을 더해서 오름차순으로 `sort` 하고 싶을 때

```javascript
let arr = [[6, 6], [2, 2], [4, 3], [4, 5], [10, 3]];

arr.sort((a, b) => (a[0]+a[1]) - (b[0]+b[1]));

console.log(arr);
👉🏽 [ [ 2, 2 ], [ 4, 3 ], [ 4, 5 ], [ 6, 6 ], [ 10, 3 ] ]
```

---
## 📍 배열 중간에 있는 값을 맨 앞으로 옮기기
배열 중간에 있는 값을 맨 앞으로 옮길때는 2가지의 방법이 있다. 한번 코드로 살펴보자.

1. `temp`로 `target`을 빼내는 방법: `target`이 몇 번째 `index`에 있는지 찾는다. -> `temp`에 저장한다. -> 한 칸씩 뒤로 미룬다. -> 맨 앞에 `temp`값을 넣는다.
2. `splice`방법: `target`이 몇 번째 `index`에 있는지 착는다 -> `temp`변수에 `splice` 값을 넣는다. -> 맨 앞에 `unshift()`한다.

```javascript
let arr = [2, 3, 1, 5, 6];
let target = 1;

// target이 arr의 몇 번째 idx에 위치해있는지 찾기
let pos=-1;
for (let i=0; i<=arr.length; i++){
    if(arr[i]===target) pos=i;}

// 1번: pos부터 한 칸씩 뒤로 밀기
let temp = arr[pos];
for (let i=pos; i>=1; i--){
    arr[pos] = arr[i-1];
}
arr[0] = temp;

console.log(arr)
👉🏽 [ 1, 3, 2, 5, 6 ]

// 2번: splice
let temp = arr.splice(pos, 1);
arr.unshift(...temp);

console.log(arr)
👉🏽 [ 1, 3, 2, 5, 6 ]
```

---
## 📍 누적 값이 point보다 높은지 낮은지 비교하고 추가하기
제목은 거창하게 작성했지만, 내용은 쉬운 글이다. 이진탐색의 결정 알고리즘 문제를 풀면서 작은 `skill(?)`을 남겨 놓고 싶어 작성했다. 예를 들어, 현재까지 누적된 `sum=6`이고, 다음 `x`값을 누적할 때 `point`보다 높으면 `continue`하고, 높지 않으면 포함시키는 방법을 작성하고 싶다면 어떻게 작성할까? 다음과 같이 작성할 수 있다.

```javascript
let arr = [1, 3, 2, 5, 1, 1, 1];
let point = 10;
let sum=0;

for (let x of arr){
    if(sum+x>point)continue
    else sum+=x;
}
```

이전질문에서 조금 변형됐지만 `currentTime`에 `songTime`값을 누적할 때 만약, 다음 `songTime`값이 `point`를 넘으면 새로운 `DVD`로 녹음 한다고 할 때 `DVD`는 총 몇개가 필요할까?의 질문에는 다음과 같이 작성 할 수 있다. 중요한점은 9번째 코드의 `currentTime`을 `0`으로 초기화시키는것이 아닌 현재 `song`으로 초기화 시켜야 다음 `song`을 누적할 수 있다.

```javascript
let songs = [1, 3, 2, 5, 1, 1, 1];
let point = 10;
let currentTime=0;
let DVD=0;

for (let song of songs){
    if(currentTime+song>point){
        DVD++;
        currentTime=song;
    }
    else currentTime+=song
}

console.log(DVD)
👉🏽 3
```