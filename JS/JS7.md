## 객체

- 키와 값으로 구성된 속성의 집합
- 객체는 중괄호 {}로 감싸서 만들 수 있습니다.

## 참조 자료형

- 동적으로 추가 -> 객체의 속성에 접근해서 값을 할당
- 동적으로 삭제 -> delete 키워드 사용해서 특정 속성을 삭제
- 데이터를 정의하는 데 있어서 간편하게 데이터를 정의할 수 있는 방법을 리터럴 표기법이라고 함
  - 리터럴 표기 법 => 모든 데이터를 표기할 때 사용하는 표기법
- 객체리터럴 표기법 => `const obj = {name: 'Lee', age: 20};  // const obj = new Object({name: 'Lee', age: 20});`
- 배열리터럴 표기법 => `const arr = [1, 2, 3];  // const arr = new Array(1, 2, 3);`
- 문자열리터럴 표기법 => `const str = 'Hello'; // const str = new String('Hello');`
- 불리언리터럴 표기법 => `const bool = true;  // const bool = new Boolean(true);`
- 숫자리터럴 표기법 => `const num = 1;  // const num = new Number(1);`
- null리터럴 표기법 => `const n = null;  // const n = new Object(null);`
- symbol리터럴 표기법 => `const sym = Symbol();  // const sym = new Symbol();`

```js
const userObj1 = {
  name: "Lee",
  age: 20,
};
const userObj2 = new Object();
userObj2.name = "Lee";
userObj2.age = 30;
console.log(userObj);
```

## 객체 접근, 수정, 삭제

- 객체의 속성에 접근하는 방법
- 마침표 표기법 => `console.log(userObj.name);` //기본적으로 사용
- 대괄호 표기법 => `console.log(userObj['name']);` // 키가 공백이나 특수문자가 있는 경우 사용
- 객체 속성을 수정하는 방법 <-> 동적으로 속성을 추가하는 방법
- 객체 속성을 삭제하는 방법
- delete 키워드 사용 => `delete userObj.name;`
- 객체 내장 메서드
- hasOwnProperty 메서드 => 객체가 특정 속성을 가지고 있는지 확인
- `console.log(userObj.hasOwnProperty('name'));`

## this 키워드

- 예약이 되어져 있는 키워드
- 나(함수)를 호출한 객체를 가리키는 키워드 (함수 선언문)
- dir 메서드를 사용하면 객체의 속성을 확인할 수 있음
- window 객체는 전역 객체로서 브라우저에서 사용되는 객체
- window 객체는 생략이 가능함 => `getName();` == `window.getName();`
- this 주의할 점
- 화살표 함수에서 this 쓰려면 -> 그 함수가 선언된 스코프(어휘적 스코프)를 가리킴
- this 쓸 거면 그냥 화살표 함수는 쓰지 말자.

```js
const userObj = {
  name: "Lee",
  age: 20,
  getName: function (prefix) {
    return prefix + this.name;
  },
};
const greet = userObj.getName("Hello, ");
console.log(greet);
```

## 객체를 반복할 수 있는 (순회)방법

- for in문 => 객체의 속성을 순회하는 방법
- Object.keys 메서드 => 객체의 키를 배열로 반환
- Object.values 메서드 => 객체의 값을 배열로 반환
- Object.entries 메서드 => 객체의 키와 값을 배열로 반환

```js
const userObj = {
name: 'Lee',
age: 20,
};
//1
for (let key in userObj) {
console.log(key, userObj[key]);
}

//2
const keys = Object.keys(userObj);
for (let value of keys) {
console.log(userObj[value]);
}
//2-1
Object.keys(userObj).forEach(key => {
console.log(userObj[key]);

//3
const values = Object.values(userObj);
values.forEach(value => {
console.log(value);
});

//4
const entries = Object.entries(userObj);
entries.forEach(entry => {
const [key, value] = entry;
console.log(key, value);
});
```

## 객체 병합과 복사

- `앝은 복사(shallow copy)` => 객체, 배열
- `깊은 복사(deep copy)` => 기본 자료형
- 깊은 복사 -> 얕은 복사 // 불가능
- 얕은 복사 -> 깊은 복사 // 가능

```js
const userObj = {
  name: "Lee",
  age: 20,
};
const copyUser = { ...userObj };
userObj.name = "Kim";
console.log(userObj, copyUser);
```

- `객체 병합`
  - 객체안에 객체를 병합할 때는 얕은 복사로 병합됨

```js
const userObj = {
  name: "Lee",
  age: 20,
};
const developer = {
  skills: "js",
};
const person = { ...userObj, ...developer };
console.log(person);
```

```js
// 객체안에 객체를 병합
const user = {
  name: "철수",
  age: 20,
  today: { eat: "meat" },
};
const user2 = { ...user };
user.today.eat = "vegitable";
console.log(user, user2);
// {name: "철수", age: 20, today: {eat: "vegitable"}} {name: "철수", age: 20, today: {eat: "vegitable"}}
```

- 중첩되 있는 것 까지 완벽하게 복사하려면? -> 객체를 JSON으로 변환
- JSON.stringify 메서드 => 객체를 JSON 문자열로 변환
- JSON.parse 메서드 => JSON 문자열을 객체로 변환

```js
const user = {
  name: "철수",
  age: 20,
  today: { eat: "meat" },
};
const user2 = JSON.parse(JSON.stringify(user));
user.today.eat = "vegitable";
console.log(user, user2);
```

- lodash 라이브러리를 사용하면 깊은 복사를 쉽게 할 수 있음
- `_.cloneDeep` 메서드를 사용하면 깊은 복사를 할 수 있음

## 배열 복사

```js
const arr = [1, 2, 3];
const copyArr = [...arr];
arr[0] = 100;
console.log(arr, copyArr);
```

```js
const arr = [{ name: "철수" }, { name: "영희" }];
const copyArr = JSON.parse(JSON.stringify(arr));
arr[0].name = "민수";
console.log(arr, copyArr);
```

## 데이터 속성 설명자

- 객체 데이터 속성을 설명하는 것
- value, writable, enumerable, configurable
- 객체 데이터 속성을 정의할 때는 Object.defineProperty 메서드를 사용
  - `Object.defineProperty(객체, 속성, {value: 값, writable: true, enumerable: true, configurable: true});`

```js
const user = {};
object.defineProperty(user, "name", {
  value: "Lee",
  writable: true,
  enumerable: true,
  configurable: true,
});
// value: 'Lee' => 속성값,
// writable: true => 속성값 변경 가능
// enumerable: true => 순회할 때 접근 가능한 속성(특정 속성을 감출 수 있음)
// configurable: true => 설정을 바꿀 수 있는지 여부, 속성을 삭제할 수 있는지 여부
```

## 접근 속성 설명자

- get, set
- get -> 속성값을 가져올 때 호출되는 메서드
- set -> 속성값을 설정할 때 호출되는 메서드

```js
const user = {
  firstname: "Lee",
  lastname: "Dc",

  get fullname() {
    return `${this.firstname} ${this.lastname}`;
  },
  set fullname(name) {
    const splitNames = name.split(" ");
    this.firstname = splitNames[0];
    this.lastname = splitNames[1];
  },
};
user.fullname = "Kim";
console.log(user.fullname);
```

## 추가적으로 사용할 수 있는 메서드 - 불변성을 유지하는 메서드

- `Object.seal 메서드` => 객체의 속성을 추가하거나 삭제하는 것을 막음
- `Object.preventExtensions 메서드` => 객체의 속성을 추가하는 것을 막음
- `Object.freeze 메서드 =>` 객체의 속성을 변경하는 것을 막음

## `메서드 체이닝`

- 객체의 메서드를 연결해서 사용 할 수 있다.

```js
const calculator = {
value: 0,
add: function(n1){
 this.value += n1;
  return this;// 이건 무조건 this를 반환해야함
}
subtract: function(n1){
 this.value -= n1;
  return this;// 이건 무조건 this를 반환해야함
}
getReult; function(){
 return this.value;  // 이건 무조건 this를 반환해야함
}
};
const result = calculator.add(10).subtract(5).getResult();
console.log(result);
// 자기 자신을 내보내야 함
```

## 메서드

- foreach
  - 배열의 각 요소에 대해 주어진 함수를 실행
  - `arr.forEach(요소, 인덱스, 배열) => {실행문}`
- reduce
  - 배열의 각 요소에 대해 주어진 함수를 실행하고 하나의 결과값을 반환
- `arr.reduce((누적값, 현재값, 인덱스, 요소) => {return 결과값}, 초기값)`

```js
const arr = [1, 2, 3, 4, 5];
const result = arr.reduce((acc, cur) => acc + cur, 0);
console.log(result);
```
