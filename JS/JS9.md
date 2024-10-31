## ES6 Class 문법

- 객체지향언어 -> 전통적인 객체지향언어와 다르게 프로토타입 기반의 객체지향언어
- 클래스 기반 객체 지향 -> java, c++, c#
- 프로토타입 기반 객체 지향 -> javascript

## Class

- 프로토타입을 쉽게 사용하기 위한 Sugar Syntax(설탕 문법)
- 클래스에서 만든 메서드는 prototype에 추가됨
- 한 개의 생성자만 사용 가능함
- 생성자 함수에서는 prototype에 메서드를 추가해야 했지만 클래스에서는 클래스 내부에 메서드를 추가할 수 있음

```js
//클래스
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  } // 한 개의 생성자만 사용 가능
  getInfo() {
    console.log(this.name, this.age);
  } // 클래스에서 만든 메서드는 prototype에 추가됨
}
const person = new Person("John", 20);
person.getInfo();
console.log(person);
```

```js
//생성자 함수
function Person(name, age) {
  this.name = name;
  this.age = age;
  // this.getInfo = function() {
  //     console.log(this.name, this.age);
  // }//1
}
Person.prototype.getInfo = function () {
  console.log(this.name, this.age);
}; //2
const person = new Person("John", 20);
person.getInfo();
console.log(person);
```

### 번외 (일급 객체)

- 객체는 아니지만 객체로 취급이 되는 특징 , 특성, 것
- 함수 -> 일급 객체 / 배열 -> 일급 객체
- 클래스는 함수처럼 ()를 사용해서 호출이 가능함
- 클래스, 함수, 배열은 일급 객체
  - 1.변수에 할당이 가능해야함
  ```js
  const sum = function () {};
  ```
  - 2.함수의 인자로 전달이 가능해야함
  ```js
  funciton greet(callback) {
      callback();
  }
  greet(function() {
      console.log('Hello');
  }
  ```
  - 3.함수의 반환값으로 사용이 가능해야함
  ```js
  function outer() {
    return function () {
      console.log("Hello");
    };
  }
  const inner = outer();
  inner();
  ```
  - 4.동적으로 생성이 가능해야함
  ```js
  const dynamic = new Function("a", "b", "return a + b");
  console.log(dynamic(1, 2));
  ```
- 함수는 함수 -> Object
  - 함수를 특별한 이름으로 부리기도 함
  - 일급 객체 = 함수
  - 일급 객체 -> 특정 데이터가 객체로 취급되는 것
  - 함수는 함수라는 데이터. 그런데 JS에서는 객체로 취급됨
  - 일급 객체 취급 -> 함수와 클래스
- 배열도 일급 객체임

## 클래스의 상속

- extends 키워드를 사용하여 상속을 받을 수 있음
- super 키워드를 사용하여 부모 클래스의 생성자를 호출할 수 있음
- super 는 부모의 constructor를 호출함

```js
class Car {
  constructor(name) {
    this.name = name;
  }
  getInfo() {
    console.log(this.name);
  }
}
class SuperCar extends Car {
  constructor(name, power) {
    super(name);
    this.power = power;
  }
  getPower() {
    console.log(this.power);
  }
}
const superCar = new SuperCar("Ferrari", 500);
superCar.getInfo();
```

---

```js
// 생성자 함수 상속 call, Object.create 사용
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.greet = function () {
  console.log("Hello" + this.name + this.age);
};

function Employee(name, age, position) {
  Person.call(this, name, age);
  this.position = position;
}
Employee.prototype = Object.create(Person.prototype);
Employee.prototype.constructor = Employee;

Employee.prototype.getJob = function () {
  console.log("My job is " + this.position);
};
const developer = new Employee("철수", 20, "Web Developer");
developer.getJob();
developer.greet();
console.log(developer);
```

```js
// 위에 생성자 함수를 클래스 상속 - extends 사용
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  greet() {
    console.log("Hello" + this.name + this.age);
  }
}
class Employee extends Person {
  constructor(name, age, position) {
    super(name, age);
    this.position = position;
  }
  getJob() {
    console.log("My job is " + this.position);
  }
}
const developer = new Employee("철수", 20, "Web Developer");
developer.getJob();
developer.greet();
console.log(developer);
```

---

## 정적 메서드 정의 방법

- 인스턴스를 생성하지 않고 사용할 수 있는 메서드
- 클래스 내부에 static 키워드를 사용하여 정의
- 정적 메서드는 인스턴스를 생성하지 않아도 사용할 수 있음
- 불필요한 인스턴스 생성을 막아서 메모리를 절약할 수 있음

```js
class MathUtil {
  static add(a, b) {
    return a + b;
  }
}
const mathUtil = new MathUtil(); // 인스턴스 생성 필요 없음
const sum = MathUtil.add(1, 2);
console.log(sum);
```

```js
function MathUtil() {}
MathUtil.add = function (a, b) {
  return a + b;
};
const sum = MathUtil.add(1, 2); // 생성자 함수는 인스턴스 생성 필요 없음
console.log(sum);
```

## 접근 제어자 get, set

- 인스턴스 객체의 속성 값을 바꿀 때, 바꾸는 것을 제어하고 싶은 경우
- get -> 값을 가져올 때, set -> 값을 설정할 때

```js
class Car {
  constructor(speed) {
    this._speed = speed;
    this._color = "white";
  }
  set speed(value) {
    //this.speed = value < 0 ? 0 : value;
    // 2. Maximum call stack size exceeded -> 왜? -> this.speed = value; -> 무한루프
    this._speed = value < 0 ? 0 : value; // 다른 변수로 설정
  }

  get speed() {
    return this._speed; //
  }

  set color(value) {
    this._color = value === "white" ? "black" : value;
  }
  get color() {
    return this._color;
  }
}
const car = new Car(500, "red");
car.color = "white"; // black으로 설정
car.speed = -100; // 0으로 설정 -> set 메서드 호출 //1
console.log(car.speed);
console.log(car.color);
```

## 프라이빗 필드

- 클래스 내부에서만 사용할 수 있는 필드
- #을 사용
- 클래스 내부에서만 사용할 수 있는 필드를 만들어서 외부에서 접근하지 못하도록 제한할 수 있음

```js
class Counter {
  #count = 0;
  constructor() {
    this.#count = 0;
  }
  increase() {
    this.#count++;
  }
  decrease() {
    this.#count--;
  }
  getCount() {
    return this.#count;
  }
}
const count = new Counter(0);
count.count = 10;
count.increase();
count.increase();
console.log(count.getCount());
```

## 오버라이딩

- 부모 클래스의 메서드를 자식 클래스에서 재정의하는 것
- 부모 클래스의 메서드를 자식 클래스에서 재정의하여 사용할 수 있음

```js
class Animal {
  sound() {
    console.log("소리");
  }
}
class Dog extends Animal {
  sound() {
    console.log("멍멍");
  }
}
const dog = new Dog();
dog.sound();
```
