# 함수 타입

- 기본자료형과 참조 자료형에 타입을 붙이는 법
- 함수의 타입 -> 매개변수와 반환 값의 타입을 지정하는 것

```ts
//함수 선언문
function greet(name: string): string {
  return `Hello, ${name}!`;
}
// greet 함수는 string 타입의 매개변수를 받아 string 타입을 반환한다.

//함수 표현식
const greet = function (name: string): string {
  return `Hello, ${name}!`;
};

//화살표 함수
const greet = (name: string): string => {
  return `Hello, ${name}!`;
};
```

## 함수에서만 쓸 수 있는 타입

### void

- 함수가 아무것도 반환하지 않을 때 사용
- undefined와 void는 다르다.

```ts
function greet(name: string): void {
  console.log(`Hello, ${name}!`);
}

function sum(a: number, b?: number) {
  return a + (b || 0);
}
// b가 있을 수도 있고 없을 수도 있을 때
```

### callback 함수

```ts
function printUser(callback: (name: string) => void): void {
  callback("john");
}
printUser((name) => console.log(name));

const printUser = (callback: (name: string) => void): void => {
  callback("john");
};
printUser((name) => console.log(name)); // john

function findArray(
  arr: number[],
  condition: (item: number) => boolean,
  callback: (item: number) => void
): void {
  for (const item of arr) {
    if (condition(item)) {
      callback(item);
      return;
    }
  }
  console.log("not found");
}
findArray(
  [10, 20, 30, 40],
  (item) => item > 25,
  (result) => {
    console.log(result);
  }
);

//클로저
function createMultipler(factor: numver): (num: number) => number {
  return (num) => num * factor;
}
const func = createMultipler(2);
console.log(func(3)); //6
```

### never

- 절대 반환되지 않는 함수
- 에러를 던지거나 무한루프를 돌 때 사용

```ts
function showError(message: string): never {
  throw new Error(message);
}

function infLoop(): never {
  while (true) {}
}
```

## 타입 오퍼레이터(type operator)

- & : 교차 타입 (and), 인터섹션 타입(intersection), 타입스크립트에서는 한 개만 씀 다른곳에선 &&
- | : 합집합 타입 (or) , 유니온 타입(union)
  - 기본적으로 기본 타입에는 사용할 수 없음
  - 보통 객체에서 사용

```ts
//union
let value: string | number | boolean = 10;
value = "hello";
value = true;

let obj: { name: string; age: number } | { skill: string } = {
  name: "john",
  age: 30,
};
obj = { skill: "js" };

//intersection
// let value: string & number; //error
let value: { name: string; age: number } & { skill: string } = {
  name: "john",
  age: 20,
  skill: "js",
};
// 속성이 충돌되지 않게 개발자가 신경써서 작성해야함
```
