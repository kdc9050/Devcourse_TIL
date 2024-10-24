# JS

## **함수**

- `함수 선언문`

  - function 키워드로 시작

  ```js
  function 함수명(매개변수) {
    // 함수 몸체
  }
  함수명(인수);
  ```

- `함수 표현식` -> 값으로 평가될 수 있는 식

  - 함수를 변수에 할당

  ```js
  const 함수명 = function (매개변수) {
    // 함수 몸체
  };
  함수명(인수);
  ```

  - 함수 표현식은 함수 선언문과 달리 함수명을 생략할 수 있다.
  - `네이밍 함수(naming function)` : 함수 표현식에 함수명을 붙인 것
    ```js
    const 함수명 = function 함수명(매개변수) {
      // 함수 몸체
    };
    ```
  - `익명 함수(anonymous function)` : 함수명이 없는 함수 표현식
    ```js
    const 함수명 = function (매개변수) {
      // 함수 몸체
    };
    ```
    - `const`로 선언 하는 이유 : 함수의 가장 큰 특징은 재활용성인데 그래서 재할당을 방지하기 위해

- `화살표 함수` (ES6)
  - 깔끔하게 정리 가능 : `ex) const add = (a, b) => a + b;`
  ```js
  const 함수명 = (매개변수) => {
    // 함수 몸체
  };
  함수명(인수);
  ```
- 매개변수(parameter)를 사용하여 함수 재사용성을 높임
- 반환 값(return value)을 사용하여 함수의 결과를 외부로 전달
  ```js
  const 함수명 = (매개변수) => {
    // 함수 몸체
    return 반환 값;
  }; -> return을 생략하면 undefined를 반환
  const 결과 = 함수명(인수);
  //
  ```
- 함수 내부의 공간과 외부의 공간은 다르다.
- 함수 내부에서 선언한 변수는 함수 내부에서만 접근 가능하다.

- `가변인자`

  - 함수를 호출할 때 전달하는 인수의 개수가 가변적인 함수
  - 함수 정의 시 매개변수의 개수를 확정할 수 없을 때 사용
  - arguments 객체 또는 스프레드 연산자를 사용하여 가변 인자를 구현
  - arguments 객체

    - 유사 배열 객체로 함수 호출 시 전달된 인수들의 정보를 담고 있다.

    ```js
    function sum() {
      let sum = 0;
      for (let value of arguments) {
        sum += value;
      }
      return sum;
    }
    console.log(sum(1, 2, 3)); // 6
    ```

    - 화살표 함수에서는 arguments 객체를 사용할 수 없다.

  - 스프레드 연산자(...)
    - 전개연산자 또는 나머지 연산자
    - 배열이나 객체를 복사할 때 사용
    - 배열의 복사
    - 매개변수로 받지 않은 인수를 배열 형태로 나타낼 때 사용
    ```js
    const sum = (a, b, ...arrgs) => {
      let sum = 0;
      for (let value of arrgs) {
        sum += value;
      }
      return sum;
    };
    console.log(sum(1, 2, 3, 4, 5)); // 12
    ```

- `스코프` -> 식별자를 참조할 수 있는 범위

  - 함수 스코프와 블록 스코프 -> 지역 스코프
    - 함수 스코프 : 함수에서만 유효한 범위 -> 그래서 지역 스코프라고도 한다.
    - 블록 스코프 : let, const로만 선언 가능, {}사이에 작성된 부분을 block이라 함, 블록 내부에서만 유효한 범위 -> 그래서 지역 스코프라고도 한다.
      - 하위 블록에서 상위 블록의 변수에 접근 가능, 상위 블록에서 하위 블록의 변수에 접근 불가능
  - 전역 스코프
  - 지역 스코프에서 전역스코프 참조 가능
  - 전역 스코프에서 지역 스코프 참조 불가능

  ```js
  // 함수 스코프
  const a = 10;
  function print() {
    const b = 20;
    console.log(`함수 내부: ${a}, ${b}`); // 함수 내부: 10, 20
  }
  print();
  console.log(`함수 외부: ${a}, ${b}`); // 함수 외부: 10, b is not defined
  ```

  ```js
  // 블록 스코프
  const a = 10;
  {
    const b = 20;
    console.log(`블록 내부: ${a}, ${b}`); // 블록 내부: 10, 20
  }
  console.log(`블록 외부: ${a}, ${b}`); // 블록 외부: 10, b is not defined
  ```

- etc

  - 자바스크립트 설계상 오류
    - typeof로 null을 확인하면 object가 반환된다.
    - typeof로 배열을 확인하면 object가 반환된다.
  - 자바스크립트는 런타임 기반 언어
    - 즉 실행할 때 모든 것이 결정되는 동적 언어
    - 런타임 : 프로그램이 실행되고 있는 동안의 동작을 의미
    - 실행하기 전까지는 모름
  - 타입스크립트는 스태틱 기반 언어
    - 정적 언어 : 컴파일 시점에 타입을 검사하는 언어
  - 재귀 함수 - 실무, 다양하지 않음 x
    - 팩토리얼예제에서 제일 많이 나옴-> 자기 자신을 호출하는 함수
  - 두 가지 요소와 함께 만들어짐

    - 기저 사례 (base case)- 재귀 호출이 끝나는 조건이 명시되어 있는 코드
    - 재귀 호출 - 자기 자신을 다시 호출하는 함수

    ```js
    // 5 * factorial(4);
    // 4 * factorial(4);
    // 3 * factorial(4);
    //... <- 이게 아니라

    // 5 * factorial(4)
    // 5 * 4 * factorial(3);
    // 5 * 4 * 3 * factorial(2)
    // 5 * 4 * 3 * 2 * factorial(1)
    //... <- 이거임

    function factorial(n) {
      //기저 사례
      if (n === 0 || n === 1) return 1;
      // 재귀 호출
      return n * factorial(n - 1);
    }
    console.log(factorial(5));
    ```

## 객체

- 키와 값으로 이루어진 속성의 집합이다.
- 객체의 값을 동적으로 추가 하는 법


    ```js
    const obj = {};
    obj.key = value;
    ```

    ```js
    const score = {
    kor: 100,
    };
    score.eng = 90;
    ```
