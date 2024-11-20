## 타입스크립트 사용이유

- 런타임 기반의 자바스크립트 언어를 정적기반의 언어로 지원함으로써 코드의 안정성을 높이기 위해서
- 정적 기반? => 정적 타입을 자바스크립트에 추가하기 위해서 타입스크립트가 만들어졌음
- 런타임 타입(런타입 언어, JS)=> 코드가 실행되는 동안에 타입을 결정하는 언어
- 정적 타입(TS) => 코드가 실행되기 전에 타입을 결정하는 언어
- 컴파일 => 하나의 형식을 다른 형식으로 변환하는 과정
- 컴파일러 => 컴파일을 수행하는 프로그램, 도구

## 되돌아보기

- `any` -> 모든 타입 허용
- `unknown` -> `any`와 비슷하지만 사용할 때 타입을 확인하고 사용
- `tuple` -> 고정된 수의 요소를 가진 배열의 타입을 지정할 때 사용하는 것
- `타입 표명` -> 타입을 명시적으로 지정하는 법 -> `let 변수명: 타입 = 값`
- `타입 추론` -> 타입을 명시하지 않아도 타입을 추론하는 것 -> `let 변수명 = 값`
- `union` -> |를 사용하여 여러 타입을 지정하는 것 -> `let 변수명: 타입1 | 타입2 = 값`
- `intersection` -> &를 사용하여 여러 타입을 지정하는 것 -> `let 변수명: 타입1 & 타입2 = 값`
- `타입 별칭` -> 타입을 새로운 이름으로 지정하는 것 -> `type 새로운타입 = 타입`
- `옵셔널` -> ?를 사용하여 선택적으로 사용할 수 있는 것

## 객체에서 사용할 수 있는 특별한..

### readonly

- 읽기 전용 속성을 설정하는 것
- `readonly` 키워드를 사용하여 설정

```ts
const user: {
  readonly name: string;
  age: number;
} = {
  name: "John",
  age: 20,
};
user.name = "Jane"; // error
```

- 배열이나 튜플 -> 읽기 전용으로 바꾸기도 함
  - 변수를 완전히 상수로 바꾸는 것

```ts
const arr: readonly number[] = [1, 2, 3];
arr[0] = 4; // error
arr.push(4); // error
```

### 인덱스 시그니처

- 객체의 속성을 동적으로 추가할 때 사용하는 것
- 키와 값이 같을 때 사용 => `[key: string]: string`

```ts
const user:{
  age: number;
  [key: string]: string;
}= {
  name: "John",
  gender: "male",
  age: "20",
  address: "seoul",
  }
}
```

## 타입 별칭(type alias)++

- 나만의 타입을 정의할 때 사용
- `type` 키워드를 사용하여 정의

```ts
//객체 타입 별칭
type User = {
  name: string;
  age: number;
};
const user: User = {
  name: "John",
  age: 20,
};
```

```ts
//함수 타입 별칭
type SumFunc = (n1: number, n2: number) => number;
const sum: SumFunc = function (n1, n2) {
  return n1 + n2;
};
```

```ts
// 제네릭 => 코드의 재사용성을 높이기 위해 사용
// 관용적으로 T라는 이름을 사용
// <T, U, V> => 여러개의 제네릭을 사용할 때 => Type, Universal, Value
type Car<T> = {
  name: string;
  color: string;
  option: T;
};
const car: Car<string> = {
  name: "sonata",
  color: "black",
  option: "auto",
};
const car2: Car<number> = {
  name: "sonata",
  color: "black",
  option: 2,
};
const car3: Car<{ giftcard: boolean }> = {
  name: "sonata",
  color: "black",
  option: { giftcard: true },
};
```

```ts
// 튜플 타입 별칭
type Point = [number, number];
const point: Point = [10, 20]; //좌표
```

```ts
// 인터섹션 타입 별칭
type Nameable = { name?: string };
type Ageable = { age?: number };
type Person = Nameable & Ageable &{
  gender?: string;
}
const person: Person = {
  name: "John
  age: 20
}
```

```ts
// 리터럴 타입 별칭
// 나타낸 값만 사용할 수 있음
type Direction = "left" | "right" | "top" | "bottom";
const dir: Direction = "left";
```

```ts
// 조건부 타입 별칭
// T extends U ? X : Y => T가 U를 확장하면 X를 사용하고 아니면 Y를 사용
type IsStringType<T> = T extends string ? "yes" : "no";
const test1: IsStringType<string> = "yes";
const test2: IsStringType<number> = "no";
```

```ts
// 키 선택 타입 별칭
// keyof => 객체의 속성을 가져올 때 사용
// 키를 추출해서 유니온으로 묶어서 값으로 반환
type Person = {
  name: string;
  age: number;
  address: string;
};
type PersonKey = keyof Person; // "name" | "age" | "address"
const key: PersonKey = "name";
```

```ts
// 인덱스 시그니처 타입 별칭
type UserMap = {
  name: string;
  [key: string]: string;
};
let users: UserMap = {
  name: "John",
  gender: "male",
  address: "seoul",
};
users.name = "Jane"; //
```

## 인터페이스(interface)

- 객체의 타입을 정의할 때 사용
- 리드온리, 인덱스 시그니처, 옵셔널은 인터페이스에서도 사용 가능 => 인터페이스에서만 사용한게 아니라 객체 타입이라 사용 가능한 것
- 기본형식 => `interface 이름 { 속성: 타입 }`
- `인터페이스 vs 타입 별칭` => 인터페이스는 확장이 가능하고 타입 별칭은 확장이 불가능
- 인터페이스는 자동 병합이 됨
  - `선언 병합(Declaration Merging)` => 같은 이름의 인터페이스를 여러번 선언할 때 자동으로 병합

```ts
//1. 기본 형식
interface User {
  name: string;
  age: number;
}
cosnt user: User = {
  name: "John",
  age: 20
}
```

```ts
//2. 옵셔널
interface User {
  name: string;
  age?: number;
}
cosnt user: User = {
  name: "John"
}
```

```ts
//3. readonly
// 튜플이나 배열 -> 변수를 상수(읽기전용)
// 객체-> 속성을 상수(읽기전용)
interface User {
  name: string;
  readonly age: number;
}
cosnt user: User = {
  name: "John",
  age: 20
}
user.age = 30; // error
```

```ts
//4. 인덱스 시그니처
// 객체의 속성을 동적으로 추가할 때 사용
interface User {
  name: string; //고정 속성
  [key: string]: string; //인덱스 시그니처
}
const user: User = {
  name: "John",
  gender: "male",
};
user.name = "Jane"; // 자동완성의 편의성을 위해 고정 속성을 먼저 작성
```

```ts
//5. 함수 타입
//타입
type SumFunc = (a: number, b: number) => number;
const sum: SumFunc = (a, b) => a + b;

//인터페이스
interface ISumFunc {
  (a: number, b: number): number;
}
const sum2: ISumFunc = (a, b) => a + b;
// 근데 인터페이스로는 거의 지정하지 않음
```

### 선언 병합(Declaration Merging)

- 같은 이름의 인터페이스를 여러번 선언할 때 자동으로 병합
- auto merge !!!

```ts
interface User {
  name: string;
}
interface User {
  age: number;
}
const user: User = {
  name: "John",
  age: 20,
};
```

### 인터페이스 확장 (extends)

- 인터페이스를 확장할 때 사용 (상속)
- `extends` 키워드 사용

```ts
//interface
interface Shape {
  color: string;
}
interface Circle extends Shape {
  radius: number;
}
const circle: Circle = {
  color: "red",
  radius: 10,
};

//type
type Shape = {
  color: string;
};
type Circle = Shape & {
  radius: number;
};
const circle: Circle = {
  color: "red",
  radius: 10,
};
```

```ts
interface Person{
  name: string;
  age: number;
}
interface Address{
  city: string;
  zipcode: string;
}
const person: Person = {
  name: "John",
  age: 20
}
interface Employee extends Person, Address {
  employeeId: number;
}
const employee: Employee = {
  name: "Jane",
  age: 30,
  employeeId: 1
  city: "seoul",
  zipcode: "10000"
}
```

```ts
interface Animal {
  name: string;
  //sound: () => void;
  sound(): void;
}
interface Pet extends Animal {
  //play: () => void;
  // play?(): void;
  play(): void;
}
const dog: Pet = {
  name: "dog",
  sound() {
    console.log("bark");
  },
  play() {
    console.log("play");
  },
};
// dog.play(); // play?() 면 에러
if (dog.play) dog.play(); // 이렇게 해야함
```

```ts
// 상속 + 제네릭
//1
interface Container<T> {
  value: T;
}
interface Box<T> extends Container<T> {
  label: string;
  scale?: T;
}

const contaniner: Container<number> = {
  value: 10,
};
const box: Box<number> = {
  label: "grid box",
  value: 10,
  scale: 10,
};

//2
interface Container<T> {
  value: T;
}
interface Box<T, U> extends Container<U> {
  label: string;
  scale?: T;
  inStock?: U;
}

const contaniner: Container<number> = {
  value: 10,
};
const box: Box<number, boolean> = {
  label: "gird box",
  value: true,
  scale: 10,
};
```
