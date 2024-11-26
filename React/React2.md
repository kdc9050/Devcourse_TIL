## 리액트 파일 확장자

- JSX : JavaScript XML
  - .tsx : TypeScript + JSX
  - .jsx : JavaScript + JSX
  - .js : JavaScript
  - ts는 jsx에서 사용 불가
- vite
  - .jsx : JavaScript + JSX
  - .tsx : TypeScript + JSX
  - .ts : TypeScript

## 리액트 사용이유?

- 가장많은 사용자가 존재하기 때문에

### 클라이언트에서 도메인이 입력이 되고 display까지 나오는 과정

1. 도메인 입력
2. DNS 조회
   3 Client
3. HTTP 요청
4. 서버 처리
5. HTTP 응답
6. HTML 파싱
7. DOM 생성
8. CSS 파싱
9. CSSOM 생성
10. Render Tree 생성
11. Layout (Reflow)
12. Paint (Repaint)
13. Display

- 리플로우 : 레이아웃이 변경되어 다시 그리는 것 (웬만하면 transform으로 처리)
- 리페인트 : 스타일이 변경되어 다시 그리는 것(웬만하면 opacity로 처리)
- `크리티컬 랜더링 패스` : 브라우저가 페이지를 렌더링하는 과정에서 가장 중요한 부분
  - html 파싱, css 파싱, cssom 생성, render tree 생성, layout, paint, display
- Render Pahse: Virtual DOM 생성
  - Virtual DOM: 실제 DOM을 추상화한 자바스크립트 객체
  - Virtual DOM은 실제 DOM보다 가볍고 빠르다
  - Virtual DOM은 실제 DOM과 동기화된다
  - Virtual DOM은 변경된 부분만 실제 DOM에 반영한다
- Commit Phase: 실제 DOM에 반영

### 컴포넌트

- 컴포넌트는 재사용 가능한 UI 조각
- 컴포넌트는 독립적이고 재사용 가능하다

## 컴포넌트 아키텍쳐

### 클래스형 컴포넌트

```tsx
class App extends Component {
  render() {
    return <div>Hello, React</div>;
  }
}
export default App;
```

### 함수형 컴포넌트

```tsx
export default function App() {
  return <div>Hello, React</div>;
}
```

- 클래스형 컴포넌트로 구현할 수 있는 코드를 함수 컴포넌트로 구현 못하는 경우가 있었음
  - state, lifecycle method(생명주기 메서드)
  - 리액트 16.8 => Hooks 도입
- 그래서 클래스형 컴포넌트를 배제하고 함수형 컴포넌트로만 구현
- 대부분 함수형 컴포넌트로 구현 그래서 클래스형 컴포넌트는 배울 필요가 없음
- `React.Fragment` : 불필요한 div 태그를 생성하지 않기 위해 사용 => <></>로 사용 가능
- 컴포넌트 트리 : 컴포넌트의 계층 구조
  -

## React CSS 작성방법

- 글로벌 스타일을 지정하고 싶으면
  - main.tsx에 추가
- 기본 스타일 지정 방법
  - `인라인 스타일`
    - style 속성의 값으로 스타일을 지정하는 방법
  ```tsx
  export default function Title() {
    const styled = {
      fontSize: "20px",
      color: "red",
    };
    return <h1 style={styled}>gd</h1>;
  }
  ```
  - `글로벌 스타일`
    - 외부 CSS 파일을 import하여 사용하는 방법
    ```tsx
    import "./Title.css";
    ```
  - `CSS Modules`
    - CSS 파일을 모듈화하여 사용하는 방법
    - CSS 파일명.module.css로 작성
    - CSS Modules를 사용할 때는 classNames 라이브러리를 함께 사용하는 것이 효율이 좋음
    ```tsx
    import styles from "./Title.module.css";
    export default function Title() {
      return <h1 className={`${style.title} ${style deco}`gd</h1>;
    }// styles.title로 사용
    ```

### classnames 라이브러리

- 조건부 클래스를 적용할 때 사용
- 원하는 이름을 리턴하고 싶을 때 사용

```tsx
import classNames from "classnames";
export default function Title() {
  const isBlue = true;
  return <h1 className={classNames("title", { blue: isBlue })}>gd</h1>;
}
```

- CSS in JS
  - Tailwind CSS
  - styled-components
  - emotion
  - Vanilla Extract
