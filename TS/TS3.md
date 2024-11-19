## 11.18 복습

- 기본 자료형 : number, string, boolean, null, undefined, symbol
- 참조 자료형 : [],{},()=> void
- 타입 오퍼레이터 : 유니온타입 | or , 인터섹션 & and

  - 유니온타입 : 서로 다른 타입 중 한 개, 여러 타입을 하나의 변수에 할당 할 수 있게 된다는 것

    - 주의 할 점 : `toUpperCase()`

    ```ts
    function print(value: string | number): void {
      console.log(value.toUpperCase());
    } // 에러 발생

    function print(value: string | number): void {
      //타입 가드 : 코드에서 값의 타입을 좁히거나 확실하게 추론할 수 있도록 도와주는 방법
      if (typeof value === "string") {
        console.log(value.toUpperCase());
      } else {
        console.log(value);
      } // 에러 발생하지 않음
    }
    ```

  - 인터섹션 : 모두 만족하는 타입을 할당 할 수 있게 된다는 것
    - 객체에서 활용
    - any랑 결합하면 any가 된다.
    - never랑 결합하면 never가 된다.
    ```ts
    let value: { name: string } & { age: number } = {
      name: "happy",
      age: 10,
    };
    ```
    }

  ## 함수 오버로드

  - 함수의 이름은 같지만 매개변수와 반환 타입이 다른 여러 함수를 가질 수 있다.
  - 함수 오버로드를 사용하면 자바스크립트의 함수처럼 여러 타입을 받아 처리할 수 있다.

  ```ts
  function combine(a: number | string, b: number | string): number | string {
    if (typeof a === "string" && typeof b === "string") return `${a}${b}`;
    if (typeof a === "number" && typeof b === "number") return a + b;
    throw new Error("둘 다 문자열이거나 숫자여야 합니다.");
  }
  const result = combine(1, "a");
  console.log(result.toUpperCase()); // 에러 발생
  ```

  ```ts
  //1
  function combine(a: number, b: number): number; //오버로드 시그니처
  function combine(a: string, b: number): string; //오버로드 시그니처
  function combine(a: number, b: string): string; //오버로드 시그니처
  function combine(a: string | number, b: string | number): string | number {
    if (typeof a === "string" && typeof b === "string") return `${a}${b}`;
    if (typeof a === "number" && typeof b === "number") return a + b;
    throw new Error("둘 다 문자열이거나 숫자여야 합니다.");
  }
  const result = combine(1, 10);
  console.log(result.toFixed(2));
  ```

  ```ts
  //2
  function showInfo(name: string, age: number): string;
  function showInfo(age: number): string;
  function showInfo(name: string, age?: number): string {
    if (age) {
      return `name: ${name}, age: ${age}`;
    } else {
      return `age: ${name}`;
    }
  }
  console.log(showInfo("happy", 10));
  console.log(showInfo(10));
  ```

  ## 타입 추론(Type Inference)

  - 변수의 할당된 값으로 타입을 추론하는 것
  - 매개변수에 기본값을 지정하면 any가 된다.
  - 변수를 선언할 때, 타입을 명시하지 않더라도 TS가 자동으로 타입을 추론하는 것
    - `ex) let num = 10;`

  ## 타입 표명(Type Annotation)

  - 타입 추론의 반대 개념
  - 변수의 타입을 명시적으로 선언하는 것
    - `ex) let num: number = 10;`

  ## 타입 별칭 (Type Alias)

  - 나만의 타입을 정의할 수 있다.
  - type 키워드를 사용하여 첫 번째 문자를 대문자로 작성한다.

  ```ts
  type MyType = name: string, age: number;
  let user: MyType = {
    name: "happy",
    age: 10
  }
  ```

  # 리터럴 타입

  - 리터럴 타입은 값으로 추론 해주는 것을 말함.
  - let으로 선언 하는 이유?
    - const는 타입추론이 안된다. => 값으로 타입을 추론하기 때문에 => const 로 할당된 값은 영원히 바꾸지 못해서

  ```ts
  let num1 = 10;
  let num2 = 10;
  //타입추론이 된다.
  ```

  ```ts
  const num1 = 10;
  const num2 = 10;
  //타입추론이 안된다.
  ```

  ```ts
  const num1: 10 = 10;
  const arr: [1, 2, 3] = [1, 2, 3];
  arr.push(4); //에러 발생
  //리터럴 타입을 사용하면 값을 타입으로 사용할 수 있다.
  ```
