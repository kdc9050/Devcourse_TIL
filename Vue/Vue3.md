## vue 필수문법 및 개념 2

### 디렉티브

- v-for : 반복문
  - `<div v-for="item in items" :key="item.id">{{ item.name }}</div>`
  - `v-for`는 `template`태그로 사용 가능함

### <template> 태그의 주요 목적

- DOM에 렌더링되지 않는 요소: <template> 자체는 DOM에 추가되지 않으며, 내부 내용만 렌더링됨됨
- 위치 지정 역할: 특정 Vue 지시문과 함께 사용하여 구조를 정의하고 컨텐츠를 유연하게 관리할 수 있음
- teplate과 같이 사용할 수 있는 지시문
  - v-if, v-else-if, v-else, v-for, v-slot
    -v-for와 key
  - v-for가 있는 <template> 태그는 key 속성을 가질 수 있음, 이 외의 속성은 <template> 태그에 의미가 없으므로 무시됨
  ```
  <template v-for="item in items" :key="item.id">
    <div>{{ item.name }}</div>
    <span>{{ item.description }}</span>
  </template>
  ```

## vue 스타일 적용 방법

### SFC에 있는 스타일 태그 사용

- <style> 태그를 사용하여 컴포넌트에 스타일을 적용할 수 있음
- scoped 속성을 추가하면 해당 스타일은 컴포넌트 내에서만 적용됨
- scoped 속성이 없으면 전역 스타일로 적용됨
- style 태그안에 @import를 사용하여 외부 스타일시트를 불러올 수 있음
- vite.config.js에 '@': fileURLToPath(new URL('./src', import.meta.url)) => 커스텀 에일리어스 설정
  - 이 설정을 통해 src 디렉토리를 '@'로 사용할 수 있음
  - 대부분 ~ 또는 @를 사용함
  - 이 설정을 통해 경로를 더 간결하게 사용할 수 있음

### 전역 스타일 적용 main.js

- 그냥 main.js에 import './index.css'로 불러오는 것도 가능함
- import "..." => 외부 스타일시트 가져오기 전역

### 인라인 스타일

- <div :style="{ color: 'red', fontSize: '13px' }"></div> => 인라인 스타일 적용
- v-bind:style 속성을 사용하여 인라인 스타일을 적용할 수 있음
  - `:style="{ color: 'red', fontSize: '13px' }"`
- data 속성을 사용하여 동적으로 스타일을 적용할 수 있음
  - `styleObject: { color: 'red', fontSize: '13px' }`
- 배열 스타일 바인딩
  - `:style="[styleObject, { fontSize: '13px' }]"`

### 객체 클래스 바인딩

- <div :class="{ active: isActive }"></div> => 객체 클래스 바인딩

### 외부 css 프레임 워크와 vue 스타일

- 부트스트랩
  - vue-bootstrap
- 테일윈드
  - https://tailwindcss.com/docs/guides/vite#vue
  - npm install -D tailwindcss postcss autoprefixer
  - npx tailwindcss init -p
  - content 에서 vue 추가해줘야함

### CSS 전처리기 사용

- sass
- npm install sass-loader sass --save-dev

### styled-components

- npm i @vue-styled-components/core

## v-model 디렉티브

- v-model 디렉티브는 폼 입력과 애플리케이션 상태를 양방향으로 바인딩하는데 사용됨
- v-model로 바인딩된 입력 요소는 사용자 입력에 따라 애플리케이션 상태가 업데이트됨
