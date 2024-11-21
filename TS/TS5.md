## 타입 단언 (Type Assertion)

- 타입스크립트한테 개발자가 타입을 알려주는 기능
- 타입스크립트 엔진보다 내가 더 타입을 잘 알고 있을 때 사용
- 타입가드 -> 타입을 좁혀주기 위해 => 런타임에 타입을 확인해주는 원리
- 타입단언 <>, as
  - 타입 단언을 하므로써 발생하는 모든 에러는 개발자의 책임
  - 웹 api 같이 별도의 api를 사용할 때 많이 사용함

```ts
let value: unknown = "hello";
(<string>value).toUpperCase(); // 요즘은 이 방법을 잘 사용하지 않음
(value as string).toUpperCase(); // 요즘은 이 방법을 잘 사용함
```

```ts
//WEB API를 사용했을 때, 타입을 제대로 추론하지 못하는 경우
const button = document.getElementById("myButton");
(button as HTMLElement).click();
//옵셔널 체이닝 연산자(자바스크립트에서도 사용가능)
button?.click();
//널 아님 보장 연산자(타잆스크립트에서만 사용가능)
button!.click();
```

```ts
// 널 병합 연산자
// 변수나 표현식이 null or undefined일 때 대체 값을 제공하는 방법
let foo: string | null = null;
let foo2 = foo ?? "default value"; //null , undefined
let foo3 = foo || "default value2"; //null, undefined, false, 0, NaN, ""
```

## enum

- 열거형 타입
- 고정된 값들의 집합을 정의하는데 사용
- `enum` 키워드 사용
- 열거형도 병합이 가능
  - 같은 이름의 열거형을 여러번 선언할 수 있음
  - 병합된 열거형은 모든 열거형의 값들을 하나의 열거형으로 합침
  - 그런데, 열거형의 값이 중복되면 안됨
- `숫자 열거형`
  - 열거형의 값이 숫자인 경우, 값을 지정하지 않으면 0부터 시작
  - 값을 지정하면 그 값부터 시작
  - 역방향 추적도 가능 -> ex) Direction[0] = "Up"
- `문자열 열거형`
  - 열거형의 값이 문자열인 경우, 값을 지정하지 않으면 문자열 값이 그대로 할당

```ts
// 숫자 열거형
enum Direction {
  Up, // 0
  Down,// 1
  Left,
  Right,
}
console.log(Direction.Up); // 0
console.log(Direction.Down); // 1

enum Direction {
  Up, // 0
  Down =20,// 20
  Left, // 21
  Right, // 22
}
console.log(Direction.Up); // 0
console.log(Direction.Down); // 20

function move(direction: Direction) {
  switch (direction) {
    case Direction.Up:
      console.log("You moved up!");
      break;
    case Direction.Down:
      console.log("You moved down!");
      break;
    case Direction.Left:
      console.log("You moved left!");
      break;
    case Direction.Right:
      console.log("You moved right!");
      break;
    default:
      const _exhaustiveCheck: never = direction;
  }
```

```ts
// 문자열 열거형
enum Gender {
  Male = "Male",
  Femal = "Female",
}
type User = {
  name: string;
  gender: Gender;
};
const user: User = {
  name: "John",
  gender: Gender.Male,
};
```

### const enum

- 컴파일 결과에서 열거형을 제거하고, 실제 사용되는 곳에 직접 값을 삽입
- 성능 최적화를 위해 사용
- 열거형의 값이 변하지 않아야 함
- 그냥 enum을 쓰면 enum 객체가 생성되어서 메모리를 차지함
- 실무에서는 이렇게 사용하는 경우가 많음

## 제네릭 (Generics)

- 코드의 재사용성을 증가 시키기 위해서 사용하는 것, 치환(값을 대체하는 것)
- 해당 값의 타입이 여러개 일 때 유용하게 사용
- 제네릭은 어렵진 않지만, 어떻게 사용하는지에 대해 떠올리기가 어려움

```ts
// 인터페이스 + 제네릭
interface User<T> {
  name: string;
  value: T;
}
const user: User<"option"> = {
  name: "John",
  value: "option",
};
```

```ts
// 함수 + 제네릭
// 함수 제네릭은 타입 추론이 가능
function getFirestElement<T>(arr: T[]): T {
  return arr[0];
}
console.log(getFirestElement([1, 2, 3])); // 1
console.log(getFirestElement(["a", "b", "c"])); // "a"
console.log(getFirestElement<string>(["a", "b", "c"])); // "a"
```

```ts
//1. 함수 선언부에 제네릭을 선언
// const getFirestElement = <T>(arr: T[]): T => arr[0]; // 화살표 함수로도 가능

//2. 함수 선언부에 제네릭을 선언
// const getFirestElement: <T>(arr: T[]) => T = (arr) => arr[0]; // 타입을 명시적으로 지정 , 변수에 타입을 지정

//3. 타입 별칭, 인터페이스로 제네릭을 선언
type FirsthFunc = <T>(arr: T[]) => T; // 타입 별칭으로도 가능
interface FirsthFunc {
  <T>(arr: T[]): T;
} // 인터페이스로도 가능
const getFirestElement: FirsthFunc = (arr) => arr[0];
```

```ts
function mergeObjects<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}
const merged = mergeObjects(
  { name: "me", age: 10 },
  { jobTitle: "developer", salary: 2000 }
);
console.log(merged); // { name: 'me', age: 10, jobTitle: 'developer', salary: 2000 }
```

### 제네릭 제약

- 너무나 폭 넓은 재사용성을 가지게 해줘서 문제가 될 때도 있음
  - 다른 건 다 쓰고 싶은데 이건 안 쓰고 싶을 때
  - 제네릭 조건 타입
  - 제네릭을 사용할 때, 타입을 제한하는 방법
    - T extends U ? X : Y
    - extends 뒤에 있는 것만 사용 가능

```ts
// 제네릭 제약1
function getFirstElement<T extends number | string>(arr: T[]): T {
  return arr[0];
}
console.log(getFirstElement([1, 2, 3])); // 1
console.log(getFirstElement(["a", "b", "c"])); // "a"
console.log(getFirstElement([true, false])); // 에러
```

```ts
// 제네릭 제약2
function getFirstElement<T extends { length: number }>(arr: T[]): T {
  return value.length;
}
console.log(getFirstElement([1, 2, 3])); // 3
console.log(getFirstElement(["a", "b", "c"])); // 3
console.log(getFirstElement(10)); // 에러
```

```ts
// 제네릭 제약3
type Nameable = { name: string };
type Ageable = { age: number };

function printUserInfo<T extends Nameable & Ageable>(user: T): void {
  console.log(`name: ${user.name}, age: ${user.age}`);
}
printUserInfo({ name: "John", age: 30 }); // name: John, age: 30
```

### 객체 속성 값 반환 함수

- keyof 객체의 키를 추출해서 유니온 타입으로 만들어줌

```ts
function getProperty<T extends object, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

// K extends "name"
console.log(getProperty({ name: "John" }, "name"));
// K extends "name" | "age"
console.log(getProperty({ name: "John", age: 30 }, "name")); // John
```

```ts
// 객체 속성 값 업데이트 함수
function updateProperty<T extends object, K extends keyof T>(
  obj: T,
  key: K,
  value: T[K]
) {
  obj[key] = value;
  return obj;
}
const car = { brand: "Hyundai", model: "Sonata", year: 2020 };
console.log(updateProperty(car, "year", 2021)); // { brand: 'Hyundai', model: 'Sonata', year: 2021 }
```

## ts 클래스

- TS 클래스는 속성에 타입을 적용해야 한다.
- 접근제어자, public, private, protected
  - 접근제어자는 기본적으로 public
  - public: 클래스 내부, 클래스 외부 모두 접근 가능
  - private: 해당 클래스 내부에서만 접근 가능, 클래스 외부에서 접근 불가능
  - protected: 클래스 내부에서 사용, 클래스 외부에서 사용 불가능, 서브 클래스에서만 접근 가능(상속받은 클래스에서만 접근 가능)

```ts
class Car {
  public speed: number;
  constructor(speed: number) {
    this.speed = speed;
  }
  getSpeed() {
    return this.speed;
  }
}
const Car = new Car(100);
console.log(Car.getSpeed());
```

### 추상 클래스(abstract class)

- 추상 클래스는 인스턴스를 만들 수 없는 클래스
- 단순이 정의!
- extends로 상속받는 키워드는 오직 하나

```ts
abstract class CarAbstract {
  abstract name: string;
  abstract color: string;
  abstract start(): string;
  printInfo() {
    console.log(`name: ${this.name}, color: ${this.color}`);
  }
}
class Car extends CarAbstract {
  name: string;
  color: string;
  constructor(name: string, color: string) {
    super();
    this.name = name;
    this.color = color;
  }
  start() {
    return "Car is started";
  }
}
const car = new Car("Sonata", "Black");
car.start();
car.printInfo();
```

### 인터페이스 , type

- 타입이나 인터페이스 둘 다 상관 없음
- 무조건 구현해야 하는 것
- 클래스에서 구현할 때는 implements 키워드 사용
- 인터페이스는 다중 상속 가능

````ts
interface Moveable{
  move(): {
    console.log("move");
  };
}
interface Driveable{
  drive(): {
    console.log("drive");
  };
}

class Car implements Moveable, Driveable{
  speed: number;
  constructor(speed: number){
    //super();
    this.speed = speed;
  }
  move(){
    console.log("move");
  }
  drive(){
    console.log("drive");
  }
}

### 제네릭 클래스

```ts
class Box<T>{
  value: T;
  constructor(value: T){
    this.value = value;
  }
  getValue(): T{
    return this.value;
  }
}
const box = new Box<string>("Hello");
// const box = new Box("Hello");// 자동으로 타입 추론도 가능
console.log(box.getValue());
const box2 = new Box<number>(10);
console.log(box2.getValue());

// 제네릭 클래스 상속
class StringBox extends Box<T>{
  constructor(value: T){
    super(value);
  }
  printString(){
    console.log("stringBox");
  }
}

const stringBox = new StringBox("Hello");
const stringBox2 = new StringBox<string>("Hello");
````

### 추상 제네릭 클래스

```ts
abstract class Container<T> {
  abstract value: T;
  abstract getValue(): T;
}
class Box extends Container<string> {
  value: string;
  constructor(value: string) {
    super();
    this.value = value;
  }
  getValue() {
    return this.value;
  }
}
const box = new Box("Hello");
```

### 보너스 (알면 좋은 것)

## 유틸리티 타입

- 특정 기능을 하도록 미리 정의해둔 타입
- 엄청 많음 쓸모있는 몇 가지
  - Partial<T>: T의 모든 속성을 optional로 만듦
    - ex) interface User { name: string; age: number; }
    - Partial<User> => { name?: string; age?: number; }
  - Required<T>: T의 모든 속성을 필수로 만듦
    - ex) interface User { name?: string; age?: number; }
    - Required<User> => { name: string; age: number; }
  - Readonly<T>: T의 모든 속성을 readonly로 만듦
    - Readonly<User> => { readonly name: string; readonly age: number; }
  - Pick<T> : 내가 원하는 속성만 뽑아서 타입을 만들어줌
    - Pick<User, "name"> => { name: string }
  - Omit<T> : 내가 원하는 속성만 제외하고 타입을 만들어줌
    - Omit<User, "name"> => { age: number }
