## 1. 가비지 컬렉터

- 메모리에서 더 이상 사용되지 않는 객체를 자도응로 감지하고, 해당 메모리를 회수하여 메모리에서 삭제해주는 시스템
- 자바스크립트는 가비지 컬렉터를 내장하고 있어서 개발자가 메모리 관리를 할 필요가 없다.

## 2. 가비지 컬렉션

- 메모리가 회수 되는 과정 -> 가비지 컬렉션
- 메모리가 쌓임 -> 메모리 누수(줄줄 샌다. 낭비 된다.)
- 가비지 컬렉션을 자동으로 수행한다. -> 실행컨텍스트가 콜스택에서 제거가 될 때.
- 자동으로 수행이 되지 않는 경우 -> 그 컨텍스트의 레코드 값이 참조 되고 있는 경우

## 3. 클로저

- 내부 함수에서 외부 변수를 참조하면서 반환 되는 경우
- 자유변수를 참조하는 내부 함수를 반환하는 것.
- 가비지 컬렉션의 대상이 되지 못하고 메모리 제거가 되지 못해서 메모리에 남아 있는 현상을 클로저라 한다.
- 자유 변수 : 내부 함수에서 참조하고 있는 외부 변수
- 실제로 클로저를 사용하는 경우는 많지 않다.
  - 클로저는 위험하다. -> 메모리가 자동으로 삭제가 안됨.
  - 클로저가 많으면?-> 회수되지 않은 메모리가 많아진다는 것 == 자바스크립트의 가비지 콜렉터 시스템을 위협하는 행위


    ```javascript
    function outer() {
      let a = 10; // 자유변수
      return  function inner() {
        a++;
        console.log(a);
      };
    }
    let fn = outer();
    fn();

    fn = null; // 클로저 메모리 회수 -> 이거 안하면 메모리 누수
    ```

    - 면접 질문
       - 클로저는 내부함수에서 자유 변수를 가리키고 있는 함수를 의미합니다.
        =>그래서 주로 캡슐화가 필요한 로직에 사용합니다.


    - 클로저 사용 패턴
        - 1. 캡슐화 -> 은닉화
        ```javascript
        function counter() {
        let num = 0; //외부에서 접근이 불가능하게 만들어준다.
        return {
            increase() {
            return ++num;
            },
            decrease() {
            return --num;
            },
        };
        }
        let count = counter();
        console.log(count.increase()); // 1
        console.log(count.increase()); // 2
        ```
        - 2. 함수 팩트리(특정 기능을 하는 함수를 고정할 때)
        ```javascript
        function makeMultiple(multiplier) {
            return function (num) {
                return num * multiplier;
            };
            }
            let multi2 = makeMultiple(2); // -> 2가 메모리에 남아있음 -> 클로저
            console.log(multi2(3)); // 6

            multi2 = null; // 클로저 메모리 회수
            multi2(3); // 에러
        ```
        - 3. 비동기 프로그래밍 패턴
            - 동기 언어-> 특정 코드가 실행되는 것을 기다려줌
            - 비동기적으로 코드를 실행 할 수 있음
        ```javascript
        function fetchData(url) {
          let result;
          return function (callback) {
            setTimeout(() => {
            result =  "";
            callback(result);
            }, 1000);
          };
        }
        let fetch = fetchData("www.google.com");
        fetct(data) = console.log(data);
        fetch = null; // 클로저 메모리 회수
        ```
        - 4. 메모이제이션 패턴
            - 동일한 입력에 대한 출력을 캐싱하여 중복 계산을 방지하는 패턴

        ```javascript
        fuction slowFunciton(n){
            for(let i = 0; i < 1000000000; i++);
            return n *2;
        }
        console.log(slowFunciton(2)); // 4

        function memoization(fn) {
            const cache = {};
            return function (...args) {
                const key = JSON.stringify(args); // 배열을 문자열로 변환
                if (cache[key]) {
                    return cache[key];
                }

                const result = fn(...args);
                cache[key] = result;

                return result;
            };
        }
        let f = memoization(slowFunciton);
        console.log(f(2)); // 4
        console.log(f(2)); // 4
        f = null; // 클로저 메모리 회수
        ```
