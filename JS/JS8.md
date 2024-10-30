## 객체 복습

### get 키워드

- 함수가 아닌 속성처럼 사용 가능
- get은 매개변수를 받지 않는다.
- get은 반드시 무언가를 반환해야 한다.
- get은 값을 반환하는 함수를 만들어주는 역할을 한다.

### 계산된 속성

```js
const key = "name";
const obj = {
  [key]: "value",
};
```

### 즉시 실행 함수(IIFE)

- 함수를 선언하자마자 실행하는 함수
- 전역 범위를 오염시키고 싶지않을 때 사용함
- 한 번 호출되고 다시 부를 수 없음
- 메모리에서 즉시 제거됨

```js
//1
(function () {
  console.log("IIFE");
})();
//2
(() => {
  console.log("IIFE");
})();

(function greet(name) {
  console.log(`Hello ${name}`);
})("world");
```

## 생성자 함수

- 객체를 만드는 함수
- 함수이름은 파스칼 케이스로 작성 ex) User

```js
function User(name, age){ {
    this.name = name;
    this.age = age;
    this.getInfo = function(){
        return `name: ${this.name}, age: ${this.age}`;
}
const us = new User("kim",20);//생성자 함수로 객체 생성 -> 인스턴스
console.log(us);
console.log(us.getInfo());
```

## 프로토타입

- 함수와 1:1로 매칭이 되는 프라이빗한 공간
- 함수라면 무조건 가지고 있는 프로토타입 속성
- 메모리를 효율적으로 사용하기 위해 사용 -> 중복되는 함수를 프로토타입에 넣어줌
- 화살표 함수는 프로토타입이 없음
- 함수 선언문에서 사용

```js
// 위에 생성자 함수에 프로토타입 추가
function User(name, age){ {
    this.name = name;
    this.age = age;

}
User.prototype.getInfo = function(){
    return `name: ${this.name}, age: ${this.age}`;
}
const us = new User("kim",20);
console.log(us);
console.log(us.getInfo()); // 프로토타입에 있는 함수 호출
console.log(us.__proto__); // 프로토타입 확인
console.log(us.__proto__.getInfo); // 원래는 이렇게 쓰는데 생략이 가능함
console.log(us.hasOwnProperty('name')); // true -> hasOwnProperty를 어케 씀? -> 프로토타입 체인
```

- 프로토타입 체인(체이닝): 객체의 프로퍼티나 메소드에 접근할 때 객체의 프로토타입 체인을 따라 올라가면서 찾는 것
- 프로토타입 체인은 객체의 **proto** 속성을 통해 이루어짐
- 프로토타입 객체도 누군가의 인스턴스임
- 모든 객체는 Object의 인스턴스임

```js
funtion Object(){
this.hasOwnProperty = function(){}
this.propertyIsEnumerable = function(){}
this.isprotwtypeOf = function(){}
this.toString = function(){}
}
// this.hasOwnProperty = function(){} -> 프로토타입에 있는 함수
// this.propertyIsEnumerable = function(){} -> 프로토타입에 있는 함수'
```

## 래퍼객체(wrapper object)

- 일시적으로 기본 자료형을 객체로 만들어서 사용하는 것
- 자바스크립트 엔진이 기본 자료형의 값을 객체처럼 사용하기 위해서 암묵적으로 만드는 객체
- 래퍼객체 -> 그 자료형과 관련있는 생성자 함수의 인스턴스 객체로 감쌈
- 숫자다? Number() 생성자 함수로부터 객체를 만들어서 감싸줄게

```js
const Pt = 3.145192;
console.dir(Pt); // Number {3.145192}
console.log(Pt.toFixed(2)); // 3.15
```

## 객체지향

- 클래스 기반의 객체 지향 -> 자바, 파이썬 -> 클래스를 만들고 그 클래스로 객체를 만듬
- 프로토타입 기반의 객체 지향 -> 자바스크립트 -> 객체를 만들고 그 객체를 프로토타입으로 만듬

## 프로토타입 예제

```js
function Calculator() {}

Calculator.prototype.add = function (a, b) {
  return a + b;
};
Calculator.prototype.sub = function (a, b) {
  return a - b;
};
Calculator.prototype.mul = function (a, b) {
  return a * b;
};
Calculator.prototype.div = function (a, b) {
  return a / b;
};

const instance = new Calculator();
console.log(instance.add(1, 2));
console.log(instance.sub(1, 2));
```

```js
function Counter() {
  this.count = 0;
}
Counter.prototype.increase = function () {
  this.count++;
};
Counter.prototype.decrease = function () {
  this.count--;
};
Counter.prototype.getCount = function () {
  return this.count;
};
const counter = new Counter();
counter.count = 100;
console.log(counter.getCount());
counter.increase();
console.log(counter.getCount());
```

## 고급 패턴

### 생성자 함수를 프라이빗 패턴

- 프로토타입으로 뺄 수는 없음 이렇게 만들면

```js
function Counter() {
  let count = 0;

  this.increase = function () {
    count++;
  };
  this.decrease = function () {
    count--;
  };
  this.getCount = function () {
    return count;
  };
}
const counter = new Counter();
counter.count = 100; // 영향을 주지 않음
console.log(counter.getCount()); // 0
counter.increase();
console.log(counter.getCount()); // 1
```

```js
// 은닉화 전
function BankAccount(initialBalance) {
  this.balance = initialBalance;
}
BankAccount.prototype.deposit = function (amount) {
  this.balance += amount;
};
BankAccount.prototype.withdraw = function (amount) {
  this.balance -= amount;
};
const account = new BankAccount(1000);
console.log(account.balance);
account.deposit(500);
account.balance = 1000000;
console.log(account.balance);
```

```js
// 은닉화 후
function BankAccount(initialBalance) {
  let balance = initialBalance;

  this.deposit = function (amount) {
    balance += amount;
  };
  this.withdraw = function (amount) {
    balance -= amount;
  };
  this.getBalance = function () {
    return balance;
  };
}
const account = new BankAccount(1000);
console.log(account.getBalance());
account.deposit(500);
account.balance = 1000000;
console.log(account.getBalance());
```

### 생성자 함수 팩토리 패턴

```js
function createPerson(type) {
  function Employee(name) {
    this.name = name;
    this.type = "employee";
  }
  function Manager(name) {
    this.name = name;
    this.type = "manager";
  }

  switch (type) {
    case "employee":
      return new Employee(name);
    case "manager":
      return new Manager(name);
  }
}
const p1 = createPerson("employee");
const p2 = createPerson("manager");
console.log(p1);
console.log(p2);
```

### 상속 패턴

- 프로토타입 체인을 이용한 상속

```js
function Person(name) {
  this.name = name;
}
Person.prototype.introduce = function () {
  return `I am ${this.name}`;
};
function Developer(name, position) {
  Person.call(this, name);
  this.position = position;
}
Developer.prototype = Object.create(Person.prototype);
Developer.prototype.constructor = Developer; // constructor란? -> 생성자 함수를 가리키는 속성
Developer.prototype.skill = function () {
  return "react.js";
};
const dev = new Developer("kim", "junior");
console.dir(dev);
console.log(dev.introduce());
console.log(dev.skill());
```

```

```
