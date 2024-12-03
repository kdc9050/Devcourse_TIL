## 여러가지 react 꿀팁

- 고유 아이디 생성하기

  1. 고유 아이디를 생성할 때는 Date.now()를 사용하면 됨
  2. uuid 라이브러리를 사용하여 고유 아이디를 생성할 수 있음

- useId 사용하기

  - 고유한 아이디를 생성하는 훅
  - ex) const uuid = useId();
  - 이렇게 사용하면 uuid라는 고유한 아이디가 생성됨
  - 함수형 컴포넌트 내에서만 사용 가능

- 리액트 훅 규칙

  - 최상위 스코프 레벨에서만 사용해야함
  - 함수 바로 안에서만 써야함

- enter키 처리하는 방법
  1. form태그의 onSubmit속성을 사용하여 엔터키를 처리할 수 있음
  2. input태그의 onKeyDown속성을 사용하여 엔터키를 처리할 수 있음
  - 2-1. e.key === "Enter" 이런식으로 사용
  - 2-2. 그렇지만 한글이 조합문자라 2번 눌림
  - 2-3. e.nativeEvent.isComposing을 사용하여 조합문자인지 확인할 수 있음
  - 2-4. 그런데 맥북이슈임 => 윈도우에서는 잘 작동함 => 근데 콘솔에는 2번 눌림

## useEffect

- 함수형 컴포넌트에서 생명주기를 다룰 때 사용하는 리액트 훅
- 생명주기? => 그 컴포넌트가 태어나고 죽을 때까지
- 생명주기 => 그 컴포넌트가 렌더링 되고, 화면에서 사라질 때 까지
- 의존성 배열에 들어있는 값이 변경되지 않으면 다시 호출되지 않음
- useEffect(콜백함수, 의존성배열);
- 생명주기 : 생성, 수정, 삭제
- 생성 => 컴포넌트가 처음 렌더링 될 때, 한번만 실행
- 수정 => 컴포넌트가 렌더링 될 때마다 실행
- 삭제 => 컴포넌트가 사라질 때, 한번만 실행

```tsx
useEffect(() => {
  //컴포넌트가 생성되면 하고 싶은 로직
  // API 호출, 이벤트 등록, 타이머 등록

  // 클린업 함수=> 컴포넌트가 삭제될 때 실행
  return () => {
    //컴포넌트가 삭제될 때 하고 싶은 로직
  };
}, []);
// 의존성 배열 => 빈 배열이면 컴포넌트가 생성될 때만 실행
// 의존성 배열 => 특정 값이 변경될 때만 실행
// 의존성 배열 => 여러 개 넣을 수 있음
```

### localStorage

- localStorage => 브라우저에 데이터를 저장하는 객체
  - localStorage.setItem("키", "값") => 데이터 저장

## memoization

- 중복 계산을 피하기 위해 계산 결과를 저장해두고, 동일한 입력 값에 대해서는 이미 계산된 결과를 재사용하는 방법
- 알고리즘에서 많이 사용됨

```js
function fibbnacci(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  memo[n] = fibbnacci(n - 1, memo) + fibbnacci(n - 2, memo);
  return memo[n];
}
console.log(fibbnacci(100));
```

- 리액트에서도 중복 계산을 피하기 위해 memoization을 사용함
- useMemo, useCallback, React.memo

  - React.memo => 고차함수 (컴포넌트를 반환하는 함수)
  - useCallback => 함수를 기억하는 훅
  - useMemo => 값을 기억하는 훅

- 컴포넌트
  - `랜더링` => 최초 한 번 실행되는 것
  - `리랜더링` => 이미 생성된 컴포넌트가 다시 생성되는 것
    - 무조건 이 두가지 경우에만 실행됨
    - 컴포넌트에 정의된 상태가 변경되었을 때
    - 컴포넌트에 전달된 props가 객채가 변경되었을 때
- 트리구조로 App -> A -> B -> C일때 A가 리랜더링 되면 B, C도 리랜더링 됨

  - 랜더링이 될 필요가 없는데 랜더링이 될 때 => 성능 저하
  - 부모 컴포넌트가 랜더링 될 때 => 자식 컴포넌트도 랜더링 됨
  - 이게 불필요한 리랜더링임
  - 이런 문제를 해결하기 위해 memoization을 사용함

  ### React.memo => 컴포넌트를 반환하는 고차함수 / 컴포넌트

- `컴포넌트를 메모이제이션 할 때 사용`
- 함수형 컴포넌트를 반환하는 함수를 인자로 받음

```tsx
React.memo(function B() {
  console.log("B render");
  return (
    <>
      <h1>B</h1>
      <C />
    </>
  );
});
```

- 이렇게 사용하면 B컴포넌트가 랜더링 될 때 C컴포넌트도 랜더링 되지 않음

### 메모이제이션 낭비

- 메모이제이션을 많이 사용하면 메모리를 사용하게 됨
- 최대한 적게 사용하는 것이 좋음

### 리렌더링??

- A컴포넌트에서 props로 전달받은 count2가 변경되면 B컴포넌트도 리렌더링 됨
- A컴포넌트에서 count2가 변경되지 않아도 B컴포넌트는 리렌더링 됨
- A컴포넌트에서 increase함수가 변경되면 B컴포넌트도 리렌더링 됨
- A컴포넌트에서 increase함수가 변경되지 않아도 B컴포넌트는 리렌더링 됨
- 왜? => 함수, 객체, 배열은 참조자료형이기 때문에 메모리를 사용함
- 그래서 리액트에서는 함수를 메모이제이션하는 법이 있음
- useCallback

## useCallback / 함수

- useCallback(() => 함수, 의존성배열)

```tsx
const increase = useCallback(() => {
  setCount((count) => count + 1);
}, []);
```

- 함수를 메모이제이션 하기 위해
- 함수 메모이제이션 하는 이유? => 하위 컴포넌트에서 props로 전달할 때 메모리를 사용하기 때문에
- useCallback은 함수 내부 상황까지 기억함

```tsx
const increase = useCallback(() => {
  setCount(count + 1); // 이렇게 하면 count가 증가했을때 1으로 고정됨 -> 함수 내부 상황을 기억해서
}, []);
```

- 그러면 의존성 배열은 언제 사용해야할까?
  - useCallback이 재생성이 되는 경우에 사용함
- 의존성 배열을 불필요하게 사용하면 useCallback이 의미가 없어짐 => 메모리 낭비
- 내부적으로 리액트 훅은 기본적으로 메모이제이션을 사용함
  - ex) setCount함수는 메모이제이션을 사용함
  - `useState는 컴포넌트가 정의될 때 한번만 실행됨` => 랜더링에 영향을 주지 않음

### useMemo / 값

- useMemo(() => 값, 의존성배열) => 값을 기억하는 훅
- useMemo는 값이 변경될 때만 실행됨

```tsx
const selectedItems = useMemo(
  () => initaialItems.find((item) => item.selected),
  []
);
```

- React.memo, useCallback, useMemo의 차이를 알아야함 => 꼬리질문으로 React.Memo에서 고차함수까지 => 면접 질문
- useMemo 훅으로 함수를 메모이제이션 할 수 있음?
  - 할 순 있음 그러나 함수를 전용으로 메모이제이션하는 useCallback을 사용하는 것이 더 좋음
- useCallback 훅으로 값을 메모이제이션 할 수 있음?
  - 할 수 없음, 오직 함수만 메모이제이션 할 수 있음

### 그래서 메모이제이션을 언제 사용??

- 반복렌더링으로 출력이 되는 컴포넌트는 무조건 memoization을 사용해야함
  - ex) 리스트 컴포넌트, todoList 컴포넌트, 게시판 컴포넌트

## todo_memoization

- todo는 useState로 관리함 => 그래서 todoItemList 렌더링에 관혀를 안함
- 근데 toggleTodo, removeTodo는 todoItemList에 전달되어 렌더링에 영향을 줌
  - 그래서 함수를 메모이제이션 해야함
  - useCallback을 사용하여 함수를 메모이제이션함

## 전역상태관리

- App -> Count -> CountDetail -> CountDisplay, CountButtons
- 상태끌어올리기 => 상태를 부모 컴포넌트로 올려서 관리하는 것
- propsDrilling => props가 땅을 뚫고 내려가는 것 처럼 전달되는 것
  - 로컬 상태관리가 가질 수 밖에 없는 개발 형태 (useState, useReducer)
- 전역 상태관리 => 상태를 전역으로 관리하는 것
- Context API => 리액트에서 제공하는 전역 상태관리 라이브러리
- useContex
- Zustand

### Context API

- 리액트에서 제공하는 전역 상태관리 라이브러리
- 컨텍스트가 다르면 공유할 수 없음
- 컴포넌트를 같은 컨텍스트로 묶어서 상태를 공유할 수 있음!
- 같은 컨텍스트로 묶기 => 상태공유

1.  Context 객체를 만든다
2.  Context.Provider를 만든다
3.  Context.Consumer를 만든다

- 상태를 제공하는 것과 상태를 사용하는 것 각각 따로 만들어야 메모이제이션을 할 수 있음
  - 데이터를 공급 컨텍스트와 데이터를 사용하는 컨텍스트를 따로 만들어야함
  - ex) count 는 공급 컨텍스트, count를 사용하는 increase, decrease, reset은 데이터를 사용하는 컨텍스트
