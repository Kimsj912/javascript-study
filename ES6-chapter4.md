# 매개변수 기본값, Rest 파라미터, Spread 문법 (Extended Parameter Handling)

## 매개변수 기본값 (Default Parameter value)

함수는 매개변수의 개수와 인수의 개스를 체크하지 않음

인수가 부족한 경우 매개변수의 값은 `undefined`가 됨

```jsx
function sum(x, y) {
  return x + y;
}

console.log(sum(1)); // NaN
```

ES6에서는 매개변수에 기본값을 할당할 수 있으며, 할당된 기본값은 매개변수에 인수를 전달하지 않았을 경우에만 유효함

```jsx
function sum(x = 0, y = 0) {
  return x + y;
}

console.log(sum(1));    // 1
console.log(sum(1, 2)); // 3
```

매개변수 기본값은 함수 정의 시 선언한 매개변수의 개수를 나타내는 함수 객체의 `length` 프로퍼티와 `arguments` 객체에 영향을 주지 않음

```jsx
function foo(x, y = 0) {
  console.log(arguments);
}

console.log(foo.length); // 1

sum(1);    // Arguments { '0': 1 }
sum(1, 2); // Arguments { '0': 1, '1': 2 }
```

## Rest 파라미터

### 기본 문법

: 매개변수 이름 앞에 세개의 점 `...` 을 붙여서 정의한 매개변수를 의미하며, Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받음

```jsx
function foo(...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
```

함수에 전달된 인수들은 순차적으로 파라미터와 Rest 파라미터에 할당되고, Rest 파라미터는 먼저 할당된 인수를 제외한 나머지 인수들을 모두 배열에 담아 할당하므로 반드시 마지막에 위치해야 함

```jsx
function bar(param1, param2, ...rest) {
  console.log(param1); // 1
  console.log(param2); // 2
  console.log(rest);   // [ 3, 4, 5 ]
}

bar(1, 2, 3, 4, 5);
```

Rest 파라미터는 `length` 프로퍼티에 영향을 주지 않음

```jsx
function foo(...rest) {}
console.log(foo.length); // 0

function bar(x, ...rest) {}
console.log(bar.length); // 1
```

### arguments와 rest 파라미터

**ES5**

인자의 개수를 사전에 알 수 없는 가변 인자 함수의 경우 `arguments` 객체를 통해 인수를 확인함

하지만 `arguments` 객체는 유사 배열 객체이므로 배열 메소드를 사용하려면 `Function.prototype.call`을 사용해야 하는 번거로움이 있음

```jsx
function sum() {
  /*
  가변 인자 함수는 arguments 객체를 통해 인수를 전달받는다.
  유사 배열 객체인 arguments 객체를 배열로 변환한다.
  */
  var array = Array.prototype.slice.call(arguments);
  return array.reduce(function (pre, cur) {
    return pre + cur;
  });
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```

**ES6**

Rest 파라미터를 사용하여 가변 인자의 목록을 배열로 전달받을 수 있음

화살표 함수에는 `arguments` 프로퍼티가 없으므로 화살표 함수로 가변 인자 함수를 구현할 때에는 반드시 Rest 파라미터를 사용해야 함

```jsx
function sum(...args) {
  console.log(arguments); // Arguments(5) [1, 2, 3, 4, 5, callee: (...), Symbol(Symbol.iterator): ƒ]
  console.log(Array.isArray(args)); // true
  return args.reduce((pre, cur) => pre + cur);
}
console.log(sum(1, 2, 3, 4, 5)); // 15
```

## Spread 문법

Spread 문법(`...`)은  대상을 개별 요소로 분리하며, 대상은 이터러블이어야 함

이터러블 : 순회 가능한 자료구조

```jsx
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(→ 1, 2, 3)
console.log(...[1, 2, 3]) // 1, 2, 3

// 문자열은 이터러블이다.
console.log(...'Hello');  // H e l l o

// Map과 Set은 이터러블이다.
console.log(...new Map([['a', '1'], ['b', '2']]));  // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3]));  // 1 2 3

// 이터러블이 아닌 일반 객체는 Spread 문법의 대상이 될 수 없다.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```

### 함수의 인수로 사용하는 경우

**ES5**

배열을 분해하여 각 요소를 파라미터에 전달하고 싶은 경우 `Function.prototype.apply` 사용

```jsx
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 분해하여 배열의 각 요소를 파라미터에 전달하려고 한다.
const arr = [1, 2, 3];

// apply 함수의 2번째 인수(배열)는 분해되어 함수 foo의 파라이터에 전달된다.
foo.apply(null, arr);
// foo.call(null, 1, 2, 3);
```

**ES6**

ES6의 Spread 문법을 사용한 배열을 인수로 함수에 전달하면 배열의 요소를 분해하여 순차적으로 할당

```jsx
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 foo 함수의 인자로 전달하려고 한다.
const arr = [1, 2, 3];

/* ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(→ 1, 2, 3)
   spread 문법에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다. */
foo(...arr);
```

Rest 파라미터는 Spread 문법을 사용하여 파라미터를 정의한 것

```jsx
/* Spread 문법을 사용한 매개변수 정의 (= Rest 파라미터)
   ...rest는 분리된 요소들을 함수 내부에 배열로 전달한다. */
function foo(param, ...rest) {
  console.log(param); // 1
  console.log(rest);  // [ 2, 3 ]
}
foo(1, 2, 3);

/* Spread 문법을 사용한 인수
  배열 인수는 분리되어 순차적으로 매개변수에 할당 */
function bar(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(-> 1, 2, 3)
// spread 문법에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
bar(...[1, 2, 3]);
```

### 배열에서 사용하는 경우

1. concat

**ES5**

기존 배열의 요소를 새로운 배열 요소의 일부로 만들고 싶은 경우 `concat` 메소드 사용

```jsx
var arr = [1, 2, 3];
console.log(arr.concat([4, 5, 6])); // [ 1, 2, 3, 4, 5, 6 ]
```

**ES6**

Spread 문법을 사용하면 배열 리터럴만으로 기존 배열의 요소를 새로운 배열 요소의 일부로 만들 수 있음

```jsx
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ]
```

2. push

**ES5**

기존 배열에 다른 배열의 개별 요소를 각각 넣어주려는 경우 `push` 사용

```jsx
var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];

// apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 push 메소드에 전달된다.
Array.prototype.push.apply(arr1, arr2);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

**ES6**

```jsx
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// ...arr2는 [4, 5, 6]을 개별 요소로 분리한다
arr1.push(...arr2); // == arr1.push(4, 5, 6);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

3. splice

**ES5**

기존 배열에 다른 배열의 개별 요소를 삽입하는 경우 `splice` 사용

```jsx
var arr1 = [1, 2, 3, 6];
var arr2 = [4, 5];

/*
apply 메소드의 2번째 인자는 배열. 이것은 개별 인자로 splice 메소드에 전달된다.
[3, 0].concat(arr2) → [3, 0, 4, 5]
arr1.splice(3, 0, 4, 5) → arr1[3]부터 0개의 요소를 제거하고 그자리(arr1[3])에 새로운 요소(4, 5)를 추가한다.
*/
Array.prototype.splice.apply(arr1, [3, 0].concat(arr2));

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

**ES6**

```jsx
const arr1 = [1, 2, 3, 6];
const arr2 = [4, 5];

// ...arr2는 [4, 5]을 개별 요소로 분리한다
arr1.splice(3, 0, ...arr2); // == arr1.splice(3, 0, 4, 5);

console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

4. copy

**ES5**

기존 배열을 복사하기 위해 `slice` 메소드 사용

```jsx
var arr  = [1, 2, 3];
var copy = arr.slice();

console.log(copy); // [ 1, 2, 3 ]

// copy를 변경한다.
copy.push(4);

console.log(copy); // [ 1, 2, 3, 4 ]
// arr은 변경되지 않는다.
console.log(arr);  // [ 1, 2, 3 ]
```

**ES6**

```jsx
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
const copy = [...arr];

console.log(copy); // [ 1, 2, 3 ]

// copy를 변경한다.
copy.push(4);

console.log(copy); // [ 1, 2, 3, 4 ]
// arr은 변경되지 않는다.
console.log(arr);  // [ 1, 2, 3 ]
```

Spread 문법을 사용하면 유사배열 객체를 배열로 손쉽게 변환 가능

```jsx
const htmlCollection = document.getElementsByTagName('li');

// 유사 배열인 HTMLCollection을 배열로 변환한다.
const newArray = [...htmlCollection]; // Spread 문법

// ES6의 Array.from 메소드를 사용할 수도 있다.
// const newArray = Array.from(htmlCollection);
```