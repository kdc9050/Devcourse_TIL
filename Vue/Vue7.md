## vue 슬롯

- slot은 컴포넌트의 템플릿에 컨텐츠를 추가할 수 있는 방법을 제공한다.
- react의 children과 비슷하다.
- 축약형 `#`을 사용하여 슬롯을 사용할 수 있다.

### 이름이 없는 슬롯

- `<slot></slot>`을 사용하여 이름이 없는 슬롯을 만들 수 있다.
- 컴포넌트에 컨텐츠를 추가하면 해당 위치에 렌더링된다.

```html
<template>
  <div>
    <slot></slot>
  </div>
</template>
```

```html
<template>
  <MyComponent>
    <p>hello</p>
  </MyComponent>
</template>
```

### 이름이 있는 슬롯

- 이름이 있는 슬롯을 사용하려면 `<slot name="name"></slot>`을 사용한다.
- 컴포넌트에 컨텐츠를 추가할 때 `v-slot:name`을 사용하여 이름이 있는 슬롯에 컨텐츠를 추가한다.

```html
<template>
  <div>
    <slot name="header"></slot>
  </div>
</template>
```

```html
<template>
  <MyComponent>
    <template v-slot:header>
      <h1>header</h1>
    </template>
  </MyComponent>
</template>
```

### 혼합 슬롯

- 이름이 있는 슬롯과 이름이 없는 슬롯을 혼합하여 사용할 수 있다.
- 이름이 없는 슬롯은 컨텐츠가 없을 때 렌더링된다.

```html
<template>
  <div>
    <slot name="header"></slot>
    <slot></slot>
  </div>
</template>
```

```html
<template>
  <MyComponent>
    <template v-slot:header>
      <h1>header</h1>
    </template>
    <p>hello</p>
  </MyComponent>
</template>
```

### 슬롯의 기본 값

- 슬롯에 컨텐츠가 없을 때 기본 값을 설정할 수 있다.
- `<slot></slot>`의 내용을 설정하면 된다.

```html
<template>
  <slot><span>default</span></slot>
</template>
```

```html
<template>
  <MyComponent></MyComponent>
</template>
```

### 동적슬롯

- <template v-slot:[dynamicName]></template>을 사용하여 동적 슬롯을 사용할 수 있다.
- <template #[dynamicName]></template>

### 슬롯 특징

- 스타일을 제공할 때는 부모컴포넌트에 있는 스타일에 영향을 받는다.
- 이것을 슬롯의 범위라고 한다.
- 데이터는 부모 컴포넌트의 영향을 받는다
- 슬롯의 범위를 지정하면 자식 컴포넌트의 데이터를 사용할 수 있다.

## 컴포지션 API

- Composition API는 Vue3에서 새롭게 도입된 API이다.
- Composition API는 코드를 더 쉽게 이해하고 재사용할 수 있도록 도와준다.
- Composition API는 setup() 함수를 사용하여 컴포넌트의 로직을 분리한다.
- Composition API는 ref(), reactive(), computed() 등의 함수를 제공한다.

### 등장 배경

- options API는 컴포넌트가 커질수록 가독성이 안좋아짐
- composition API는 코드의 재사용성을 높이고 가독성을 높인다.

## script setup

- Vue3에서 script setup이라는 새로운 기능이 도입
- script setup은 Composition API를 사용할 때 코드를 더 간결하게 작성할 수 있도록 도와준다.
- <script setup>을 사용하면 setup() 함수를 사용하지 않고도 컴포넌트의 로직을 작성할 수 있다.
- <script setup>안에 코드를 작성하면 자동으로 setup() 함수로 변환된다.
- 루트태그에서만 import {ref, computed} from 'vue' 해주면 된다.

## 컴포지션 API ++

- ref() : 기본값을 가진 반응형 데이터로 정의할 때
- reactive() : 참조자료형(객체, 배열)을 반응형 데이터로 정의할 때
- ref로 접근하려면 state.value.name 이런식으로 접근해야한다.
- reactive로 접근하려면 state.name 이런식으로 접근해야한다.
- computed() : 연산된 값을 반환할 때

### watch

- watch() : 데이터의 변화를 감지하여 처리할 때
- watch(감시 대상, 콜백 함수, 옵션) 형태로 사용

```javascript
watch(count, (cur, prev) => {
  console.log(cur, prev);
});

watch(
  state,
  () => {
    console.log(state.name);
  },
  { deep: true }
);
```

- deep true를 주면 배열이나 객체의 내부 값이 변경되어도 감지한다.
- once: true를 주면 한번만 실행된다. 콜백이 한 번만 실행된다.

### watchEffect

- watchEffect() : 데이터의 변화를 감지하여 처리할 때
- watchEffect(콜백 함수) 형태로 사용
- immediate: true + deep: true => 처음에 한번 실행하고 그 이후에는 변화가 있을 때만 실행한다.
- flush
  - pre: 기본값, 비동기로 실행된다.
  - post: 동기로 실행된다.

### watchPostEffect

- watchPostEffect() : 데이터의 변화를 감지하여 처리할 때
- immediate: true + deep: true + flush: post => 3개 옵션이 모두 적용된 상태
- watchEffect와 watch의 기능을 합친 것이다.

## auto import

- npm install unplugin-auto-import
- vite.config.js에 추가

  - import AutoImport from 'unplugin-auto-import/vite'
  - plugins: AutoImport({imports: ['vue']})

  # 컴포지션 API 라이프사이클 훅

## 1. 라이프사이클 훅의 개념

- 컴포넌트의 생애주기 동안 특정 시점에서 실행되는 함수.
- Composition API에서는 `onXxx` 형식의 훅으로 사용.
- 주요 시점: 생성, DOM 마운트, 데이터 변경, 컴포넌트 소멸 등.

## 2. 주요 라이프사이클 훅

- **`onBeforeMount`**: 컴포넌트가 DOM에 추가되기 직전에 실행. 초기화 작업에 사용.
- **`onMounted`**: 컴포넌트가 DOM에 추가된 후 실행. DOM 접근이나 초기 API 호출에 적합.
- **`onBeforeUpdate`**: 데이터 변경 후 DOM 업데이트 직전에 실행. 변경 전 작업 수행.
- **`onUpdated`**: 데이터와 DOM이 변경된 후 실행. DOM 조작 후 작업에 사용.
- **`onBeforeUnmount`**: 컴포넌트가 DOM에서 제거되기 직전에 실행. 이벤트 리스너 제거나 리소스 정리에 유용.
- **`onUnmounted`**: 컴포넌트가 DOM에서 완전히 제거된 후 실행. 정리 작업을 완료.

## 3. 라이프사이클 훅의 특징

- Composition API의 훅은 **직관적**이고 **유연성**이 높음.
- 특정 상태나 동작을 관리할 때 코드의 가독성을 높이는 데 도움.
- `onMounted`와 같은 초기화 관련 훅은 **API 호출, DOM 조작** 등 중요한 작업에 자주 사용.

# `provide`와 `inject`

## 1. 개념

- Vue의 `provide`와 `inject`는 **부모-자식 관계**에서 데이터를 전달하기 위한 메커니즘.
- **`provide`**: 부모 컴포넌트가 데이터를 제공.
- **`inject`**: 자식 컴포넌트가 제공된 데이터를 주입받아 사용.
- 복잡한 컴포넌트 계층에서 데이터를 간단하게 전달하는 데 유용.

## 2. 주요 특징

- `provide`에서 제공한 데이터는 **반응성을 유지**.
- 상하위 관계에서만 동작하며, 글로벌 상태와는 별개.
- 주입된 값은 기본적으로 **읽기 전용**이지만, 참조형 데이터(`ref`, `reactive`)는 수정 가능.

## 3. 활용 사례

- **상위-하위 컴포넌트 간 데이터 공유**:
  - 깊은 계층 구조에서 props를 여러 단계 전달하지 않아도 됨.
- **상태 관리 대체**:
  - Vuex나 Pinia를 사용할 필요가 없는 간단한 경우 대체로 사용 가능.

## 4. 고급 사용법

1. **반응형 데이터 전달**:
   - 부모에서 `ref`나 `reactive`로 데이터를 제공하면, 자식에서도 반응형으로 동작.
2. **기본값 설정**:
   - 자식에서 `inject` 사용 시 기본값을 지정하여 주입 실패 시 대비 가능.
3. **함수 전달**:
   - 부모에서 함수를 제공하여 자식에서 호출 가능. 콜백 패턴을 간단히 구현.

## 5. 한계와 주의사항

- **명시적이지 않음**:
  - 데이터 흐름이 props와 다르게 명시적이지 않아 코드 추적이 어려울 수 있음.
- **재사용성 제한**:
  - 특정 부모-자식 관계에 강하게 의존.
- **대체 방법**:
  - Vuex, Pinia 등 상태 관리 라이브러리를 통해 글로벌 상태를 관리하는 것이 권장될 수 있음.

---
