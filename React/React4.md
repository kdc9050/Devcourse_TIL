## vite 6.0

- npm crete vite@latest .
  - 이거 하는데 y가 보인다.
  - 컴퓨터에 패키지가 없어서 뜨는 것
    --legacy-peer-deps => 이전 버전의 피어 디펜던시를 사용하겠다는 것

## 버전 최신

- npm outdated => 버전이 최신인지 확인
- npm install npm-check => npm-check 설치
  - npx npm-check => 버전이 최신인지 확인
  - npx npm-check -u => 업데이트 가능한 것들 업데이트
  - npx npm-check-updates vite -u => vite만 업데이트

## props

- 컴포넌트의 속성(properties)
  - 컴포넌트의 props로 데이터를 전달한다.
  - props는 부모 컴포넌트에서 자식 컴포넌트로 전달된다.
  - props 객체로 전달된다.
  - 컴포넌트에 사용된 속성들이 하나의 객체로 모이게 되는데 이를 객체 props라고 한다.
- types
  - types 파일을 만들어서 타입을 정의하고 사용한다.
  - \_\_.d.ts 파일을 만들어서 타입을 정의하고 사용한다.
- 비구조화 할당
  - props를 비구조화 할당하여 사용한다.
  - props를 비구조화 할당하여 사용하면 props.을 생략할 수 있다.
  - ex) const {name, age} = props; => name, age로 사용 가능
- 데이터 타입 쉽게 확인 방법
  - 툴팁을 사용하여 데이터 타입을 확인한다.

## children

- 컴포넌트 태그 사이에 있는 내용을 children이라고 함
- 모든 children은 React.ReactNode 타입이다. 무조건! 이 타입을 사용
- 태그는 props로 전달 될 수 없어서 children을 사용하여 전달한다.

## Event

- React의 이벤트는 소문자 대신 캐멀 케이스(camelCase)를 사용합니다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달합니다.
- on + 이벤트 이름으로 이벤트를 설정합니다.
- 콜백함수 형태에서 매개 변수를 받아서 추론된 형태로 이벤트 타입을 설정합니다.

  - ex) <button onClick={(e) => console.log(e)}>Click</button>

- onClick
  - 클릭 이벤트를 처리합니다.
  - `e`로 이벤트 객체를 전달 받을 수 있습니다.
  - e 객체의 타입을 알고 싶으면 `e: React.MouseEvent<HTMLButtonElement, MouseEvent>`로 설정합니다.
- onChange
  - 입력값이 변경될 때 발생하는 이벤트를 처리합니다.
- onKeyDown
  - 키보드의 키를 누를 때 발생하는 이벤트를 처리합니다.
- onSubmit

  - 폼을 제출할 때 발생하는 이벤트를 처리합니다.
  - e.preventDefault()를 사용하여 기본 동작을 막을 수 있습니다.

- 이벤트 헨들러에서
  - onSumit = {handleSubmit} => 이벤트 객체를 제외한 커스텀 매개변수를 전달 하지 않을까
  - onSumit ={(e)=>{handleSubmit(e)} 이벤트 객체 말고 커스텀 매개변수가 전달되려면
  - onSumit ={(e)=>{sum(e,10,20)} => 이렇게 하면 e는 이벤트 객체고 10,20은 커스텀 매개변수
