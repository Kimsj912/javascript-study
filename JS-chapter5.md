# 자바스크립트의 기본 문법
- Link : https://poiemaweb.com/js-syntax-basics
<br>

# Contents
  1. 변수(variable) & 값(Value)
  2. 연산자(Operator)
  3. 키워드(Keyword)
  5. 주석(Comment)
  6. 문(Statement) & 표현식(Expression)
  7. 함수(Function)


<br><br><br>
# 1. 변수(variable) & 값(Value)
  ### * 값
  : 프로그램에 의해 조작될 수 있는 대상 
  
  ### * 리터럴
  : 소스코드 안에서 직접 만들어 낸 상수 값 자체를 말하며 값을 구성하는 최소 단위
  - Variable이나 constants와 대조되는 개념

  ### * 변수
  : 값을 저장(할당)하고 저장된 그 값을 참조하고자 사용하며, 값이 저장된 메모리 공간의 주소를 가리키는 식별자(identifier)
  - <Strong>재활용성</Strong><br>
  - <Strong>가독성 향상</Strong><br>
  - <Strong>사람이 이해할 수 있는 언어로 지정한 식별자</Strong>
  - <Strong>선언은 var와 할당은 =</Strong>
  - <Strong>동적 타이핑</Strong><br>

  ### * 데이터 타입
  : 프로그래밍 언어에서 사용할 수 있는 데이터의 종류<br>
    
    - 원시 타입 (primitive data type)
      * boolean
      * null
      * undefined
      * number
      * string
      * symbol (ES6에서 추가)
      
    - 객체 타입 (object/reference type)
      * object
    
  - 자세한 내용은 https://github.com/mina-gwak/javascript-study/edit/main/JS-chapter6.md 에서 이어짐.
      
# 2.객체 
: 데이터를 의미하는 프로퍼티(property)와 데이터를 참조하고 조작할 수 있는 동작(behavior)을 의미하는 메소드(method)로 구성된 집합
- 원시 타입(Primitives)을 제외한 나머지 값들(함수, 배열, 정규표현식 등)은 모두 객체
- 자바스크립트의 함수는 일급 객체이므로 값으로 취급할 수 있다.
- 프로퍼티 값으로 함수를 사용할 수도 있으며 프로퍼티 값이 함수일 경우, 일반 함수와 구분하기 위해 메소드라 부른다.
- 데이터(프로퍼티)와 그 데이터에 관련되는 동작(메소드)을 모두 포함할 수 있기 때문에 데이터와 동작을 하나의 단위로 구조화할 수 있어 유용하다.
- 객체지향의 상속을 구현하기 위해 “프로토타입”이라고 불리는 객체의 프로퍼티와 메소드를 상속받을 수 있다.
```
  var person = {
  name: 'Lee',
  gender: 'male',
  sayHello: function () {
    console.log('Hi! My name is ' + this.name);
  }
};

console.log(typeof person); // object
console.log(person); // { name: 'Lee', gender: 'male', sayHello: [Function: sayHello] }

person.sayHello(); // Hi! My name is Lee
```

# 3. 배열
: 1개의 변수에 여러 개의 값을 순차적으로 저장할 때 사용하는 객체
#### 배열의 생성
```
let fruits = ['사과','바나나']
```
#### 배열에 접근
```
let last = fruits[1]
```
#### 배열의 항목 순환 처리
```
fruits.forEach(function (item, index, array) {
  console.log(item, index)
})
```
#### 배열 끝에 항목 추가
```
let newLength = fruits.push('오렌지')
```
#### 배열 끝의 항목 제거
```
let newLength = fruits.pop()
```
#### 배열 앞에 항목 추가
```
let newLength = fruits.unshift('딸기')
```
#### 배열 앞의 항목 제거
```
let first = fruits.shift()
```  
이외의 자세한 내용 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array
    
# 4. 연산자(Operator)
: 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입 연산 등을 수행해 하나의 값을 만드는 대상
- 연산자에 의해 연산되는 대상을 <b>피연산자(Operand)</b>라고 한다.
- 종류
  * 산술연산자
    : +,-,*,/,++,--,** 등 산술행위를 하는 연산자
    ```
    var width = 2 + 5;
    var height = 7 - 3;
    var area = width * height;
    var divided = area / 4;
    ```
    
  * 문자열 연결 연산자
    : 문자열을 연결하는 연산자
    ```
    var str = "My name is"+"Sujeong";
    ```
    
  * 할당연산자
    : =, +=, -=, *=, /=, &= 등을 통해 값을 할당하는 연산자
    ```
    var korean *= 2;
    var math +=30;
    var english -= 20;
    var avg = korean + enlgish + math;
    var avg /= 3
    ```   
    
  * 비교연산자
    : ==, !=, >, >=, <, <=  등 피연산자를 서로 비교하고, 비교 결과가 참인지에 따라 논리 값을 반환하는 연산자
    ```
    3 == '3'
    var1 != 4
    var2 >= var2
    var1 <= var2   
    ```
    
  * 논리연산자
    : &&, ||, ! 를 이용하여 보통 불리언(논리) 값과 함께 사용해서 불리언 값을 반환하는 연산자
    ```
    expr1 && expr2
    expr1 || expr2
    !expr
    ```
    
  * 타입연산자
    : 평가 전의 피연산자 타입을 나타내는 문자열을 반환하는 연산자
    ```
    다음과 같은 변수를 가정하겠습니다.
    var myFun = new Function("5 + 2");
    var shape = "round";
    var size = 1;
    var foo = ['Apple', 'Mango', 'Orange'];
    var today = new Date();
    
    typeof 연산자는 위의 변수들에 대해서 다음과 같은 값을 반환합니다.
    typeof myFun;     // "function" 반환
    typeof shape;     // "string" 반환
    typeof size;      // "number" 반환
    typeof foo;       // "object" 반환
    typeof today;     // "object" 반환
    typeof dontExist; // "undefined" 반환
    ```
    
  * 조건연산자 (혹은 삼항연산자)
    : 주어진 조건에 따라 두 값 중 하나를 반환하는 연산자
    ```
    var status = (age >= 18) ? "성인" : "미성년자";
    ```
  
  이외의 자세한 내용 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Expressions_and_Operators#assignment_operators
  
# 5. 키워드(Keyword)
: 미리 규정된 수행할 동작을 의미
- 클래스명이나 메소드명, 변수명으로 사용할 수 없다.
- 종류
  - 변수에서의 키워드
  : var를 통해 변수를 선언할 수 있다.
  ```
  // 변수의 선언
  var x = 5 + 6;
  ```
 
  - 함수에서의 키워드
  : function을 통해 함수를 선언하고, return을 통해 함수를 종료하며 값을 반환한다.
  ```
  // 함수의 선언
  function foo (arg) {
    // 함수 종료 및 값의 반환
    return ++arg;
  }
  ```

# 6. 주석(Comment)
: 작성된 코드의 의미를 설명하기 위해 사용
- 가독성을 높이기 위해 사용한다.
- 종류
  - 한 줄 주석
  ```
  // 한 줄 주석을 표현하기 위한 
  // 방법입니다.
  // 여러 줄을 쓰면 더 번거로워요.
  ```
  - 여러 줄 주석 
  ```
  /*
  여러줄을
  표현하기 위한
  주석 처리 방법
  */
  ```

# 7. 문(Statement) & 표현식(Expression)
## 문
: 컴퓨터가 수행할 프로그램을 구성하는 각각의 명령을 문이라고 부르며, 문이 실행되면 무슨 일인가가 일어나게 된다.
- 리터럴, 연산자, 표현식, 키워드, ; 등으로 구성된다.
- 코드블록 {...}으로 그룹화하여 함께 실행되어야하는 문을 정의할 수 있다.
- 위에서 아래로 순서대로 실행된다. 
  (if,switch, while, for 등으로 흐름을 제어하거나 함수를 호출함으로서 순서를 제어할 수 있다.)
- 함수 단위의 유효범위(Function-level scope)만이 생성된다.
  (다른 언어와 달리 자바스크립트는 블록 유효범위(Block-level scope)를 생성하지 않는다.)
```
var man = 10;
var woman = 15;

function myFunc(x,y){ return x+y;}
var total = myFunc(man,woman);

if (total !=20) 
  for(var i=0;i<total;i++){
    console.log(i+"명 째 오고 있어요.);
   }
else {
  console.log("20명이 있어요");
}
```

## 표현식
: 하나의 값으로 표현되는 식
- 다른 표현식의 일부가 되어 좀 더 복잡한 표현식을 구성할 수 있다.
- 값(리터럴), 변수, 객체의 프로퍼티, 배열의 요소, 함수 호출, 메소드 호출, 피연산자와 연산자의 조합은 모두 표현식이며 하나의 값으로 평가(Evaluation)된다.
```
5             // 5
5 * 10        // 50
5 * 10 > 10   // true
(5 * 10 > 10) && (5 * 10 < 100)  // true
```
## 문 vs. 표현식
문 -> 하나의 문장 / 컴퓨터에게 명령하여 무언갈 할 수 있다.
표현식 -> 문장의 구성요소 / 값을 만드는 것만 할 수 있다.


# 8. 함수(Function)
: 어떤 작업을 수행하기 위해 필요한 문(statement)들의 집합을 정의한 코드 블록
- 이름과 매개변수를 갖으며 필요한 때에 호출하여 코드 블록에 담긴 문들을 일괄적으로 실행할 수 있다.
- 탁월한 재사용성 
  - 여러번 호출할 수 있다.
  - 반복적으로 수행하는 부분을 함수로 정의하면 효율적이다.
```
// 함수의 정의(함수 선언문)
function square(number) {
  return number * number;
}

// 함수의 호출
square(2); // 4
```

