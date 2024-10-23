## 1. 반복문

- 지정한 조건이 참(true)으로 평가되는 동안 지정된 블록문을 반복 실행할 때 사용하는 문법
- `do while`
  - do{ 블록문 } while(조건식);
  - 블록문을 실행한 후 조건식을 평가
- `while`
  - while(조건식){ 블록문 }
  - 조건식을 평가한 후 블록문을 실행
- `for`
  - for(초기식; 조건식; 증감식){ 블록문 }
  - 초기식을 실행한 후 조건식을 평가
  - const는 사용할 수 없음
  - let으로 일반적으로 선언함
- `for in`

  - 객체의 프로퍼티를 반복할 때 사용
  - for(변수 in 객체){ 블록문 }
  - 실제 데이터는 인덱스 번호임
  - 배열-> 인덱스 , 객체-> 키값

  ```js
  let strbrr = ['a', 'b', 'c', 'd', 'e'];
  for (let index in strbrr){
    console.log(index);
  } <- 해당 인덱스 번호 출력

  for (let index in strbrr){
    console.log(strbrr[index]);
  } <- 해당 값 직접적으로 출력

  let userobj = {
    name: 'Mike',
    age: 30
  };

  for (let key in userobj){
    console.log(key);
  } <- 해당 키값 출력

  for (let key in userobj){
    console.log(userobj[key]);
  } <- 해당 값 출력
  - 배열 반복 할 떄는 index를 사용, 객체 반복할 때는 key를 사용
  ```

- `for of`

  - 배열의 요소를 반복할 때 사용
  - for(변수 of 배열){ 블록문 }
  - 실제 값에 접근 가능
  - for in과 다르게 인덱스 번호가 아닌 실제 값에 접근 가능
  - 배열 -> 값, 객체 -> X

  ````js
  for (let value of strbrr){
    console.log(value);
  } <- 해당 값 출력

  for (let value of strbrr){
    console.log(strbrr[value]);
  } <- 해당 인덱스 번호 출력```

  ````

- `continue`
  - 반복은을 건너 뛸 때 사용
- `break`
  - 반복문을 종료 할 때 사용
  ```js
  for (let i = 0; i < 10; i++){
    if (i === 5){
      break;
    }
    console.log(i);
  } <- 0, 1, 2, 3, 4 출력
  ```
- `무한 반복문(infinite loop)`
  - 코드를 작성해서 실행
  - 브라우저가 먹통이 되거나, 컴퓨터가 멈추는 현상이 발생
  - 무한 반복문을 방지하기 위해 조건식을 작성
  - false로 평가되는 조건식을 작성
- `유사배열 객체 `

  - 배열은 아니고 객체인데, 배열처럼 보이는 것
  - 문자열 같은 경우는 접근할 수 있지만 변경할 수 없음
  - 래퍼 객체(wrapper object)

- `length 프로퍼티`
  - 유사배열 객체의 길이를 반환
  - ex) `const str = 'hello'; console.log(str.length); // 5`
  - ex) `const arr = [1, 2, 3]; console.log(arr.length); // 3`
- do while, for 문은 객체를 반복할 수 없음

  - for in 문은 객체를 반복할 수 있음

- 단일 반복문

  - 이중 반복문 또는 다중 반복문

  ```js
  for (let i = 0; i < 3; i++){
    for (let j = 0; j < 3; j++){
      console.log(i, j);
    }
  } <- 0 0, 0 1, 0 2, 1 0, 1 1, 1 2, 2 0, 2 1, 2 2 출력
  ```

- 연습문제

```js
//1 피보나치 수열 계산
let n = 10;
let fibo = [];
for (let i = 2; i < n; i++) {
  fibo[0] = 0;
  fibo[1] = 1;
  fibo[i] = fibo[i - 1] + fibo[i - 2];
}
console.log(`피보나치 수열(${n}항):`, fibo);
```

```js
// 1 - 강사님 풀이
const n=10;
let a =0
let b=1;
const results=[];
let temp=null;

for (let i =0; i<n; i++{
    results.push(a);
    temp = a;
    a = b;
    b = temp + b;

}
console.log(results);
```

```js
//2 소수 찾기
let start = 1;
let end = 100;
let results = [];

for (let i = start; i <= end; i++) {
  let isPrime = true;
  if (i === 1) continue;
  for (let j = 2; j < i; j++) {
    if (i % j === 0) {
      isPrime = false;
      break;
    }
  }

  if (isPrime) {
    results.push(i);
  }
}

console.log(results);
```

```js
// 2 - 강사님 풀이
const primes = [];
for (let number = 2; number <= 100; number++) {
  console.log(number);
  let isPrime = true;
  for (let divisor = 2; divisor < number; divisor++) {
    if (number % divisor === 0) {
      isPrime = false;
      break;
    }
  }
  if (isPrime) {
    primes.push(number);
  }
}
console.log(primes);
```

```js
// 3배열 요소의 합 구하기
const numbers = [5, 10, 15, 20, 25];
let results = 0;
for (let i = 0; i < numbers.length; i++) {
  results += numbers[i];
}

console.log(results);
```

```js
//3 - 강사님 풀이
const numbers = [5, 10, 15, 20, 25];
let results = 0;
for (let number of numbers) {
  results += number;
}
console.log(results);
```

```js
//4 문자열 뒤집기
const str = "Hello, World!";
let reverse = "";

for (let i = 0; i < str.length; i++) {
  reverse += str[str.length - i - 1];
}
console.log("뒤집힌 문자열:", reverse);
```

```js
//4 - 강사님 풀이
const str = "Hello, World!";
let reverse = "";
for (let i = str.length - 1; i >= 0; i--) {
  reverse += str[i];
}
console.log(reverse);
```

```js
//5 특정 숫자까지의 곱 계산
let n = 5;
let factorial = 1;

for (let i = 1; i <= n; i++) {
  factorial *= i;
}
console.log(factorial);
```

```js
//5 - 강사님 풀이
const n = 5;
let factorial = 1;
for (let i = 1; i <= n; i++) {
  factorial *= i;
}
```

```js
//6 암스트롱수
for (let i = 100; i <= 999; i++) {
  let one = (i - (i % 100)) / 100;
  let two = ((i % 100) - (i % 10)) / 10;
  let three = i % 10;

  if (i === one ** 3 + two ** 3 + three ** 3) {
    console.log(i);
  }
}
```

```js
//6- 강사님 풀이1
for (let i = 1; i < 10; i++) {
  for (let j = 0; j < 10; j++) {
    for (let k = 0; k < 10; k++) {
      const result = i * 100 + j * 10 + k;
      if (result === i ** 3 + j ** 3 + k ** 3) {
        console.log(result);
      }
    }
  }
}
```

```js
//6- 강사님 풀이2
for (let i = 100; i < 1000; i++) {
  const one = i % 10; // 일의 자리 -> 9
  const ten = ((i - one) / 10) % 10; // 129 -> 2
  const hundred = (i - one - ten * 10) / 100; // 100 -> 1 777 -> 700/ 7= 7
  if (one * one * one + ten * ten * ten + hundred * hundred * hundred === i) {
    console.log(i);
  }
}
```

```js
//6- 강사님 풀이3
for (let number = 100; number <= 999; number++) {
  const digits = String(number).split("").map(Number);
  const sumOfCubs = digits.reduce((sum, digit) => sum + digit ** 3, 0);
  if (sumOfCubs === number) {
    console.log(number);
  }
}
```
