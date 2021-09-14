# Contents
  1. 디스트럭처링 (Destructuring)
  2. 배열 디스트럭처링 (Array Destructuring)
  3. 객체 디스트럭처링 (Object Destructuring)
<br><br>

# 1. 디스트럭처링
  - 정의
    : 구조화된 배열이나 객체를 개별적인 변수에 할당하는 것.
    
  - 특징
    - 배열 또는 객체 리터럴에서 필요한 값만을 추출하여 변수에 할당/반환하기에 유용하다.
    - ex. 
      ```
      var thirdVal = arr[3];
      var name = obj.firstName;
      ```
  
# 2. 배열 디스트럭처링
  - ES5 (이전)
    - ES5에서는 배열을 디스트럭처링할 때 다음처럼 사용했습니다.
    ```
    var arr = [1, 2, 3];

    var one   = arr[0];
    var two   = arr[1];
    var three = arr[2];

    console.log(one, two, three); // 1 2 3
    ```
    하지만 이는 값이 많아지거나 새로 저장하고픈 변수의 이름이 다양하면 배열을 만들어 for문을 사용하거나 직접 적어줘야하는 불편함이 있습니다.
    
  - ES6
    - ES6에서는 배열의 각 요소를 배열로부터 추출하여 변수 리스트에 할당합니다. 
    ```
    const arr = [1,2,3];
    
    const [one,two,three] = arr;
    
    console.log(one, two, three);
    ```
    - 과정 설명
      - ES5와 달리 디스트럭처링 과정이 매우 짧게 표현되었습니다. 설명을 첨가하자면, 각 배열의 인덱스에서 값을 하나씩 가져와 변수 one, two, three에 저장하는 대신 arr의 인덱스를 기준으로 arr에서 값을 추출하고 one,two,three에 값을 할당하는 과정이 `const [one, two, three] = arr;`에서 이뤄졌습니다.
    - 특징
      - 배열에서 필요한 요소만 추출하여 변수에 할당하고 싶은 경우에 유용합니다.
      ```
      const today = new Date(); // Tue May 21 2019 22:19:42 GMT+0900 (한국 표준시)
      const formattedDate = today.toISOString().substring(0, 10); // "2019-05-21"
      
      // ES5
      var todayStringArr = formattedDate.split('-');
      const year = todayStringArr[0];
      const month = todayStringArr[1];
      const day = todayStringArr[2];

      console.log([year, month, day]); // [ '2019', '05', '21' ]
      
      // ES6
      const [year, month, day] = formattedDate.split('-');
      
      console.log([year, month, day]); // [ '2019', '05', '21' ]
      
      ```
    - 선언과 할당
      - 선언과 할당을 따로 해도 되고 한번에 해도 상관이 없습니다.
      ```
      let x, y, z;
      [x, y, z] = [1, 2, 3];

      // 위의 구문과 동일하다.
      let [x, y, z] = [1, 2, 3];
      ```
    - 더 다양한 케이스 예시
      ```
      let x, y, z;

      [x, y] = [1, 2];
      console.log(x, y); // 1 2

      [x, y] = [1];
      console.log(x, y); // 1 undefined

      [x, y] = [1, 2, 3];
      console.log(x, y); // 1 2

      [x, , z] = [1, 2, 3];
      console.log(x, z); // 1 3

      // 기본값
      [x, y, z = 3] = [1, 2];
      console.log(x, y, z); // 1 2 3

      [x, y = 10, z = 3] = [1, 2];
      console.log(x, y, z); // 1 2 3

      // spread 문법
      [x, ...y] = [1, 2, 3];
      console.log(x, y); // 1 [ 2, 3 ]
      ```
          

# 3. 객체 디스트럭처링
  - ES5 (이전)
    프로퍼티 이름(키)를 이용해 디스트럭처링하여 변수에 값을 할당했다.
    ```
    var obj = { firstName: 'Ungmo', lastName: 'Lee' };

    var firstName = obj.firstName;
    var lastName  = obj.lastName;

    console.log(firstName, lastName); // Ungmo Lee
    ```
    
  - ES6
    - 프로퍼티 이름(키)을 기준으로 객체의 디스트럭처링이 이뤄지고 값이 할당된다.
    - 순서는 의미가 없다
      ```
      const obj = { firstName: 'Ungmo', lastName: 'Lee' };

      // 변수 lastName, firstName가 선언 -> obj(initializer(초기화자))가 Destructuring(비구조화, 파괴)되어 할당
      const { lastName, firstName } = obj;

      console.log(firstName, lastName); // Ungmo Lee
      ```
    - default value 설정
      - 객체의 프로퍼티 prop1과 prop2를 디스트럭처링한다. 
      - 다음과 같은 방법으로 prop3의 디펄트 값을 'c'로 할당한다.
      ```
      const { prop1, prop2 } = { prop1: 'a', prop2: 'b' };
      console.log({ prop1, prop2 }); // { prop1: 'a', prop2: 'b' }

      // default value
      const { prop1, prop2, prop3 = 'c' } = { prop1: 'a', prop2: 'b' };
      console.log({ prop1, prop2, prop3 }); // { prop1: 'a', prop2: 'b', prop3: 'c' }
      ```
      
    - 필요한 프로퍼티 값만 추출
      - Arrays.prototype.filter 메소드를 이용하여 대상 배열의 요소를 받고 필요한 프로퍼티만 추출하여 비교한다.
      ```
      const todos = [
        { id: 1, content: 'HTML', completed: true },
        { id: 2, content: 'CSS', completed: false },
        { id: 3, content: 'JS', completed: false }
      ];

      // todos 배열의 요소인 객체로부터 completed 프로퍼티만을 추출한다.
      const completedTodos = todos.filter(({ completed }) => completed);
      console.log(completedTodos); // [ { id: 1, content: 'HTML', completed: true } ]
      ```
      - 위에서는 todos의 요소를 하나씩 순회하며 completed 프로퍼티의 값이 true인 것만  completedTodos에 담는다.
      
    - 중첩 객체의 경우
      - 중괄호({...})를 중첩하여 디스트럭처링한다. 
      ```
      const person = {
        name: 'Lee',
        address: {
          zipCode: '03068',
          city: 'Seoul'
        }
      };

      const { address: { city } } = person;
      console.log(city); // 'Seoul'
      ```
      

# 마무리 정리
  - 디스트럭처링(Destructuring) = 배열이나 객체를 파괴하여 변수에 할당하는 것.
  - 배열의 디스트럭처링
    ```
    var 변수명 = 배열[인덱스]; ...(n까지 반복) 
    ```
    ```
    const {변수명1, 변수명2, ... 변수명n} = 배열;
    ```
  - 객체의 디스트럭처링
    ```
    //ES5
    var 변수명 = 객체명.프로퍼티이름; ... (n개의 프로퍼티이름을 모두 적어 반복)
    ```
    ```
    //ES6
    const {변수명1, 변수명2, ... 변수명n} = {변수명1:프로퍼티값1, 변수명2:프로퍼티값2, ... 변수명n:프로퍼티값n};
    ```

// Ref Link : https://poiemaweb.com/es6-destructuring
