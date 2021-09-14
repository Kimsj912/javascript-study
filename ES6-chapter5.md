// Link : https://poiemaweb.com/es6-enhanced-object-property

Contents
1. 프로퍼티 축약 표현
2. 프로퍼티 키 동적 생성
3. 메소드 축약 표현
4. __proto__ 프로퍼티에 의한 상속


1. 프로퍼티의 축약 표현
  - ES5 (기존)
    객체 리터럴의 프로퍼티는 <b>프로퍼티 이름</b>과 <b>프로퍼티 값</b>으로 구성된다.
    프로퍼티의 값으로 변수가 할당될 수도 있고 이를 아래처럼 표현한다.
    ```
    var x = 1, y = 2;

    var obj = {
      x: x,
      y: y
    };

    console.log(obj); // { x: 1, y: 2 }
    ```
    변수 x와 y를 프로퍼티 값으로 저장하고 그 이름 또한 x와 y일 때, es5는 번거롭지만 이름과 값 사이에 :를 두고 모두 기록을 해야했다.
    
    
  - ES6
    앞선 경우에서 es6는 <b><u>프로퍼티 이름을 생략(Property Shorthand)</u></b>할 수 있다.
    ```
    let x = 1, y = 2;

    const obj = { x, y };

    console.log(obj); // { x: 1, y: 2 }
    ```
    es6에서 프로퍼티 이름을 생략하여 변수를 사용할 경우 위와 같이 사용하고, <b>프로퍼티 이름 = 변수의 이름</b>이 된다.
  
2. 프로퍼티 키 동적 생성
  - ES5 (기존)
    키를 동적으로 생성할 때에는 문자열(또는 문자열로 반환 가능한 값)을 반환하는 표현식을 대괄호([...])로 묶어 사용 가능합니다. 이렇게 프로퍼티 키로 사용되기 위해 대괄호로 묶이는 문자열로 된 표현식을 </b>계산된 프로퍼티 이름(Computed Property Name)</b>이라고 합니다. ES5에서 동적으로 프로퍼티 키를 생성하는 방법은 다음과 같습니다.
    ```
    var prefix = 'prop';
    var i = 0;

    var obj = {};

    obj[prefix + '-' + ++i] = i; 
    obj[prefix + '-' + ++i] = i;
    obj[prefix + '-' + ++i] = i;

    console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
    ```
    obj에 []를 사용하여 prefix값인 'prop'와 0에서 1이된 i가 계산되어 문자열 "prefix-1"이 되고 이를 프로퍼티 이름, i의 값인 1이 프로퍼티 값으로 하여 동적으로 프로퍼티가 생성됩니다.
    
  - ES6
    ES5와 같은 내용을 `$ 를 이용하여 표현할 수 있습니다. 
    ```
    const prefix = 'prop';
    let i = 0;

    const obj = {
      [`${prefix}-${++i}`]: i,
      [`${prefix}-${++i}`]: i,
      [`${prefix}-${++i}`]: i
    };

    console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
    ```
    \`${}는 ES6부터 javascript에 도입된 <b>템플릿 리터럴</b>입니다.
      - 문자열 리터럴
        - 정의
          * 내장된 표현식을 허용하는 문자열 리터럴
          
        - 특징
          * 백틱키와 플레이스 홀더를 통해 문자열을 표현한다.
          * 플레이스 홀더 안에서의 표현식과 그 사이의 텍스트는 함께 함수로 전달된다.
          * 불필요한 + 기호의 반복을 줄여 가독성과 편의성을 높일 수 있다.
          * 템플릿 리터럴 안에서 백틱 문자를 사용하려면 백틱 앞에 백슬러쉬(\)를 넣어 사용할 수 있다.
          
        - 템플릿 리터럴 사용방법
          * ESC 키 아래 위치한 백틱(\`)키를 문자열 맨 앞에 위치 시키고 계산이 필요한 위치에 플레이스 홀더인 ${계산하는 식}을 이용해 표현식을 나타냅니다. 
          
          자세한 내용 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals

3. 메소드 축약 표현
  - ES5 (기존)
    기존의 ES5에서 메소드를 선언하기 위해서는 아래와 같이 프로퍼티 값으로 함수 선언식을 할당하여 사용합니다.
    ```
    var obj = {
      name: 'Lee',
      // 메소드(프로퍼티 값으로 사용되는 함수) 부분
      sayHi: function() { 
        console.log('Hi! ' + this.name);
      }
    };

    obj.sayHi(); // Hi! Lee
    ```
  - ES6
    이전과 달리 ES6에서는 메소드를 선언할 때 <b>Function키워드를 생략하여 표현</b>할 수 있습니다.
    ```
    const obj = {
      name: 'Lee',
      // 메소드가 축약되어 표현된 부분
      sayHi() {
        console.log('Hi! ' + this.name);
      }
    };

    obj.sayHi(); // Hi! Lee
    ```
    이를 통해 메소드의 표현 방식이 단순하고 이해하기 쉽게 변화됨을 알 수 있습니다.
    
4. __proto__ 프로퍼티에 의한 상속
  - ES5 (기존)
    객체 리터럴을 상속하기 위해서는 <b>프로토타입 패턴 상속</b>이라 하는 Object.create()함수를 사용해왔다. 
    ```
    var parent = {
      name: 'parent',
      sayHi: function() {
        console.log('Hi! ' + this.name);
      }
    };

    // 프로토타입 패턴 상속
    var child = Object.create(parent); 
    child.name = 'child';

    parent.sayHi(); // Hi! parent
    child.sayHi();  // Hi! child
    ```
    
  - ES6
    객체 리터럴 내부에서 __proto__ 프로퍼티를 직접 설정하여 다른 객체를 바인딩해 상속을 표현할 수 있다.
    ```
    const parent = {
      name: 'parent',
      sayHi() { // (깨알) 메소드 축약 표현
        console.log(`Hi! ${this.name}`); // (깨알) 문자열 리터럴
      }
    };

    const child = {
      // child 객체의 프로토타입 객체에 parent 객체를 바인딩하여 상속을 구현
      __proto__: parent,
      name: 'child'
    };

    parent.sayHi(); // Hi! parent
    child.sayHi();  // Hi! child
    ```
    위처럼 child의 __proto__에 연결할 객체를 넣어 parent와 child를 바인딩할 수 있다. 이를 통해 자식 객체가 object.create()로 부모객체의 복사본으로부터 시작하는 것이 아닌 자기자신의 객체를 만들고 부모객체를 연결해내는 방식으로 만들 수 있게 되었다.
