# Contents
  1. 블록문
  2. 조건문
  2.1. if..else문
  2.2. switch문
  3. 반복문
  3.1. for문
  3.2. while문
  3.3. do...while문
  4. break문

  <br><br><br>

# 1. 블록문

```
// 블록문
{
  var foo = 10;
  console.log(foo);
}

// 제어문
var x = 0;
while (x < 10) {
  x++;
}
console.log(x); // 10

// 함수 선언문
function sum(x, y) {
  return x + y;
}
console.log(sum(1, 2)); // 3
```


<br><br>

# 2. 조건문

  <h2>2.1. if..else 문</h2>
    : 주어진 조건식의 평가 결과에 따라 실행할 코드 블록을 결정한다.<br>
    만약 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환되어 논리적 참, 거짓을 구별한다.

    if (조건식1) {
      // 조건식1이 참이면 이 코드 블록이 실행된다.
    } else if (조건식2) {
      // 조건식2이 참이면 이 코드 블록이 실행된다.
    } else {
      // 조건식1과 조건식2가 모두 거짓이면 이 코드 블록이 실행된다.
    }
*else if는 옵션, 여러번 사용가능.

    //예제
    var num = 2;
    var kind;
    if (num > 0) {
      kind = '양수';
    } else if (num < 0) {
      kind = '음수';
    } else {
      kind = '영';
    }
    console.log(kind); // 양수

  - 삼항 조건 연산자로 바꿔쓸 수 있다.
    ```
    //if..else 문
    // x가 짝수이면 ‘짝수'를 홀수이면 ‘홀수'를 반환한다.
    var x = 2;
    var result;

    if (x % 2) { // 2 % 2는 0이고 0은 false로 취급된다.
      result = '홀수';
    } else {
      result = '짝수';
    }

    console.log(result); // 짝수
    ```

    ```
    //삼항 조건 연산자
    // x가 짝수이면 '짝수'를 홀수이면 '홀수'를 반환한다.
    var x = 2;

    // 0은 false로 취급된다.
    var result = x % 2 ? '홀수' : '짝수';
    console.log(result); // 짝수
    ```

  <br><br>

  <h2>2.2. switch 문</h2>

    : switch문의 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case문으로 실행 순서를 이동시킨다.

    switch (표현식) {
      case 표현식1:
        switch 문의 표현식과 표현식1이 일치하면 실행될 문;
        break;
      case 표현식2:
        switch 문의 표현식과 표현식2가 일치하면 실행될 문;
        break;
      default:
        switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
    }

  *break문 사용하기
  ```
  // 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = 'January';
  case 2:
    monthName = 'February';
  case 3:
    monthName = 'March';
  case 4:
    monthName = 'April';
  case 5:
    monthName = 'May';
  case 6:
    monthName = 'June';
  case 7:
    monthName = 'July';
  case 8:
    monthName = 'August';
  case 9:
    monthName = 'September';
  case 10:
    monthName = 'October';
  case 11:
    monthName = 'November';
  case 12:
    monthName = 'December';
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```

<br><br>

# 3. 반복문
  : 조건식이 거짓일 때까지 반복하여 코드 블럭을 실행한다.

  <h2>3.1. for문</h2>

  ```
  for (초기화식; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}

//예제
for (var i = 0; i < 2; i++) {
  console.log(i);
}
```
*()에 아무것도 선언하지 않는다면 무한루프

<br><br>

<h2>3.2. while문</h2>
: 조건식이 참이면 코드블럭을 계속해서 반복 실행한다.

```
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
  console.log(count);
  count++;
} // 0 1 2


// 무한루프
while (true) { }
```

<br><br>

<h2>3.3. do...while 문</h2>
: 코드블럭을 먼저 실행하고 조건식을 평가한다.

```
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
  console.log(count);
  count++;
} while (count < 3); // 0 1 2
```
<br><br>

# 4. break 문
: 반복문을 탈출할 때 사용한다.
```
var string = 'Hello World.';
var index;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 문자열의 개별 문자가 'l'이면
  if (string[i] === 'l') {
    index = i;
    break; // 반복문을 탈출한다.
  }
}

console.log(index); // 2
```

<br><br>

# 5. continue 문
: 반복문의 실행 중간에 다시 반복문의 시작점으로 돌아가게 한다.
```
var string = 'Hello World.';
var count = 0;

// 문자열은 유사배열이므로 for 문으로 순회할 수 있다.
for (var i = 0; i < string.length; i++) {
  // 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== 'l') continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}

console.log(count); // 3
```