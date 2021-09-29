# 함수 (Function)

: 어떠한 작업을 수행하기 위해 필요한 문(statement)들의 집합을 정의한 코드 블록

## 특징

- 목적 : 코드의 재사용
- 객체 생성, 객체의 행위 정의(메소드), 정보 은닉, 클로저, 모듈화 등의 기능 수행
- 일급 객체, 호출 가능

## 함수의 정의

### 함수 선언문

```jsx
function square(num) {
  return num * num;
};
```

- 함수명 : 함수명은 자신을 재귀적으로 호출하거나 디버거가 함수를 구분하는 식별자로 사용되므로 생략 불가능
- 매개변수 : 괄호로 감싸고 콤마로 분리, 매개변수의 타입 기술 X
- 함수 몸체 : 함수 호출 시 실행되는 문들의 집합

### 함수 표현식

: 함수 리터럴 방식으로 함수를 정의하고 변수에 할당

```jsx
var square = function(num) {
  return num * num;
}
```

```
💡 리터럴 : 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법
   함수 리터럴 : `function() {}`
```

- 함수명을 생략하는 것이 일반적 (익명 함수)
- 기명 함수 표현식을 사용해서 함수를 정의하더라도 호출 시 함수명이 아니라 함수를 가리키는 변수명 사용

  ⇒ 변수는 함수명이 아니라 할당된 함수를 가리키는 참조값 저장, 함수명은 몸체 내부에서만 유효한 식별자

```jsx
// 기명 함수 표현식(named function expression)
var foo = function multiply(a, b) {
  return a * b;
};

// 익명 함수 표현식(anonymous function expression)
var bar = function(a, b) {
  return a * b;
};

console.log(foo(10, 5)); // 50
console.log(multiply(10, 5)); // Uncaught ReferenceError: multiply is not defined
```

- 함수 선언문도 함수 표현식과 동일하게 함수 리터럴 방식으로 정의됨

```jsx
var square = function square(number) {
  return number * number;
};
```

### Function 생성자 함수

: 내장 함수 `Function` 생성자 함수로 함수를 생성

```jsx
// new Function(arg1, arg2, ... argN, functionBody)

var square = new Function('number', 'return number * number');
console.log(square(10)); // 100
```

함수 리터럴 방식도 `Function` 생성자 함수로 생성하는 것을 단순화시킨 축약법임

## 일급 객체 (First-class Object)

: 생성, 대입, 연산, 인자 또는 반환값으로서의 전달 등 프로그래밍 언어의 기본적 조작을 제한없이 사용할 수 있는 대상

### 조건

- 무명의 리터럴로 표현 가능
- 변수나 자료 구조(객체, 배열 등)에 저장 가능
- 매개변수에 전달 가능
- 반환값으로 사용 가능

```jsx
// 1. 무명의 리터럴로 표현이 가능하다.
// 2. 변수나 자료 구조에 저장할 수 있다.
var increase = function (num) {
  return ++num;
};

var decrease = function (num) {
  return --num;
};

var predicates = { increase, decrease };

// 3. 함수의 매개변수에 전달할 수 있다.
// 4. 반환값으로 사용할 수 있다.
function makeCounter(predicate) {
  var num = 0;

  return function () {
    num = predicate(num);
    return num;
  };
}

var increaser = makeCounter(predicates.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2
```

## 함수 호이스팅

### 호이스팅

: `var` 선언문이나 `function` 선언문 등 모든 선언문이 해당 스코프의 선두로 옮겨진 것처럼 동작하는 특성

- 함수 호이스팅 : 함수 선언, 초기화, 할당이 한번에 이루어짐
  ⇒ 함수 선언 위치와 관계 없이 코드 내 어느 곳에서든 호출 가능

  `함수 선언문`


- 변수 호이스팅 : 변수 선언, 초기화가 한번에 이루어지고 할당문에 도달 시 값이 할당됨
  
  `함수 표현식`

```jsx
// 함수 선언문

var res = square(5);

function square(number) {
  return number * number;
}

// 함수 표현식

var res = square(5); // TypeError: square is not a function

var square = function(number) {
  return number * number;
}
```

## 매개변수 (Parameter, 인자)

: 함수의 작업 실행을 위해 추가적인 정보가 필요할 경우, 함수 내에서 변수와 동일하게 동작하는 매개변수를 지정함

### 매개변수, 인자 (Parameter) / 인수 (Argument)

- 매개변수 : 함수를 정의할 때 외부로부터 받아들이는 임의의 값
- 인수 : 함수 호출 시 전달되는 값

```jsx
function add(x, y) {  // x, y => 매개변수
	return x + y;
}

add(2, 5);  // 2, 5 => 인수
```

### 값에 의한 호출 (Call-by-value)

: 인수를 매개변수로 전달할 때 매개변수에 값을 복사하여 함수를 전달하는 방식 (원시 타입 인수에 적용)

⇒ 함수 내에서 매개변수를 통해 값이 변경되어도 전달이 완료된 값은 변경되지 않음

### 참조에 의한 호출 (Call-by-reference)

: 인수를 매개변수로 전달할 때 객체의 참조값이 매개변수에 저장되어 함수로 전달되는 방식 (객체형(참조형) 인수에 적용)

⇒ 함수 내에서 값 변경 시 전달된 참조형의 인수값도 함께 변경됨

```jsx
function changeVal(primitive, obj) {
  primitive += 100;
  obj.name = 'Kim';
  obj.gender = 'female';
}

var num = 100;
var obj = {
  name: 'Lee',
  gender: 'male'
};

console.log(num); // 100
console.log(obj); // Object {name: 'Lee', gender: 'male'}

changeVal(num, obj);

console.log(num); // 100
console.log(obj); // Object {name: 'Kim', gender: 'female'}
```

## 반환값

: 자신을 호출한 코드에게 수행된 결과를 반환할 수 있는데, 이 때 반환된 값을 반환값이라고 함

- `return` 키워드 사용
- 배열 등을 이용하여 한 번의 여러 개의 값 리턴 가능
- 반환 생략 가능 (암묵적으로 `undefined` 반환)
- `return` 키워드 이후의 구문은 실행되지 않음

```jsx
function getSize(width, height, depth) {
  var area = width * height;
  var volume = width * height * depth;
  return [area, volume]; // 복수 값의 반환
}

console.log('area is ' + getSize(3, 2, 3)[0]);   // area is 6
```

## 함수 객체의 프로퍼티

### `argument` 프로퍼티

: 함수 호출 시 전달된 인수(argument)들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체(array-like object)

```
💡 유사 배열 객체 : length 프로퍼티를 가진 객체, 배열이 아니므로 배열 메소드 사용 시 에러 발생
   ⇒ 배열 메소드 사용 시 `Function.prototype.call`, `Function.prototype.apply` 사용
```

**자바스크립트의 특성**

- 매개변수의 개수보다 인수를 적게 전달했을 때, 인수가 전달되지 않은 매개변수는 `undefined`로 초기화
- 매개변수의 개수보다 인수를 더 많이 전달한 경우, 초과된 인수는 무시됨

```jsx
function multiply(x, y) {
  console.log(arguments);
  return x * y;
}

multiply();        // {}
multiply(1);       // { '0': 1 }
multiply(1, 2);    // { '0': 1, '1': 2 }
multiply(1, 2, 3); // { '0': 1, '1': 2, '2': 3 }
```

⇒ 이러한 특성 때문에 호출된 함수의 인자 개수를 확인하고 이에 따라 동작을 달리 정의할 필요가 있을 수 있는데, 이 때 유용하게 사용할 수 있으며, 매개변수 개수가 확정되지 않은 가변 인자 함수를 구현할 때에도 유용하게 사용됨

```jsx
function sum() {
  var res = 0;

  for (var i = 0; i < arguments.length; i++) {
    res += arguments[i];
  }

  return res;
}

console.log(sum());        // 0
console.log(sum(1, 2));    // 3
console.log(sum(1, 2, 3)); // 6
```

### `caller` 프로퍼티

: 자신을 호출한 함수를 의미함

```jsx
function foo(func) {
  var res = func();
  return res;
}

function bar() {
  return 'caller : ' + bar.caller;
}

console.log(foo(bar)); // caller : function foo(func) {...}
console.log(bar());    // null (browser에서의 실행 결과)
```

### `length` 프로퍼티

: 함수 정의 시 작성된 매개변수의 개수 (↔ `argument.length` : 함수 호출 시 인자의 개수)

```jsx
function foo() {}
console.log(foo.length); // 0

function bar(x) {
  return x;
}
console.log(bar.length); // 1
```

### `name` 프로퍼티

: 함수명을 나타냄 (기명함수 ⇒ 함수명, 익명함수 ⇒ 빈 문자열)

```jsx
// 기명 함수 표현식(named function expression)
var namedFunc = function multiply(a, b) {
  return a * b;
};

// 익명 함수 표현식(anonymous function expression)
var anonymousFunc = function(a, b) {
  return a * b;
};

console.log(namedFunc.name);     // multiply
console.log(anonymousFunc.name); // ''
```

### `__proto__` 접근자 프로퍼티

: 모든 객체가 가지고 있는 `[[Prototype]]` 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용 (직접 접근은 불가능)

```jsx
// __proto__ 접근자 프로퍼티를 통해 자신의 프로토타입 객체에 접근할 수 있음
// 객체 리터럴로 셍성한 객체의 프로토타입 객체는 Object.prototype임

console.log({}.__proto__ === Object.prototype); // true
```

### `prototype` 프로퍼티

: 함수 객체만이 소유하는 프로퍼티로, 함수가 객체를 생성하는 생성자 함수로 사용될 때, 생성자 함수가 생성한 인스턴스의 프로토타입 객체를 가리킴

```jsx
// 함수 객체는 prototype 프로퍼티를 소유함

console.log(Object.getOwnPropertyDescriptor(function() {}, 'prototype'));
// {value: {…}, writable: true, enumerable: false, configurable: false}
```

## 함수의 형태

### 즉시 실행 함수 (IIFE, Immediately Invoke Function Expression)

: 정의와 동시에 실행되는 함수로, 최초 한번만 호출되며 다시 호출하는 것이 불가능함

⇒ 최초 한번만 실행이 필요한 초기화 처리 등에 사용

```jsx
// 즉시 실행 함수는 소괄호로 감싸줌

// 기명 즉시 실행 함수(named immediately-invoked function expression)
(function myFunction() {
  var a = 3;
  var b = 5;
  return a * b;
}());

// 익명 즉시 실행 함수(immediately-invoked function expression)
(function () {
  var a = 3;
  var b = 5;
  return a * b;
}());
```

### 내부 함수 (Inner Function)

: 함수 내부에 정의된 함수

- 내부 함수는 부모 함수의 변수에 접근할 수 있지만, 부모 함수는 내부 함수의 변수에 접근할 수 없음
- 내부함수는 부모함수의 외부에서 접근할 수 없음

```jsx
function parent(param) {
  var parentVar = param;
  function child() {
    var childVar = 'lee';
    console.log(parentVar + ' ' + childVar); // Hello lee
  }
  child();
  console.log(parentVar + ' ' + childVar);
  // Uncaught ReferenceError: childVar is not defined
}
parent('Hello');
child(); // child is not defined
```

### 재귀 함수 (Recusive Function)

: 자기 자신을 호출하는 함수

- 반복 연산을 간단히 구현할 수 있음
- 호출을 멈출 수 있는 조건을 반드시 지정해주어야 함

  ⇒ 조건이 없는 경우, 함수가 무한 호출되어 stackoverflow 에러 발생

```jsx
// 팩토리얼
// 팩토리얼(계승)은 1부터 자신까지의 모든 양의 정수의 곱이다.
// n! = 1 * 2 * ... * (n-1) * n
function factorial(n) {
  if (n < 2) return 1;
  return factorial(n - 1) * n;
}

console.log(factorial(0)); // 1
console.log(factorial(1)); // 1
console.log(factorial(2)); // 2
console.log(factorial(3)); // 6
console.log(factorial(4)); // 24
console.log(factorial(5)); // 120
console.log(factorial(6)); // 720
```

### 콜백 함수 (Callback Function)

: 특정 이벤트가 발생했을 때 시스템에 의해 호출되는 함수

- 매개변수를 통해 전달되며, 전달받은 함수의 내부에서 **어느 특정 시점**에 실행됨
- 비동기식 처리 모델에 주로 사용됨

```
💡 비동기식 처리 모델
   : 처리가 종료되면 호출될 함수(콜백 함수)를 미리 매개변수에 전달하고 처리가 종료된 후에 콜백함수를 호출하는 것
```
```jsx
function doSomething() {
  var name = 'Lee';

  setTimeout(function () {
    console.log('My name is ' + name);
  }, 100);
}

doSomething(); // My name is Lee
```