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