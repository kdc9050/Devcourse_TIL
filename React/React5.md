## props drilling pattern

- 컴포넌트 트리에서 상위 컴포넌트에서 하위 컴포넌트로 데이터를 전달하는 패턴
- 프롭스딜링 패턴을 해결하기 위해 전역 상태 관리 라이브러리를 사용한다.

## 조건부 렌더링

### if

- if문을 사용하여 조건부 렌더링을 할 수 없다.
- return문 안에서 if문을 사용할 수 없다.
- 그래서 리턴문 밖에서 if문을 사용하여 조건부 렌더링을 한다.
- 큰 범위에서 컴포넌트(또는 jsx)를 분기 처리하고 싶을 때

```jsx
export default function App() {
  const isLoggedIn = false;
  if (!isLoggedIn) {
    return (
      <h1 className="text-3xl font-bold underline">로그인 되지 않았습니다.</h1>
    );
  }
  return <h1 className="text-3xl font-bold underline">로그인 되었습니다.</h1>;
}
```

### 삼항 연산자

- 삼항 연산자를 사용하여 조건부 렌더링을 할 수 있다.
- jsx 내에서 모든 작업 수행 가능
- JSX 범위 안에서 참과 거짓에 따른 분기 처리하고 싶을때

```jsx
export default function App() {
  const isLoggedIn = false;
  return (
    <>
      <h1>{isLoggedIn ? "로그인 되었습니다." : "로그인 되지 않았습니다."}</h1>

      {isLoggedIn ? <h1>1</h1> : <h1>2</h1>}

      <h1 style={{ color: isLoggedIn ? "green" : "blue" }}>
        로그인 되었습니다.
      </h1>
    </>
  );
}
```

### 논리 연산자(&&)

- 논리 연산자를 사용하여 조건부 렌더링을 할 수 있다.
- JSX 범위 안에서 참에 대한 분기 처리 하고 싶을 때

````jsx
export default function App() {

  const isLoggedIn = true;
  return (
    <>
      {isLoggedIn && <h1>로그인 되었습니다.</h1>}
    </>
  );


### 즉시실행함수
```jsx
export default function IIFE() {
  const isLoggedIn = true;
  return (
    <>
      {(() => {
        if (isLoggedIn) {
          return <p>로그인 되었습니다.</p>;
        } else {
          return <p>로그인이 필요합니다.</p>;
        }
      })()}
    </>
  );
}
// 변형하면 jsx안에서 사용 가능 하긴 함
// 즉시 실행 함수로 jsx를 감싸고 그 안에서 조건문을 사용하면 jsx를 반환할 수 있습니다.
````

## 반복 렌더링

- 랜더링 자체가 배열의 요소를 그대로 출력해줌
- map()
- for (while)
- forEach()
- reduce()

## tailwinds css

- bg-[#주고싶은색상] : 배경색상
- w-[#px] : 너비, h-[#px] : 높이
- text-[#주고싶은색상] : 글자색상
- rounded-[#px] : 모서리 둥글게
- shadow-[#px] : 그림자
- p-[#px] : padding
- px-[#px] : padding left, right
- py-[#px] : padding top, bottom
- m-[#px] : margin
- mx-[#px] : margin left, right
- my-[#px] : margin top, bottom
- placehoder: text-[#주고싶은색상] : placeholder 색상
- appearance-none : input의 기본 스타일 제거
- gap-[#px] : grid gap
- flex items-center : 중앙정렬

### 커스텀 컴포넌트 꿀팁

```tsx
//app.tsx
<Input type="text" placeholder="입력해주세요" maxLength={10} />; // 쓰고 싶은 거 다 쓰면 됨.

//Input.tsx
type InputProps = Omit<React.ComponentPropsWithoutRef<"input">, "type"> & {
  type: "text" | "password" | "email" | "number" | "tel";
};
export default function Input(props: InputProps) {
  const { ...rest } = props;
  return (
    <input
      className="w-60 h-11 rounded-lg font-inter text-sm px-4 placeholder: text-[#ACACAC]"
      {...rest}
    />
  );
}
//props를 받아서 사용할 때는 ...rest로 받아서 사용한다.
// 비구조화 할당으로 받아서 사용할 수 있다. 완벽 커스터마이징
// 그냥 input이랑 다른게 뭔데? 라고 생각할 수 있지만, 이렇게 커스텀 컴포넌트를 만들어서 사용하면
// 나중에 디자인이 바뀌었을 때나, 잠시 바꿀 때 이 커스텀 컴포넌트만 수정하면 된다.
```

```tsx
//app.tsx
<Button className=" rounded-lg font-medium text-center bg-red-500 text-white text-lg">
  add
</Button>;

//Button.tsx
type ButtonProps = React.ComponentPropsWithoutRef<"button">;
export default function Button(props: ButtonProps) {
  const { children, className, ...rest } = props;
  return (
    <button
      className={twMerge(
        `w-[77px] h-[44px] rounded-lg  font-inter bg-[#4f4f4f]`,
        className
      )}
      {...rest}
    >
      {children}
    </button>
  );
}
// twMerge를 사용하여 기존의 클래스와 새로운 클래스를 합쳐서 사용할 수 있다.
// 이렇게 커스텀 컴포넌트를 만들어서 사용하면 나중에 디자인이 바뀌었을 때나, 잠시 바꿀 때 이 커스텀 컴포넌트만 수정하면 된다.
// children 도 받아서 사용할 수 있다.
// className을 받아서 하기 때문에 기본 값 설정하고 받아오는 방식으로 사용할 수 있다.
```

```tsx
//app.tsx
<CheckBox>I agree with terms and policies</CheckBox>;

//CheckBox.tsx
type CheckBoxProps = Omit<React.ComponentPropsWithoutRef<"input">, "type"> & {
  type?: "checkbox";
}; // Omit을 사용하여 type을 checkbox로 하고 그리고 & 연산자를 사용하여 type을 checkbox로 고정시킴
export default function CheckBox(props: CheckBoxProps) {
  const { children, className, ...rest } = props;
  return (
    <div className="flex items-center gap-2 text-white">
      <input
        type="checkbox"
        id="chk"
        className={twMerge(
          "w-5 h-5 appearance-none border-[#4F4F4F] bg-white checked:bg-[#4f4f4f] rounded-[5px] checked:bg-[url('./check-icon.svg')] checked:bg-no-repeat checked:bg-center",
          className
        )}
        {...rest}
      />
      <label htmlFor="chk">{children}</label>
    </div>
  );
}
// 다른 것도 마찬가지로 Omit을 사용해서 type 고정 시키고 사용할 수 있다..
```
