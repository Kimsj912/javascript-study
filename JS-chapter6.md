# 자바스크립트의 변수와 객체
// Link : https://poiemaweb.com/js-data-type-variable
<br>

# Contents
  #### 1. 정적 타입 언어와 동적 타입 언어(Static Type vs. Dynamic Type)
  <br>
  
  #### 2. 데이터 타입(Data Type)
  ##### - 원시 타입(Primitive Data Type)
  1. Number
  2. String
  3. Boolean
  4. Undefined
  5. Null
  6. Symbol 
  ##### - 객체 타입(Object Type/Reference Type)<br>
 <br>
 
  #### 3. 변수
  ##### - 특징
  ##### - 명명 규칙
  ##### - 선언
  ##### - 동적 타이핑(Dynamic Typing)
  ##### - 변수 호이스팅(Variable Hoisting) 

<br><br><hr><br>

# 1. 정적 타입 언어와 동적 타입 언어(Static Type/Strong Type vs. Dynamic Type/Weak Type)
  <table align="Center">
    <tr>
      <th>방식</th>
      <th>의미</th>
      <th>사용대상</th>   
    <tr>
      <th>정적 방식</th>
      <td>변수를 선언하며 변수에 <b>저장할 값의 종류를 사전에 지정</b></td>
      <td>C, java</td>
    </tr>
     <tr>
      <th>동적 방식</th>
      <td> 변수에 <b>값이 할당되는 과정에서 자동으로 변수의 타입이 결정</b>(타입 추론, Type Inference)된다.</td>
      <td> javaScript </td>
    </tr>
  </table><br><br>
  
  
# 2. 데이터 타입(Data Type)
: 프로그래밍 언어에서 사용할 수 있는 데이터의 종류<br>
- 데이터 타입은 데이터를 메모리에 저장할 때 확보해야 하는 메모리 공간의 크기와 할당할 수 있는 유효한 값에 대한 정보, 그리고 메모리에 저장되어 있는 2진수 데이터를 어떻게 해석할 지에 대한 정보를 컴퓨터와 개발자에게 제공
- 자바스크립트의 모든 값은 데이터 타입을 갖는다. 
- 종류
  <table align="Center">
    <tr>
      <th></th>      
      <th colspan='6'>원시 타입(Primitive Data Type)</th>
      <th>객체 타입(Object Type)</th>
    </tr>
    <tr>
      <th>방식</th>
      <th>Number</th>
      <th>String</th>
      <th>Boolean</th>
      <th>Undefined</th>
      <th>Null</th>
      <th>Symabol</th>
      <th>Object</th>
    </tr>
    <tr>
      <th>대상</th>
      <td>숫자</td>
      <td>문자열</td>
      <td>true/false</td>
      <td>참조되지 않음</td>
      <td>대상이 없음</td>
      <td>프로퍼티 키</td>
      <td>객체</td>
    </tr>
  </table><br><br>
  
* 원시 타입(Primitive data type)
  - immutable value(변경 불가능한 값)
  - pass-by-value(값에 의한 전달) 
  - 종류
    1) <Strong>number</Strong><br>
      : 숫자를 나타내는 데이터 타입
      - 주로 <b>산술 연산</b>을 위해 사용한다.
      - 보통의 언어들과 달리 <b>하나의 숫자타입</b>만 존재한다.
      - 모든 수를 <b>실수</b>로 처리한다.
      - -(2^53 -1) ~ (2^53 -1)
        ```
        var integer = 10;        // 정수
        var double = 10.12;      // 실수
        var negative = -20;      // 음의 정수
        var binary = 0b01000001; // 2진수
        var octal = 0o101;       // 8진수
        var hex = 0x41;          // 16진수
        console.log(octal === hex);    // true -> 진법에 따른 표현이 달라져도 같은 값으로 인식한다.
        ```
      - 무한대(Infinity)와 산술 연산 불가(Nan, Not a number)를 표현할 수 있다.
        ```
        var pInf = 10 / 0;  // 양의 무한대
        console.log(pInf);  // Infinity

        var nInf = 10 / -0; // 음의 무한대
        console.log(nInf);  // -Infinity

        var nan = 1 * 'string'; // 산술 연산 불가
        console.log(nan);       // NaN
        ```<br>
    2) <Strong>string</Strong><br>
      : 문자열을 나타내는 데이터 타입
      - 주로 텍스트로 출력하기 위해 사용한다.
      - 문자열은 0개 이상의 16bit <b>유니코드 문자(UTF-16)</b>들의 집합으로 대부분의 전세계의 문자를 표현할 수 있다. 
      - 작은 따옴표(‘’)(더 일반적으로 사용되는 편) 또는 큰 따옴표(“”) 안에 텍스트를 넣어 생성한다.
      - <b>자바스크립트의 문자열은 원시 타입이며 변경 불가능(immutable)</b>하다. 
        ```
        var string1 = 'Hello';
        var string2 = "World";
        ```<br>
      - 유사 배열
        - 배열처럼 인덱스를 통해 접근이 가능하다.
        - 이미 생성된 문자열의 일부를 변경해도 반영되지 않는다. (read only) 
          -> 새로운 문자열을 재할당하여 변경하도록 한다.
        ```
        str = 'String';
        console.log(str); // String

        str += ' test';
        console.log(str); // String test

        str = str.substring(0, 3);
        console.log(str); // Str
        ```
    3) <Strong>boolean</Strong><br>
      : 참 혹은 거짓을 나타내는 데이터 타입 <br>
      - 주로 조건문에서 흐름을 제어하기 위해 사용한다.
      - 비어있는 문자열과 null, undefined, 숫자 0은 false로 간주된다. 
        ```
        var bool1 = true;
        var bool2 = false;
        ```<br>

    4) <Strong>undefined</Strong><br>
      : 선언은 되었지만 값이 할당되진 않았을 때의 데이터 타입이자 값. <br>
      - 선언하지 않은 변수(undefined 변수)에 접근하면 ReferenceError가 발생한다.
      - 자바스크립트 엔진에 의해 초기화된 값
        - 변수 선언에 의해 확보된 메모리 공간을 처음 할당이 이루어질 때까지 빈 상태(대부분 비어있지 않고 쓰레기 값(Garbage value)이 들어 있다)로 내버려두지 않고 자바스크립트 엔진이 undefined로 초기화함으로써 사용된다.
        - 개발자가 사용하는건 권장하지 않음.
        ```
        var bar;
        ```<br><br>

    5) <Strong>null</Strong><br>
      : 아무것도 참조하고 있지 않음을 명시할 때의 데이터 타입이자 값. <br>
      - 의도적으로 변수에 값이 없다는 것을 명시할 때 사용한다.
      - 함수가 호출되었으나 유효한 값을 반환할 수 없는 경우, 명시적으로 null을 반환하기도 한다.
      - 자바스크립트는 대소문자를 구별(case-sensitive)하므로 <b>null은 Null, NULL등과 다르다.</b>
      - null 타입을 확인할 때 typeof 연산자를 사용하면 안되고 일치 연산자(===)를 사용하여야 한다.
        ```
        var foo = null;
        ```<br>

    6) <Strong>Symbol</Strong><br>
      : es6부터 도입된 객체의 프로퍼티를 만드는 원시 데이터 타입<br>
      - 주로 이름의 충돌 위험이 없는 유일한 객체의 프로퍼티 키(property key)를 만들기 위해 사용한다. 
      - Symbol 함수를 호출해 생성한다.
      ```
      // 심볼 key는 이름의 충돌 위험이 없는 유일한 객체의 프로퍼티 키
      var key = Symbol('key');
      console.log(typeof key); // symbol

      var obj = {};
      obj[key] = 'value';
      console.log(obj[key]); // value
      ```

* 객체 타입(Object data type)<br>
  --> https://github.com/mina-gwak/javascript-study/blob/main/JS-chapter5.md#2%EA%B0%9D%EC%B2%B4


# 3. 변수
: 값을 저장(할당)하고 저장된 그 값을 참조하고자 사용하며, 값이 저장된 메모리 공간의 주소를 가리키는 식별자(identifier)
- 특징
  - <Strong>재활용성</Strong><br>
    : 한번 쓰고 버리는 게 아닌 유지가 필요한 값에 사용
    ```
    3.141592653589793 * 2 * 2; // 12.566370614359172 -> 재사용 불가
    var circleArea = 3.141592653589793 * 2 * 2; -> 재사용 가능
    ```

  - <Strong>가독성</Strong><br>
    : 변수명을 통해 값의 의미를 쉽게 이해하고 가독성을 높일 수 있다.
    ```
    3; // 3의 의미를 알 수 없음. 
    var x = 3;        // x가 무슨 의미인지 알 수 없음.
    var score = 100;  // score가 점수를 의미한다는 걸 바로 알 수 있음.
    ```

  - <Strong>식별자</Strong><br> 
    : 변수는 메모리 주소에 접근하기 위해 사람이 이해할 수 있는 언어로 지정한 식별자이다.

  - <Strong>var와 =</Strong><br> 
    : 변수를 선언할 때에는 var를 사용하고, 변수에 값을 할당할 때에는 =을 사용한다.<br>
    ```
    var x; // 변수의 선언 <br> --> undefined로 초기값을 가짐.
    x=6; // 변수의 할당<br>
    var y = 8; // 동시에 변수의 선언과 할당
    ```
- 명명 규칙
  - 시작은 영문자, _, $로 시작하여야한다.(특수문자 제외 영문자, underscore, 달러기호)
  - 내용은 영문자, _, $, 숫자(0~9)를 사용할 수 있다.
  - 대소문자는 구별된다.
 
- 선언
  - 키워드
  <table align="Center">
    <tr>
      <th>구분</th>      
      <th>범위</th>
      <th>선언 전 사용</th>
      <th>재선언(중복선언)</th>
      <th>선언 시 초기값</th>
      <th>재할당</th>
    </tr>
    <tr>
      <th>var</th>
      <td>함수 레벨 스코프</td>
      <td>가능</td>
      <td>가능(이전 변수의 값을 덮어쓴다.)</td>
      <td rowspan="2">안줘도 OK</td>
      <td rowspan="2">가능</td>
    </tr>
    <tr>
      <th>let</th>
      <td rowspan="2">블럭 레벨 스코프</td>
      <td rowspan="2">에러 발생</td>
      <td rowspan="2">에러 발생</td>
    </tr>    
    <tr>
      <th>const</th>   
      <td>반드시 필요</td>
      <td>불가(단, 객체 내의 프로퍼티 변경은 막을 수 없다.</td>
    </tr>
  </table><br><br>  

- <Strong>동적 타이핑</Strong><br>
  : 변수를 선언할 때 데이터 타입을 미리 지정하지 않고, 할당된 값에 따라 동적으로 변수의 타입이 결정된다.
  ```
  var foo;
  console.log(typeof foo);  // undefined

  foo = null;
  console.log(typeof foo);  // object

  foo = {};
  console.log(typeof foo);  // object

  foo = 3;
  console.log(typeof foo);  // number

  // 같은 foo이지만 할당되는 값에 따라 데이터 타입이 결정됨.
  ```

- <Strong>변수 호이스팅(Variable Hoisting)</Strong>
