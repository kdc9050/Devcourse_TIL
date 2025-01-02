# Vue 애플리케이션 기본 구조

## 1. package.json

### 주요 항목 설명

- **name**: 애플리케이션 이름.
- **version**: 버전 정보. [major].[minor].[patch] 형식.
- **private**: 공개 여부 (`true`일 경우 npm에 배포 불가).
- **scripts**: npm 명령어로 실행 가능한 스크립트.
- **dependencies**: 프로덕션 환경에서 필요한 모듈.
- **devDependencies**: 개발 환경에서 필요한 모듈.

---

## 2. index.html

- 개발 서버 실행 시 가장 먼저 로드되는 파일로, 애플리케이션 초기 구조를 정의

---

## 3. main.ts

- Vue 애플리케이션 초기화와 구성을 담당하는 파일

```typescript
import { createApp } from "vue";
import "./style.css";
import App from "./App.vue";

createApp(App).mount("#app");
```

### 동작 원리

- 1. **`createApp`**: Vue 애플리케이션 인스턴스를 생성.
- 2. **`style.css`**: 글로벌 스타일 불러오기.
- 3. **`App.vue`**: 루트 컴포넌트를 불러오기.
- 4. **`mount('#app')`**: `#app` 요소에 Vue 컴포넌트를 렌더링.

---

## 4. App.vue

### SFC (Single File Component)

- Vue에서 `.vue` 확장자를 가진 파일은 컴포넌트로 사용되며, HTML, CSS, JavaScript를 한 파일에 작성할 수 있습니다.

```vue
<script>
export default {
  name: "App",
};
</script>

<template>
  <div id="app">
    <h1>Welcome to Vue!</h1>
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}
</style>
```

### SFC 구성 요소

1. **`<template>`**

   - HTML 마크업 작성.
   - 데이터 바인딩 (`{{}}`), 디렉티브 (`v-if`, `v-for` 등) 사용 가능.

2. **`<script>`**

   - JavaScript 로직 작성.
   - `export default {}`로 컴포넌트 내보내기.

3. **`<style>`**
   - CSS 스타일 작성.
   - `scoped` 속성으로 해당 컴포넌트에만 스타일 제한 가능.

---

### 트리 구조

- Vue 애플리케이션은 App.vue를 루트로 하위 컴포넌트를 연결하는 트리 구조로 구성됨

# vue 필수 문법 및 개념

## 옵션스 API

- 옵션스 API :vue2에서 사용하던 방식
- 컴포지션 API : vue3에서 사용하는 방식
- Vue.js Options API는 컴포넌트 정의 방식으로, 속성을 명시적으로 선언해 가독성과 재사용성을 높임임

## 주요 특징

- **명확한 구조**: 각 속성이 어떤 역할을 하는지 분명하게 구분됨.
- **선언적 접근**: 상태와 동작을 선언적으로 정의.
- **생명주기 훅**: 특정 생명주기 단계에서 자동 호출되는 콜백 함수 제공.
- **재사용성**: 잘 구조화된 코드로 재사용성 향상.

## 옵션스 API 주요 속성

| 속성                 | 설명                             |
| -------------------- | -------------------------------- |
| **data**             | 컴포넌트 상태 데이터 정의.       |
| **methods**          | 함수 정의.                       |
| **computed**         | 계산된 속성 정의.                |
| **watch**            | 데이터 변화 감시.                |
| **props**            | 부모 컴포넌트로부터 데이터 수신. |
| **emits**            | 부모 컴포넌트로 이벤트 발신.     |
| **provide**          | 하위 컴포넌트에 데이터 주입.     |
| **inject**           | 상위 컴포넌트에서 데이터 수신.   |
| **Life Cycle Hooks** | 특정 단계에서 호출되는 함수.     |

## 주요 문법

### 데이터 정의 및 보간

```javascript
const app = Vue.createApp({
  data() {
    return {
      message: "Hello, Vue!",
      count: 0,
    };
  },
});
```

```html
<div id="app">
  <h1>{{ message }}</h1>
  <button @click="count++">Increase Count</button>
</div>
```

- 데이터 보간법 : 콧 수염 문법(mustach syntax) = {{}} 사용

### 주요 디렉티브

- **`v-html`**: HTML 태그 사용, 출력.
- **`v-text`**: 텍스트 출력.
- **`v-pre`**: 컴파일 방지, 건너띄게 함.
- **`v-bind`**: 속성 바인딩.
- **`v-if / v-else-if / v-else`**: 조건 렌더링.
- **`v-show`**: 표시 여부, 랜더링은 하지만 css로 display:none 처리.
- **`v-for`**: 리스트 반복, 키값이 있어야 함.
- **`v-show`**: 조건부 렌더링.
- **`v-cloak`**: 초기 렌더링 시 깜빡임 방지.
