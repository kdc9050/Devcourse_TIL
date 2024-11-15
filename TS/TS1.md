#JS 복습

## 템플릿 문자열

```js
const str = "Hello";
const str2 = `${str} World`;
```

## 함수

- 함수 선언문
  - `ex) function add(a, b) { return a + b; }`
- 함수 표현식
  - 기명 함수
  - `ex) const add = function sum(a, b) { return a + b; }`
  - 익명 함수
  - `ex) const add = function(a, b) { return a + b; }`
- 화살표 함수 = 콜백 함수로 사용하기 위해서
  - `ex) const add = (a, b) => a + b;`

##비구조화 할당

- 배열
  - 비구조화 할당의 좋은 점 : 변수의 이름을 내 마음대로 지정할 수 있음
  - `ex) const likeFoods = ['apple', 'banana', 'orange'];`
  - `const [first, second, third] = likeFoods;`
  - `const [a, ...b] = likeFoods; // a = apple, b = ['banana', 'orange']`
- 객체

  ```js
  const { name: superName, age } = {
    name: "Jin",
    age: 20,
  };
  console.log(superName, age); // Jin 20
  ```

  ```js
  // 객체 안의 객체
  const userObj = {
    name: "철수",
    age: 20,
    address: {
      city: "Seoul",
      street: "Gangnam",
    },
    contact: {
      phone: "010-1234-5678",
      email: "chulsu@gmail.com",
    },
  };
  // 비구조화 할당
  const {
    name,
    age,
    address: { city, street },
    contact: { phone, email },
  } = {
    name: "철수",
    age: 20,
    address: {
      city: "Seoul",
      street: "Gangnam",
    },
    contact: {
      phone: "010-1234-5678",
      email: "chulsu@gmail.com",
    },
  };
  console.log(name, age, city, street, phone, email);
  ```

## 스프레드 연산자

- 전개 연산자로 사용

```js
const arr1 = [1, 2, 3];
const arr2 = arr1;
console.log(arr1 === arr2); //true
```

```js
const arr1 = [1, 2, 3];
const arr2 = [...arr1];
console.log(arr1 === arr2); // false
```

- 객체에서도 사용 가능
  - 객체 병합이 배열 병합과 다른 건 객체 병합은 뒤에 있는 객체의 속성이 덮어씌워짐

```js
const user1 = { name: "철수", age: 20 };
const user2 = { ...user1 };
console.log(user1 === user2); // false
```

```js
const user1 = { name: "철수", age: 20 };
const user2 = JSON.parse(JSON.stringify(user1));
console.log(user1 === user2); // false
```

# TypeScirpt

- npm ls -g --depth=0 // 글로벌로 설치된 패키지 확인
- 글로벌 패키지 지양 -g로 되어있는 거 비추
- npm uninstall -g [ts-node/ typescript 자신이 지우고 싶은거] 해서 글로벌을 지워줌 => 그 다음 tsc
- npm cache verify // 불필요한 캐쉬 파일을 자동 체크해서 삭제
- npm install typescript --save-dev
- npx tsc --init //
- package-lock.json 은 건들이면 안됨. 한 번더 검토해주는 것

- 정적 언어 (static) : .ts -> 컴파일러 -> .js (컴파일) => ts는 컴파일 단계에서 모든 게 결정됨. 이건 컴파일 과정에서 오류가 있는지 없는지 검사 가능.
- 동적 언어 (dynamic) : .js (런타임) 모든게 런타임에 결정됨 => 코드를 실행해 봐야 암.
- ts = js + type시스템
- npx -> node package excutor -> npm 패키지를 실행할 수 있게 해줌
- npx ts-node -> ts-node 알아서 실행, -> 자기가 설치까지 친절하게 안내함
- npx ts-node src/index.ts

## 타입스크립트 타입

- string (타입) 스트링 타입을 의 함

```js
let str: string = `hello, Typescript!`;
let emoji: string = `🤣`;
console.log(str);
```

- number (타입)

```js
let x: number = 10; //정수
let y: number = 3.14; //소수점
let z: number = NaN; //Not a Number
let a: number = -100; //음수
let b: number = Infinity; //무한대

let result: number = 0 / 0; //NaN
let positiveInfinity: number = 1 / 0; //Infinity
let negativeInfinity: number = -1 / 0; //-Infinity

//메서드에서도..
let pi: number = Math.PI;
let sqrt: number = Math.sqrt(16);
let ramdom: number = Math.random();
```

- boolean (타입)

```js
let isActive: boolean = true;
let isCompleted: boolean = false;
let isBigger: boolean = 10 > 20;
let boolTrue: boolean = JSON.parse("true"); //논리형으로 바꿔줌

// 0, "",NaN
let isZero: boolean = !!0; //false
let isEmpty: boolean = !!empty; //false
let empty: string = "";
let isNanValue: boolean = !!NaN; //false
```

- object (타입)
  - 굉장히 포괄성이 높은 타입임 => 사용에 주의가 필요함 => 실무에서는 많이 사용하지 않음
  - 기본 자료형 빼고 거의다 object로 표현 가능
  - 하나 문제점이 있음 => .으로 접근하면 에러가 남 => 정확하게 타입을 지정해줘야함

```js
let emptyObj: object = {};
let emptyArr: object = [];
let emptyFunc: object = function () {};

let userObj: object = { name: "철수", age: 20 };
console.log(userObj.name); //error

// 객체는 정확하게 타입을 지정해줘야함
let userObj: { name: string, age: number } = { name: "철수", age: 20 };
console.log(userObj.name); //철수
```

- array (타입)
  - array는 array라는 이름으로 사용할 수 없음
  - []를 사용해서 타입을 지정해줘야함 -> 신버전
  - Array<[]>을 사용해서 타입을 지정해줄 수 있음 -> 구버전
  - 구성요소가 있으면 안에 있는 요소가 무엇인지 따라서 정확하게 명시해줘야함.

```js
let empthArr: [] = [];
let emptyArr2: Array<[]> = [];

let numArr: number[] = [1, 2, 3];
let numArr2: Array<number> = [1, 2, 3]; //과거

let strArr: string[] = ["a", "b", "c"];
let strArr2: Array<string> = ["a", "b", "c"];

let fruits: sting[] = new Array("apple", "banana", "orange");
let fruits2: Array<string> = new Array("apple", "banana", "orange");

//튜플
let mixArr: [number, string, {}, number[]] = [1, "a", {}, [1, 2, 3]];

let nestedArr: number[][] = [
  [1, 2],
  [3, 4],
  [5, 6],
];
let nestedArr2: Array<Array<number>> = [
  [1, 2],
  [3, 4],
  [5, 6],
];

let userArr: { name: string, age: number }[] = [
  { name: "철수", age: 20 },
  { name: "영희", age: 21 },
];
let userArr2: Array<{ name: string, age: number }> = [
  { name: "철수", age: 20 },
  { name: "영희", age: 21 },
];
```

- 튜플 (tuple)
  - 배열의 길이가 고정되고 각 요소의 고유한 타입이 지정되어 있는 배열
  - 요소의 타입이 다를 수 있음

```js
//1
let mixArr: [number,string, {}, number[]] = [1,'a',{},[1,2,3]];

//2
let user: [string, number] = ['철수', 20];
user[0]= 10; //error
user[1] = '영희'; //error - 정확한 타입을 지정해줘야함

//3
let emptyArr: [] = []; // 빈 배열도 튜플의 한 종류
emptyArr.push(1); //error => 빈 배열이기 때문에 에러가 남 - 미리 정의된 타입만 들어갈 수 있음

//4
let user :[string, number, string?] = ['철수', 20]; // ?를 붙이면 선택적으로 사용할 수 있음 (옵셔널요소)
user = ['영희', 21, '서울']; // 가능
user.push("male");
```

- null & undefined (타입)

```js
let x: null = null;
let z: string = x ?? "test"; //null 병합 연산자 (??) => null이면 test를 넣어줌
let y: undefined = undefined;
```

- any (타입)
  - 모든 타입을 허용하는 타입
  - 일부러 모든 자료형을 다 허용하게 지정한 느낌
  - 타입스크립트의 타입 시스템을 사용하지 않는 것과 같음
  - Nest.js에서는 compile 실패함

```js
let x: any = [1, 2];
console.log(x[0]); //1
```

- unknown (타입)
  - 모든 타입을 허용하는 타입
  - 알 수 없을때 => 나중에 뭐가 들어갔는지 확인해야 함.
  - 실제 값을 사용할 때 타입을 검증해야함 any는 검증하지 않아도 됨

```js
let x: unknown = [1, 2];
console.log(x[0]); //error => unknown 타입이라서 에러가 남

//x가 무엇인지 모르기 때문에 타입을 정확하게 지정해줘야함
if (Array.isArray(x)) {
  console.log(x[0]); //1
} // 이렇게 해야함 => 이런 과정을 타입 가드라고 함
```
