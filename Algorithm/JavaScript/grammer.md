## 📍 var, let, const 변수 차이점과 호이스팅(hoisting), TDZ(Temporal Dead Zone), 스코프

일반적으로 `var` , `let` , `const` 라고 할 때의 기본적인 차이점은 대략적으로나마 알고있을 것이다. (어렴풋이 작성한 <a href='https://blog.naver.com/abcd8637/222115190399'>나의 글</a>) 간략하게 말하면 `var` 와 `let` 은 변수를 선언하고 변수를 할당한 이후에도 값을 변경할 수 있지만(정확히는 `var` 는 재선언 및 재할당이 가능하고, `let` 은 재선언은 불가능하지만 재할당은 가능하다.) `const`는 한번 할당한 값은 다시 바꿀 수 없다.

이러한 `var` 변수의 뛰어난 유연성만큼 단점도 있는데,`var` 문법은 스코프의 범위(정확하게는 함수 스코프)가 넓어서 의도치 않은 버그의 발생원인이 될 수 있기 때문에 이를 해결하기 위해 `ES6` 문법에  `let`, `const` 문법이 추가되면서 `var` 대신 `let`, `const` 사용을 권장하고 있다. 

그렇다면 `변수`와 `스코프`의 범위는 어떤 관계가 있을까? 이를 알기위해서는 `JS` 의 기본특성인 `호이스팅(hoisting)`을 알아야 하는데, <a href='https://developer.mozilla.org/ko/docs/Glossary/Hoisting'>호이스팅</a>이란 변수 및 함수 선언이 물리적으로 작성한 코드의 상단으로 옮겨지는 것이지만, 실제로는 그렇지 않은것을 말한다. `JS` 에서는 함수 선언을 메모리에 저장하는 방식을 채택하는데 이것의 장점은 코드에서 선언하기 전에 함수를 사용할 수 있는것이다. 다음의 예를 보자.

```jsx
printMyname("안영우")

function printMyName(name){
	console.log(`제 이름은 ${name}입니다.`)
}

👉🏽 제 이름은 안영우입니다.
```

이처럼 `printMyName` 함수를 선언하기 전인데도 불구하고 `printMyName`을 호출하면 정상적으로 컴파일하는것을 알 수 있다. 또한, 호이스팅은 함수내부에 국한하지 않고 함수외부에서도 일어나는데, 여기서 주의할 점은 변수 선언은 호이스팅되지만, 변수 할당은 호이스팅이 일어나지 않는다. 다음의 예를 보자.

```jsx
// 실제코드
console.log(name);  // undefined
var name = "안영우";
console.log(name);  // 안영우

// 내부 작동 코드
var name;    // isHoisting
console.log(name);    // undefined
name = "안영우";    // assignment
console.log(name);    // 안영우
```

같은 상황에서 `let` 은 다르게 출력되는데, 코드를 실행하면 `ReferenceError: Cannot access 'name' before initialization` 오류가 뜬다. 

```jsx
console.log(name);  // ReferenceError: Cannot access 'name' before initialization 
let name = "안영우";
console.log(name);  // 안영우
```

`var` 변수와 달리 `let`, `const` 는 호이스팅이 되지 않아서 이런 에러가 뜨는것일까? 그렇지 않다. `let`, `const` 변수도 호이스팅된다. 하지만 `var` 변수와는 다르게 `let` , `const` 변수는 `TDZ(Temporal Dead Zone)` 의 영향을 받는다. 이전 코드에서 `TDZ` 의 영역은 다음과 같다. `TDZ(Temporal Dead Zone)`란 <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz'>시간적 사각지대</a>를 의미하는데, 변수가 블록 시작부터 초기화가 완료될 때까지를 `TDZ` 라고 일컫는다. 쉽게 말해서 변수에 실질적인 값을 할당하기 전엔 사용할 수 없는데 `TDZ` 를 설정하는 이유는 코드를 예측가능하고, 잠재적인 버그를 줄이기 위함이다.

```jsx
console.log(name);  // TDZ(Temporal Dead Zone)
let name = "안영우";
console.log(name);  // 안영우
```

`JS` 에서 변수의 생성과정은 3단계에 걸쳐서 정의되는데, 변수 선언 → 변수 초기화 → 변수 할당의 순서로 정의된다. 여기서 `var`  `let` , `const` 는 각각 다른 과정으로 변수가 만들어진다.

우선, `var` 는 선언단계 + 초기화단계가 동시에 이루어지고 이후 할당 단계를 거친다. 다음의 코드를 보자.  선언하지도 않은 `name` 값에 `undefined` 가 출력되는것을 알 수 있는데, 이는 호이스팅과정을 거치면서 `var` 변수의 생성 + `var` 초기화 값 `undefined` 이 동시에 이루어지기 때문이다. 이후 `name = "안영우"` 라는 값을 할당하면 그제서야 내가 할당한 값인 `안영우` 값이 나온다.

```jsx
// 실제 코드
console.log(name);    // undefined
var name;
name = "안영우";
console.log(name);    // 안영우

// 내부 호이스팅
var name;
console.log(name);    // undefined
name = "안영우";
console.log(name);    // 안영우
```

다음으로 `let` 은 선언 → 초기화 → 할당 순으로 이루어지는데, 다음의 코드에서는 `let`이 호이스팅되면서 선언단계까지 이루어졌지만, 보통 초기화 단계는 실제 코드에 도달했을 때 일어나기 때문에 `ReferenceError` 가 나오는것이다.

```jsx
// 실제 코드
console.log(name);    // ReferenceError: Cannot access 'name' before initialization
let name;
name = "안영우";
console.log(name);    // 안영우

// 내부 호이스팅
console.log(name);    // TDZ 
let name;
name = "안영우";
console.log(name);    // 안영우
```

마지막으로 `const` 는 선언 + 초기화 + 할당 모두 동시에 이루어져야한다. `var`, `let`는 선언만 해두고 나중에 사용하는것이 가능하지만 `const`는 한번에 할당까지 해야 사용가능하다.

```jsx
// var
var name;
name = "안영우";

// let
let age;
age = 27;

// const
const gender;
gender = "male";    // SyntaxError: Missing initializer in const declaration
```

또, `var` , `let` , `const`  변수는  호출 가능한 영역(?)인 스코프가 각각 정해져있는데 여기서 <a href='https://developer.mozilla.org/ko/docs/Glossary/Scope'>스코프</a>란 현재 실행되는 `컨텍스트(context)` 쉽게 말해 변수 또는 다른 표현식이 해당 스코프내에 있지 않다면 사용 할 수 없다. 스코프는 또한 계층적인 구조를 가지기 때문에 하위 스코프는 상위 스코프에 접근할 수 있지만 반대는 불가하다.  `var` 는 `함수 스코프(function-scoped)`의 영향을, `let` , `const` 는 `블록 스코프(block-scoped)` 의 영향을 받는다. 

 `var` 변수는 유일하게 `함수 스코프(function-scoped)`영향을 받는다고 했는데, 쉽게말하면 함수내부에서 값을 호출 할때는 함수외부에서 호출 할 수 없고 함수 내부에서만 호출 할 수 있고 다른 조건문, 반복문 등에서는 호출이 가능하다. 다음 예를 보자.

```jsx
// 함수 score 외부에서 var변수 호출(불가능)
function myName(){
    var name = "안영우";    
}
myName();
console.log(name);    // ReferenceError: name is not defined

// 함수 score 내부에서 var변수 호출(가능)
function myName(){
    var name = "안영우";    
    console.log(name);   
}

myName();    // 안영우

// 조건문 밖에서 var변수 호출(가능)
if (true){
    var age = 27;
}

console.log(age);    // 27

```

`let`, `const` 는 블록 스코프의 영향을 받는다. 여기서 블록이란 중괄호 내부 (`if`, `for` , `while` , `try/catch` 문 등)을 뜻한다.

```jsx
// if문 내부에서 호출(가능)
if(true){
    let age = 27;
    console.log(age);    // 27
}

// if문 외부에서 호출(불가능)
if(true){
    let age = 27;
}
console.log(age);    // ReferenceError: age is not defined

// function 내부에서 호출(가능)
function showMyAge(){
    const age = 27;
		console.log(age);
}

showMyAge();    // 27

// function 외부에서 호출(불가능)
function showMyAge(){
    const age = 27;
}

showMyAge();
console.log(age);    // ReferenceError: age is not defined

```

지금까지 `var`, `let` ,`const` 변수들의 차이점과 호이스팅(hoisting), TDZ, 스코프에대해서 배웠다. `var` 는 이제 사용하지않고, `let` ,`const` 를 사용하는 이유는 예측가능하고 잠재적인 `bug` 를 줄이기 위한것임을 기억하자.

Reference
1. <a href='https://www.youtube.com/watch?v=ocGc-AmWSnQ&list=PLZKTXPmaJk8JZ2NAC538UzhY_UNqMdZB4&index=1'>자바스크립트 중급 강좌 #1 - 변수, 호이스팅, TDZ(Temporal Dead Zone)</a>
2. <a href='https://developer.mozilla.org/ko/'>MDN</a>

---
## 📍 객체 메소드(Object Methods)에 대해 알아보자.

기본적으로 `원시 타입(Primitive)`과 `객체(Object)`의 근본적인 차이점은 원시타입은 값 자체를 저장 또는 할당하고 객체는 저장되어있는 메모리의 주소를 가리킨다는 점이다.

일반적으로 다음과 같은 코드는 객체 값이 복사되지 않고 `주소값`만 복사 된다. 같은 주소를 가리키고 있기 때문에 `user`의 프로퍼티 값을 바뀌면 자연스럽게 `copyUser`의 값도 바뀌게 된다.(맨 처음에 언급했던 객체는 같은 주소값을 가리키고 있는것을 생각하자.)

```jsx
const user = {
	name: "안영우",
	age: 27,
} 

const copyUser = user;
user["name"] = "안영준"
user["age"] = 14

console.log(copyUser);  // { name: '안영준', age: 14 }
```

이전에 `var`, `let`, `const` 변수의 차이점을 <a href='https://ywtechit.tistory.com/227'>공부</a>하면서 떠오른것은 `const` 변수로 선언된 객체는 `선언 + 초기화 + 할당` 을 동시에 하기 때문에 변수선언 이후 프로퍼티가 바뀌면 오류가 나야하는것 아닌가?? 라고 할수도 있지만, `const` 변수는 `user`의 값을 고정하지만 그 내용은 고정하지 않는다. ([참고: 코어 자바스크립트](https://ko.javascript.info/object#ref-18))

---
### 1️⃣ Object.assign()
결론적으로 참조값을 복사하지 않고 객체 자체를 복사하고 싶다면 `Object.assign()` 함수인 `const copyUser = Object.assign({}, user)`을 사용하면 되는데, 여기서 첫번째 매개변수인 `{}` 는 `초기값`을 뜻하고 두번째 매개변수는 첫번째 매개변수(초기값 {})와 합친다는 뜻이다. 다음 코드에서 `assign`으로 객체를 복사한 변수는 원래의 값을 변경해도 프로퍼티의 값이 변경되지 않는 모습을 볼 수 있다.

```jsx
const user = {
	name: "안영우",
	age: 27,
} 

const copyUser = Object.assign({}, user);
user["name"] = "안영준"
user["age"] = 14

console.log(copyUser);  // { name: '안영우', age: 27 }
```

위에서 언급한 `const copyUser = Object.assign({}, user)`코드에서 첫번째 파라미터인 `{}`는 초기값을 뜻한다고 했는데, 여기에 초기값을 `{}` 대신 값이 들어있는 객체형태로 선언해서 합칠 수도 있다. 

```jsx
const userInfo = {
	age: 27
}
const addUserInfo = Object.assign({name: "안영우"}, userInfo);

console.log(addUserInfo);  // { name: '안영우', age: 27 }
```

만약, 초기객체의 `key`와 새로 덮으려는 `key` 값이 중복되면 새로 넘어온 값을 덮어씌운다. 

```jsx
const userInfo = {
	name: "안영우"
}
const overLapNameInfo = Object.assign(userInfo, {name: "안영준"});

console.log(overLapNameInfo);  // { name: '안영준' }
```

또, 2개이상의 객체도 합칠 수 있다. 이때 가장 좌측에있는 초기객체에 덮어씌운다.

```jsx

const mergeMultipleObjs = Object.assign({name: "안영우"}, {age: 27}, {gender: "man"});

console.log(mergeMultipleObjs);  // { name: '안영우', age: 27, gender: 'man' }
```

---
### 2️⃣ Object.keys()
객체의 `key`값을 모아 새로운 배열로 반환시키는 메소드다.

```jsx
const user = {
	name: "안영우",
    age: 27,
    gender: "male"
} 
const userKey = Object.keys(user);
console.log(userKey);  // [ 'name', 'age', 'gender' ]
```

---
### 3️⃣ Object.values()
객체의 `value`를 모아 새로운 배열로 반환시키는 메소드다.

```jsx
const user = {
	name: "안영우",
    age: 27,
    gender: "male"
} 
const userKey = Object.values(user);
console.log(userKey);  // [ '안영우', 27, 'male' ]
```

---
### 4️⃣ Object.entries()
`key`와 `value`를 모두 배열로 반환할 때 사용하는 메소스다.

```jsx
const user = {
	name: "안영우",
    age: 27,
    gender: "male"
} 
const userKey = Object.values(user);
console.log(userKey);  // [ [ 'name', '안영우' ], [ 'age', 27 ], [ 'gender', 'male' ] ]
```

---
### 5️⃣ Object.fromEntries()
`Object.entries()` 와 반대로 `key` 와 `value` 가 쌍으로 묶여있는 배열을 객체로 바꿀때 사용하는 메소드다

```jsx
const changeObjFromArray = Object.fromEntries([ [ 'name', '안영우' ], [ 'age', 27 ], [ 'gender', 'male' ] ]);
console.log(changeObjFromArray)   // { name: '안영우', age: 27, gender: 'male' }
```

Reference
1. [자바스크립트 중급 강좌 #3 - 객체 메소드(Object methods), 계산된 프로퍼티(Computed property)](https://www.youtube.com/watch?v=6NZpyA64ZUU&list=PLZKTXPmaJk8JZ2NAC538UzhY_UNqMdZB4&index=3)
2. [모던 JavaScript 튜토리얼](https://ko.javascript.info/)
3. [Object.assign() - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)