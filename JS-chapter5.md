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
  8. 객체(Object)

<br><br><hr><br>
# 1. 변수(variable) & 값(Value)
  ### * 값
  : 프로그램에 의해 조작될 수 있는 대상 
  
  ### * 리터럴
  : 소스코드 안에서 직접 만들어 낸 상수 값 자체를 말하며 값을 구성하는 최소 단위
  - Variable이나 constants와 대조되는 개념

  ### * 변수
  : 값을 저장(할당)하고 저장된 그 값을 참조하고자 사용하며, 값이 저장된 메모리 공간의 주소를 가리키는 식별자(identifier)
  - <Strong>재활용성</Strong><br>
    : 한번 쓰고 버리는 게 아닌 유지가 필요한 값에 사용

  - <Strong>가독성</Strong><br>
    : 변수명을 통해 값의 의미를 쉽게 이해하고 가독성을 높일 수 있다.

  - <Strong>식별자</Strong><br> 
    : 변수는 메모리 주소에 접근하기 위해 사람이 이해할 수 있는 언어로 지정한 식별자이다.

  - <Strong>var와 =</Strong><br> 
    : 변수를 선언할 때에는 var를 사용하고, 변수에 값을 할당할 때에는 =을 사용한다.<br>
    ```
    var x; // 변수의 선언 <br>
    x=6; // 변수의 할당<br>
    ar y = 8; // 동시에 변수의 선언과 할당<br>
    ```
  - <Strong>동적 타이핑</Strong><br>
    : 변수를 선언할 때 데이터 타입을 미리 지정하지 않고, 할당된 값에 따라 동적으로 변수의 타입이 결정된다.

  ### * 데이터 타입
  : 프로그래밍 언어에서 사용할 수 있는 값의 종류<br>
  - 종류<br>
    * 원시 타입(Primitive data type)<br>
    1) <Strong>number</Strong><br>
      : 숫자를 나타내는 데이터 타입
        ```
        var num1 = 1001;
        var num2 = 10.50;
        ```<br>
    2) <Strong>string</Strong><br>
      : 문자열을 나타내는 데이터 타입
        ```
        var string1 = 'Hello';
        var string2 = "World";
        ```<br>
    3) <Strong>boolean</Strong><br>
      : 참 혹은 거짓을 나타내는 데이터 타입 <br>
        ```
        var bool1 = true;
        var bool2 = false;
        ```<br>
    4) <Strong>null</Strong><br>
      : 아무것도 참조하고 있지 않음을 명시할 때의 데이터 타입이자 값. <br>
        ```
        var foo = null;
        ```<br>
    5) <Strong>undefined</Strong><br>
      : 선언은 되었지만 값이 할당되진 않았을 때의 데이터 타입이자 값. <br>
        ```
        var bar;
        ```<br><br>
    * 객체 타입(Object data type)<br>
      --> 바로 아래 객체 파트에서 설명<br><br>
      
  ### * 객체 
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

  ### * 배열
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
    
# 2. 연산자(Operator)
# 3. 키워드(Keyword)
# 5. 주석(Comment)
# 6. 문(Statement) & 표현식(Expression)
# 7. 함수(Function)


