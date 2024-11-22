## 라이브러리, 프레임워크

- 어떤 개발을 함에 있어서 일정한 아키텍쳐로 개발할 수 있게 도와주는 도구
- 리액트(라이브러리이지만 프레임워크), vue(프레임워크), next.js(프레임워크)
- 떡볶이 -> 떡, 고추장, 오뎅 등등 직접 다 조합해서 만드는 것 -> 라이브러리
- 떡볶이 -> 떡, 고추장, 오뎅 등등 밀키트 형식 -> 프레임워크

- `리액트`

  - 2013, 리액트가 출시, Jordan Walke 페이스북, (개인 사이드 프로젝트)
  - 페이스북 일부 시스템에 적용하기 시작 -> 페이스북에 큰 호응 -> 오픈 소스로 전환
  - 개발의 시초는 다 미국, 외국에서 시작되는 경우가 많음
  - 그래서 국내에서는 늦게 시작되는 경우가 많음
  - 리액트는 경력이 10년 이상인 사람은 거짓말일 확률 실 경력은 7년 정도가 평균적
  - DOM 조작을 도와주는 라이브러리
  - 작년, 리액트가 전자정부프레임워크에 공식 등록됨
  - 리액트는 라이브러리이지만 프레임워크의 기능을 가지고 있음
  - 리액트는 점점 높아질 것, 스벨트라는 라이브러리도 있는데 국내에선 사용 x
  - 리액트 17 -> 18, 큰 변화 x
  - 리액트 15 -> 16, 큰 변화 o, 리액트 훅 도입
  - 리액트 18 -> 19, 큰 변화 있을 것 -> 서버 컴포넌트가 본격적으로 도입 될 것

- `vue`

  - 2014, 중국인 에반 유(Evan You)가 개발, 구글에서 일하던 중, 개인 프로젝트로 시작
  - 커뮤니티에 발표 -> 호응이 있었음
  - html, css, js -> 그대로 사용해서 개발 할 수 있게 도와줌
  - 배우기 쉽게, 사용하기 쉽게
  - 리액트 70 뷰 30, 리액트는 더 많이 사용됨

- `next.js`

  - 리액트 기반의 프레임워크
  - 캐싱이 잘 되어 있음
  - 리액트 19가 나와도 수요가 떨어지지 않을 것

- 학습 과정
  - 리액트 기초 문법(설치하는 법, jsx, 컴포넌트 작성방법 등) => 함수형 컴포넌트, 클래스형 컴포넌트
  - 리액트 훅
  - 전역 상태 관리 라이브러리 -> Context Api, 리액트 툴킷, Zustand | recoil
  - tanstackquery -> react-query
  - 리액트 라우터

## 리액트 들어가기..

- 바벨 -> js 최신 문법을 구형 브라우저에서도 돌아가게 해줌 (트랜스컴파일러)
- `createElement`
  - 리액트의 가장 기본적인 함수 -> 리액트가 출시되었을 때 사용하던 방식
  - createElement(태그명, 속성, 콘텐츠)
  - 사용한 이유는 -> 그 때 당시에는 jsx를 해석할 수 있는 브라우저가 없었음
  ```jsx
  const element = React.createElement(
    "main",
    { id: "main" },
    React.createElement("h1", null, "Hello, React with CDN!"),
    React.createElement("h2", null, "Hello, React with CDN!")
  );
  ReactDOM.render(element, document.getElementById("root"));
  ```
- `JSX`
  - facebook이 만든 자바스크립트 문법 확장
  - javascript + xml(Html)
  - 이것도 출시되었을 때 사용하던 방식
  ```jsx
  function App() {
    return (
      <main id="main">
        <h1>Hello, React with JSX!</h1>
        <h2>Hello, React with JSX!</h2>
      </main>
    );
  }
  ReactDOM.render(<App />, document.getElementById("root"));
  ```
- `create-react-app`
  - 가장 고전적인 방법, 더 이상 권장되지 않음
  - 더이상 유지보수 x

### NPM(Node Package Manager)

- node.js에 기본으로 설정되어 있는 관리 도구.
- 패키지 설치:
  - dependency에 설치 : npm install <package name> —save
  - devDependency에 설치: npm install <package name> —save-dev
  - devDependency에 설치: npm install -D <package name>
- 패키지 제거: npm uninstall <package name>
- 패키지 업데이트: npm update <package name>
- 패키지 실행: npm run <script_name>
- 글로벌 패키지
  - 설치: npm install -g <package name>
  - 제거: npm uninstall -g <package name>
- 패키지 초기화: npm init
  - pacakge.json 파일로 npm 프로젝트 초기화 명령어
- 프로젝트 생성: npm create <package name>
  - 내부적으로 npx를 사용해서 패키지를 활용하여 프로젝트 생성
- node.js와 함께 설치됨
- “.npmrc” 파일을 통해 설정 가능
- “package-lock.json” 파일을 사용하여 패키지 버전을 고정
- dependency -> 프로덕션 환경에서 필요한 패키지
- devDependency -> 개발 환경에서 필요한 패키지
- dependency와 devDependency의 차이점은 무엇인가요?
  - dependency는 프로덕션 환경에서 필요한 패키지이고, devDependency는 개발 환경에서 필요한 패키지입니다.
  - 웹은 html, js, css만 실행 할 수 있음.
  - dependency에서 다 적으면 다 빌드되서 나가기 때문에 빌드 시간이 오래 걸림
  - devDependency는 개발할 때만 필요한 것들을 넣어두면 됨
  - 둘의 구분? => 공식문서를 보면서 판단 => -save, -save-dev로 구분

### NPX(Node Package Execute)

- 일회성 패키지 실행: npx <package name>
- 특정 버전 패키지 실행: npx <package name>@<version>

- npm과 함께 설치됨
- 개발 의존성을 줄이고 필요한 경우 패키지를 설치하여 실행
- 임시적으로 패키지를 실행할 때 유용함

### Yarn

- 패키지 설치
  - 로컬: yarn add <package name>
  - 전역: yarn global add <package name>
- 패키지 제거
  - 로컬: yarn remove <package name>
  - 전역: yarn global remove <package name>
- 패키지 업데이트: yarn upgrade <package name>
- 패키지 실행: yarn run <package name>
- 병렬로 패키지를 설치하여 속도 향상
- yarn.lock 파일을 사용하여 더 확정적인 의존성 트리 생성
- 오프라인 모드 지원: 이전에 설치된 패키지를 다시 다운로드하지 않고 설치 가능
- 호환성 문제가 있음.
  - npm에 있는 패키지를 yarn으로 설치하면 문제가 생길 수 있음

### 패키지 버전 읽는 법

- 1.0.0 -beta (Major.Minor.Patch-옵셔널)
  - 1. Major : 주요 릴리즈
    - 1. 패키지에서 엄청난 변화가 있을 경우에 해당 위치의 숫자를 증가시킴
    - 2. 주로 이전 버전과 호환성을 깨트릴 정도의 중요한 패치의 경우 변경됨
  - 2. Minor: 새로운 기능
    - 1. 패키지에서 새로운 기능이 추가 되었을 경우에 해당 위치의 숫자를 증가 시킴
    - 2. 이전 버전과의 호환성은 유지함
  - 3. Patch: 버그 수정
    - 1. 기존에 포함되었던 기능에 대한 버그 수정을 하였을 경우 해당 위치의 숫자를 증가시킴
    - 2. 이전 버전과의 호환성은 유지함
  - 4. 옵셔널
    - 1. 특정 버전 뒤에 문자열로 된 의미를 부여하고 싶을 때 사용

### create-react-app

- 가장 고전적인 방법, 더 이상 권장되지 않음
- 더이상 유지보수 x
- npx create-react-app . -> npm run start
  -npx로 설치하는 법
  - npx create-react-app my-app
  - npm으로 설치하는 법
    - npm install -g creact-react-app
    - create-react-app my-app
    - 여기서 npm을 사용하지 않는 이유는 npm은 내부 로컬 환경에 패키지를 설치해서 사용하는 방법인데, 설치 당시의 버전을 그대로 활용하기 때문에 ‘최신 버전이 아닐 확률’이 높기 때문!

### vite

- npm create vite@latest . => npm run dev
  - vite를 현재 폴더에 설치
- swc (speedy web compiler)
  - 신종 컴파일러
  - 빌드 속도
- node_modules, package-lock.json, yarn.lock은 git에 올리지 않음 그리고 직접 관리하지 말기.
- 이 친구는 왜 npm run dev를 사용하는가?
  - package.json에 scripts에 dev를 등록해두었기 때문입니다.
  ```
  "scripts": {
    "dev": "vite",
    "build": "tsc -b && vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  },
  ```
  - 개발 서버 ?
    - npm run dev -> 개발서버 -> index.html 로드 -> main.tsx로드 -> app.tsx로드 -> 컴포넌트 로드
    - pulic 폴더와 asset 폴더의 차이점은??
      - 빌드도구에 의해 처리되는 파일과 그렇지 않은 파일의 차이
      - pulic 폴더에 있는 파일은 빌드 도구에 의해 처리되지 않는 파일
      - asset 폴더에 있는 파일은 빌드 도구에 의해 처리되는 파일

## 리액트 컴포넌트

- es7 react/redux/graphql/react-native snippets 설치
  - 리액트 코드를 빠르게 작성할 수 있게 도와주는 스니펫
- rfc => 입력하면 함수형 컴포넌트가 생성됨
- `reder`는 무엇
  - 컴포넌트를 화면에 그려주는 역할을 하는 함수
- `export default 와 export 차이점`
  - ex) import { App } from './App'; => export
  - ex) import App from './App'; => export default
  - export default는 한 파일에 한 번만 사용 가능
  - export는 여러 번 사용 가능
  - export default는 이름을 바꿀 수 있음
  - export는 이름을 바꿀 수 없음
  - 혼합된 경우
    - ex) import App, { App2 } from './App';

### JSX

- jsx 는 설탕 문법임
  - jsx는 컴파일러에 의해서(SWC) 변환해줌
  ```jsx
  export default function App() {
    return (
      <div>
        <h1>Hello, React!</h1>
      </div>
    );
  }
  // 변환
  export default function App() {
    return React.createElement(
      "div",
      null,
      React.createElement("h1", null, "Hello, React!")
    );
  ```
- JSX 규칙!

  - 1. 반드시 하나의 최상위 요소를 반환해야 한다.
  - 2. 태그는 반드시 닫혀 있어야 한다.
  - 3. JSX 속성은 camelCase로 작성한다.
  - 4. 주석은 {/별 별/ } 로 작성한다.

- JSX 권장사항
  - 1. 한 줄 이상의 코드는 소괄호로 감싸준다.
