## CSS in JS

- 런타임 기반 라이브러리
- js 파일에서 css 코드를 작성하는 방식

  - Tailwind CSS
  - styled-components
  - emotion
  - Vanilla Extract

### styled-components

- npm install styled-components
- styled-components는 컴포넌트를 만들 때 css를 사용할 수 있게 해준다.

```tsx
import styled from "styled-components";

const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;
```

- 단점으로는 태그를 파악하기 어렵다는 점이 있다.

### emotion

- npm install @emotion/css :
- import {css} from "@emotion/css";

```tsx
<div>
  <h1
    className={css`
      font-size: 30px;
      &:hover {
        color: blue;
      }
    `}
  >
    Hello
  </h1>
</div>
```

- npm install @emotion/react @emotion/styled :
  - import styled from '@emotion/styled';
  - 이거 쓰면 스타일드 컴포넌트랑 똑같이 사용 가능

### Vanilla Extract

- 제일 최신 기술, 제로 런타임, 타입스크립트 지원
- ts 파일에서 css 코드를 작성하는 방식 => style.css.ts
- 런타임때 css 생성한다는 것이 단점이었다. => 생성해야하는 css 코드가 많아지면 초기 실행이 느려질 수 있다.
  - 이를 해결하기 위해 vanilla extract은 제로 런타임 방식을 사용한다.
  - 빌드 타임에 css 코드를 생성한다.
- 설치
  - npm install @vanilla-extract/css
  - vite 기반 => npm install --save -dev @vanilla-extract/vite-plugin
  - vite.config.ts 파일에 설정 추가
  ```tsx
  import { vanillaExtractPlugin } from "@vanilla-extract/vite-plugin"; // 올바른 경로인지 확인
  export default {
    plugins: [vanillaExtractPlugin()],
  };
  ```

````

## Tailwind CSS
- 유틸리티 퍼스트(Utility First) CSS 프레임워크
  - 작은 스타일의 재사용 가능한 클래스를 통해 UI를 구성하는 방법
  - 유틸리티 퍼스트 => 클래스를 이용해서 스타일을 적용하는 방식
- 설치
  - npm install -D tailwindcss postcss autoprefixer
- 테일윈드의 클래스 1개당 CSS 속성 1개, 1:1 매칭
- font-size: 16px => text-base , text-decoration: underline => underline
- 장점
  - 어느 곳이든 class명만 유지한다면 스타일 적용 쉬움
  - 클래스명만 사용하면 별도의 css 파일 사용할 필요 없음
  - reset.css 자동 적용
  - 대부분의 next.js에서 공식적으로 밀고 있는 css 적용 방법 2개
    - CSS Module
    - Tailwind CSS
- 단점
  - 외우기 힘듬
- settings.json => 밑줄 제거
  - "css.lint.unknownAtRules": "ignore", // 추가 or 업데이트
- npm i tailwind-merge
  - classNames와 비슷한 기능을 함
  - 충돌을 방지하기 위해 사용
  ```tsx
  import { twMerge } from "tailwind-merge";
  <div className={twMerge("text-red-500", "text-blue-500")}>Hello</div>;
````

- npm install -D @tailwindcss/forms
  - 폼 요소를 스타일링하기 위한 플러그인
  - tailwind.config.js 파일에 추가
  ```tsx
  plugins: [require("@tailwindcss/forms")],
  ```

## 폰트 적용법

- rel = "preconnect" : 브라우저가 서버에 미리 연결하도록 지시
- display=swap : 폰트가 로드되기 전까지는 시스템 폰트를 표시하다가, 폰트가 로드되면 바로 적용
- block : 폰트가 로드될 때가지 텍스트를 보이지 않도록 하는 방식, 폰트가 로드되면 텍스트가 해당 폰트로 표시되어야함.

### 구글 폰트

- 구글폰트에서 원하는 폰트 선택 후 임베드 코드 복사

  - link 방식
    - index.html 파일에 붙여넣기
    - fonts.css 만들어서 폰트 적용 후 자신 만의 이름 적고 index.css에서 import 후 App에서 클래스네임에 적용
  - import 방식
    - index.css 파일에 붙여넣기
    - @import url('');

- 둘 중 더 나은 건 link 방식 => precoonect로 미리 연결하도록 지시하기 때문에 더 빠르게 폰트를 불러올 수 있다.

### 눈누 폰트

- 눈누 폰트에서 원하는 폰트 선택 후 웹폰트로 다운로드
- font.css에 import 아래 @font-face에 넣고 클래스 이름 만들어서 src빼고 복붙 후 사용

### 다운로드 폰트

- 다운로드 폰트에서 원하는 폰트 선택 후 다운로드
- 눈누 폰트와 같은 방식으로 사용
