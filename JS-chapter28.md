# 배열 (Array)

: 1개의 변수에 여러 개의 값을 순차적으로 저장할 때에 사용함

## 배열의 생성

### 배열 리터럴

- 0개 이상의 값을 쉼표로 구분하여 대괄호 `[]` 로 묶음
- 존재하지 않는 요소에 접근 시 `undefined` 반환
- 요소에 접근 시 대괄호 표기법 사용, 대괄호 내에 접근하려는 요소의 인덱스 넣어줌
- 배열의 요소들은 모두 같은 데이터 타입이 아니어도 상관없음

```jsx
const misc = [
  'string',
  10,
  true,
  null,
  undefined,
  NaN,
  Infinity,
  ['nested array'],
  { object: true },
  function () {}
];

console.log(misc[1]); // 10
```

### Array() 생성자 함수

: 내장 함수 `Array()` 생성자 함수로 배열을 생성

매개변수가 1개인 경우 전달된 숫자를 `length` 값으로 가지는 빈 배열을 생성하며, 2개 이상인 경우 전달된 값들을 요소로 가지는 배열을 생성함

```jsx
const arr = new Array(2);
console.log(arr); // (2) [empty × 2]
```

## 배열 요소의 추가와 삭제

### 배열 요소의 추가

: 인덱스를 사용하여 값 할당

```jsx
const arr = [];
console.log(arr[0]); // undefined

arr[1] = 1;
arr[3] = 3;

console.log(arr); // (4) [empty, 1, empty, 3]
console.log(arr.length); // 4
```

### 배열 요소의 삭제

- `delete` : 요소의 값만 삭제
- `Array.prototype.splice` : 해당 요소를 완전히 삭제

```jsx
const numbersArr = ['zero', 'one', 'two', 'three'];

// 요소의 값만 삭제
delete numbersArr[2]; // (4) ["zero", "one", empty, "three"]
console.log(numbersArr);

// 요소 값만이 아니라 요소를 완전히 삭제
// splice(시작 인덱스, 삭제할 요소수)
numbersArr.splice(2, 1); // (3) ["zero", "one", "three"]
console.log(numbersArr);
```

## 배열의 순회

`forEach` 메소드, `for`문, `for...of` 문 사용하는 것을 권장

(`for...in`문 사용 시 불필요한 프로퍼티까지 출력될 수 있음)

```jsx
const arr = [0, 1, 2, 3];
arr.foo = 10;

for (const key in arr) {
  console.log('key: ' + key, 'value: ' + arr[key]);
}
// key: 0 value: 0
// key: 1 value: 1
// key: 2 value: 2
// key: 3 value: 3
// key: foo value: 10 => 불필요한 프로퍼티까지 출력

arr.forEach((item, index) => console.log(index, item));

for (let i = 0; i < arr.length; i++) {
  console.log(i, arr[i]);
}

for (const item of arr) {
  console.log(item);
}
```

## Array Property

### Array.length

`length` 프로퍼티는 요소의 개수(배열의 길이)를 나타냄

- `length` 프로퍼티 값은 명시적으로 변경 가능

  ⇒ 값을 현재보다 작게 변경 시 해당 값보다 크거나 같은 인덱스에 있는 요소들은 모두 삭제됨

- `length` 프로퍼티와 배열 요소의 개수가 일치하지 않는 경우도 존재함 ⇒ 희소 배열 (Sparse Array)

```jsx
const arr = [ 1, 2, 3, 4, 5 ];

console.log(arr.length); // 5

// 배열 길이의 명시적 변경
arr.length = 3;
console.log(arr); // (3) [1, 2, 3]
```

## Array Method

- ✏️ 메소드는 `this`(원본 배열)를 변경
- 🔒 메소드는 `this`(원본 배열)를 변경하지 않음

### Array.isArray(arg: any): boolean

: 주어진 인수가 배열이면 `true`,  배열이 아니면 `false` 반환

```jsx
// true
Array.isArray([]);
Array.isArray([1, 2]);
Array.isArray(new Array());

// false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(1);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
```

### Array.from

: 유사 배열 객체 또는 이터러블 객체를 변환하여 새로운 배열을 생성

```jsx
// 문자열은 이터러블이다.
const arr1 = Array.from('Hello');
console.log(arr1); // [ 'H', 'e', 'l', 'l', 'o' ]

// 유사 배열 객체를 새로운 배열을 변환하여 반환한다.
const arr2 = Array.from({ length: 2, 0: 'a', 1: 'b' });
console.log(arr2); // [ 'a', 'b' ]

// Array.from의 두번째 매개변수에게 배열의 모든 요소에 대해 호출할 함수를 전달할 수 있다.
// 이 함수는 첫번째 매개변수에게 전달된 인수로 생성된 배열의 모든 요소를 인수로 전달받아 호출된다.
const arr3 = Array.from({ length: 5 }, function (v, i) { return i; });
console.log(arr3); // [ 0, 1, 2, 3, 4 ]
```

### Array.of

: 전달된 인수를 요소로 갖는 배열 생성

```jsx
// 전달된 인수가 1개이고 숫자이더라도 인수를 요소로 갖는 배열을 생성
const arr1 = Array.of(1);
console.log(arr1); // // [1]

const arr2 = Array.of(1, 2, 3);
console.log(arr2); // [1, 2, 3]

const arr3 = Array.of('string');
console.log(arr3); // 'string'
```

### 🔒 Array.prototype.indexOf(searchElement: T, fromIndex?: number): number

: 원본 배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환

```jsx
const arr = [1, 2, 2, 3];

// 배열 arr에서 요소 2를 검색하여 첫번째 인덱스를 반환
arr.indexOf(2);    // -> 1
// 배열 arr에서 요소 4가 없으므로 -1을 반환
arr.indexOf(4);    // -1
// 두번째 인수는 검색을 시작할 인덱스이다. 두번째 인수를 생략하면 처음부터 검색한다.
arr.indexOf(2, 2); // 2
```

ES7에서 도입된 `Array.prototype.includes` 메소드로도 요소가 존재하는지 확인 가능

```jsx
const foods = ['apple', 'banana'];

if (!foods.includes('orange')) {
  // foods 배열에 'orange' 요소가 존재하지 않으면 'orange' 요소를 추가
  foods.push('orange');
}

console.log(foods); // ["apple", "banana", "orange"]
```

### 🔒  Array.prototype.concat(…items: Array<T[] | T>): T[]

: 인수로 전달된 값들(배열 또는 값)을 원본 배열의 마지막 요소로 추가한 새로운 배열 반환

배열을 전달받으면 배열을 해체하여 요소로 추가함

```jsx
const arr1 = [1, 2];
const arr2 = [3, 4];

// 배열 arr2를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환
// 인수로 전달한 값이 배열인 경우, 배열을 해체하여 새로운 배열의 요소로 추가한다.
let result = arr1.concat(arr2);
console.log(result); // [1, 2, 3, 4]

// 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환
result = arr1.concat(3);
console.log(result); // ["1, 2, 3]

//  배열 arr2와 숫자를 원본 배열 arr1의 마지막 요소로 추가한 새로운 배열을 반환
result = arr1.concat(arr2, 5);
console.log(result); // [1, 2, 3, 4, 5]

// 원본 배열은 변경되지 않는다.
console.log(arr1); // [1, 2]
```

### 🔒 Array.prototype.join(separator?: string): string

: 배열의 모든 요소를 문자열로 변환한 후 인수로 전달받은 값, 즉 구분자로 연결한 문자열을 반환함 (생략 가능)

```jsx
const arr = [1, 2, 3, 4];

// 기본 구분자는 ','이다.
// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 기본 구분자 ','로 연결한 문자열을 반환
let result = arr.join();
console.log(result); // '1,2,3,4';

// 원본 배열 arr의 모든 요소를 문자열로 변환한 후, 빈문자열로 연결한 문자열을 반환
result = arr.join('');
console.log(result); // '1234'
```

### ✏️ Array.prototype.push(…items: T[]): number

: 인수로 전달받은 모든 값을 원본 배열의 마지막에 요소로 추가하고 변경된 `length`값 반환

배열을 전달받은 경우 배열을 그대로 원본 배열의 마지막 요소로 추가함

```jsx
const arr = [1, 2];

// 인수로 전달받은 모든 값을 원본 배열의 마지막에 요소로 추가하고 변경된 length 값을 반환한다.
let result = arr.push([3, 4]);
console.log(result); // 4

// push 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [1, 2, 3, 4]
```

### ✏️ Array.prototype.pop(): T | undefined

: 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환함

빈 배열인 경우 `undefined` 반환

```jsx
const arr = [1, 2];

// 원본 배열에서 마지막 요소를 제거하고 제거한 요소를 반환한다.
let result = arr.pop();
console.log(result); // 2

// pop 메소드는 원본 배열을 직접 변경한다.
console.log(arr); // [1]
```

### ✏️ Array.prototype.reverse(): this

: 배열 요소의 순서를 반대로 변경함

```jsx
const a = ['a', 'b', 'c'];
const b = a.reverse();

// 원본 배열이 변경된다
console.log(a); // [ 'c', 'b', 'a' ]
console.log(b); // [ 'c', 'b', 'a' ]
```

### ✏️ Array.prototype.shift(): T | undefined

: 배열에서 첫 요소를 제거하고 제거한 요소를 반환함

빈 배열인 경우 `undefined` 반환

```jsx
const a = ['a', 'b', 'c'];
const c = a.shift();

// 원본 배열이 변경된다.
console.log(a); // a --> [ 'b', 'c' ]
console.log(c); // c --> 'a'
```

### 🔒 Array.prototype.slice(start=0, end=this.length): T[]

: 인자로 지정된 배열의 부분을 복사하여 반환함

인자를 전달하지 않는 경우 원본 배열의 복사본을 생성하여 반환함

**매개변수**

- start : 복사를 시작할 인덱스
- end : 옵션, 기본값은 `length` 값

```jsx
const items = ['a', 'b', 'c'];

// items[0]부터 items[1] 이전(items[1] 미포함)까지 반환
let res = items.slice(0, 1);
console.log(res);  // [ 'a' ]

// items[1]부터 items[2] 이전(items[2] 미포함)까지 반환
res = items.slice(1, 2);
console.log(res);  // [ 'b' ]

// items[1]부터 이후의 모든 요소 반환
res = items.slice(1);
console.log(res);  // [ 'b', 'c' ]

// 인자가 음수인 경우 배열의 끝에서 요소를 반환
res = items.slice(-1);
console.log(res);  // [ 'c' ]

res = items.slice(-2);
console.log(res);  // [ 'b', 'c' ]

// 모든 요소를 반환 (= 복사본(shallow copy) 생성)
res = items.slice();
console.log(res);  // [ 'a', 'b', 'c' ]

// 원본은 변경되지 않는다.
console.log(items); // [ 'a', 'b', 'c' ]
```

### ✏️ Array.prototype.splice(start: number, deleteCount=this.length-start, …items: T[]): T[]

: 기존 배열의 요소를 제거하고 그 위치에 새로운 요소를 추가함, 배열 중간에 새로운 요소를 추가할 때에도 사용

**매개변수**

- start : 배열에서의 시작 위치
- deleteCount : 시작 위치부터 제거할 요소의 수
- items : 삭제한 위치에 추가될 요소들

```jsx
const items = [1, 2, 3, 4];

// items[1]부터 2개의 요소를 제거하고 그자리에 새로운 요소를 추가한다. 제거된 요소가 반환된다.
const res = items.splice(1, 2, 20, 30);

// 원본 배열이 변경된다.
console.log(items); // [ 1, 20, 30, 4 ]
// 제거한 요소가 배열로 반환된다.
console.log(res);   // [ 2, 3 ]
```