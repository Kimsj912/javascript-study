# 화살표 함수 (Arrow Function)

## 화살표 함수의 선언

`function` 키워드 대신 화살표 `=>`를 사용하여 간략하게 함수를 선언하는 방법

```jsx
// 매개변수 지정 방법
    () => { ... } // 매개변수가 없을 경우
     x => { ... } // 매개변수가 한 개인 경우, 소괄호를 생략할 수 있다.
(x, y) => { ... } // 매개변수가 여러 개인 경우, 소괄호를 생략할 수 없다.

// 함수 몸체 지정 방법
x => { return x * x }  // single line block
x => x * x             // 함수 몸체가 한줄의 구문이라면 중괄호를 생략할 수 있으며 암묵적으로 return된다. 위 표현과 동일하다.

() => { return { a: 1 }; }
() => ({ a: 1 })  // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.

() => {           // multi line block.
  const x = 10;
  return x * x;
};
```

## 화살표 함수의 호출

- 익명 함수로만 사용 가능

```jsx
// 함수 표현식
const pow = function(x) { return x * x; };
// 화살표 함수
const pow = x => x * x;

console.log(pow(10)); // 100
```

- 콜백 함수로 사용 가능

```jsx
const arr = [1, 2, 3];

// 함수 표현식
var pow = arr.map(function (x) {
  return x * x;
});
// 화살표 함수
const pow = arr.map(x => x * x);

console.log(pow); // [ 1, 4, 9 ]
```

## this

`this`는 `function` 키워드로 생성한 일반 함수와 화살표 함수의 가장 큰 차이점임

### 일반 함수의 this

자바스크립트의 경우 함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 `this`에 바인딩할 객체가 동적으로 결정됨

바인딩 : 어떤 대상물의 이름을 그것이 나타내는 실제의 대상물과 연결하는 것

```jsx
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // (A)
  return arr.map(function (x) {
    return this.prefix + ' ' + x; // (B)
  });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

- (A) 지점의 `this` : 생성자 함수 Prefixer가 생성한 객체인 `pre`를 가리킴
- (B) 지점의 `this` : 전역 객체 `window` ⇒ 콜백 함수의 `this`는 전역 객체를 가리키기 때문

위의 경우에서 (B) 지점의 `this`가 우리가 원하는 방식대로, 즉 `pre`를 가리키게 하는 방법은 3가지임

```jsx
// Solution 1: that = this
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  var that = this;  // this: Prefixer 생성자 함수의 인스턴스
  return arr.map(function (x) {
    return that.prefix + ' ' + x;
  });
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

```jsx
// Solution 2: map(func, this)
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;
  }, this); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

```jsx
// Solution 3: bind(this)
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  return arr.map(function (x) {
    return this.prefix + ' ' + x;
  }.bind(this)); // this: Prefixer 생성자 함수의 인스턴스
};

var pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

### 화살표 함수의 this

화살표 함수의 `this`는  언제나 상위 스코프의 `this`를 가리키며, `call`, `apply`, `bind` 메소드를 사용하여 `this`를 변경할 수 없음

```jsx
function Prefixer(prefix) {
  this.prefix = prefix;
}

Prefixer.prototype.prefixArray = function (arr) {
  // this는 상위 스코프인 prefixArray 메소드 내의 this를 가리킴
  return arr.map(x => `${this.prefix}  ${x}`);
};

const pre = new Prefixer('Hi');
console.log(pre.prefixArray(['Lee', 'Kim']));
```

## 화살표 함수를 사용해서는 안되는 경우

### 메소드

```jsx
// Bad
const person = {
  name: 'Lee',
  sayHi: () => console.log(`Hi ${this.name}`)
};

person.sayHi(); // Hi undefined
```

위와 같은 방식으로 사용할 경우 `sayHi` 메소드의 `this`는 상위 컨택스트인 전역 객체 `window`를 가리킴

```jsx
// Good
const person = {
  name: 'Lee',
  sayHi() { // === sayHi: function() {
    console.log(`Hi ${this.name}`);
  }
};

person.sayHi(); // Hi Lee
```

### prototype

화살표 함수르 정의된 메소드를 `prototype`에 할당하는 경우에도 동일한 문제가 발생하므로, 일반 함수 사용

```jsx
// Bad
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);

person.sayHi(); // Hi undefined
```

```jsx
// Good
const person = {
  name: 'Lee',
};

Object.prototype.sayHi = function() {
  console.log(`Hi ${this.name}`);
};

person.sayHi(); // Hi Lee
```

### 생성자 함수

화살표 함수는 생성자 함수로 사용할 수 없음

⇒ 생성자 함수는 `prototype` 프로퍼티를 가지지만 화살표 함수는 `prototype` 프로퍼티가 없기 때문임

```jsx
const Foo = () => {};

// 화살표 함수는 prototype 프로퍼티가 없다
console.log(Foo.hasOwnProperty('prototype')); // false

const foo = new Foo(); // TypeError: Foo is not a constructor
```

### addEventListener 함수의 콜백 함수

이 경우에도 동일하게 화살표 함수의 `this`가 전역 객체 `window`를 가리키게 되므로 `function` 키워드로 정의한 일반 함수를 사용해야 함

```jsx
// Bad
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
  console.log(this === window); // => true
  this.innerHTML = 'Clicked button';
});
```

```jsx
// Good
var button = document.getElementById('myButton');

button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```