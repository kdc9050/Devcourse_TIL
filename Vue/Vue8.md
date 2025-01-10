## Vue Router

- npm install vue-router@4

### Vue Router 사용법

- Main.js에 router를 생성하고 App을 마운트한다.
  - import { createRouter } from "vue-router";
  - const router = createRouter({}); => router 인스턴스 생성
    - 필수속성 : history: createWebHistory(), routes: []
    - history: createWebHistory() => /user/1 같은 URL을 사용할 수 있게 해줌
    - history: createWebHashHistory() => /#/user/1 같은 URL을 사용할 수 있게 해줌 // 요즘은 잘 안씀
    - routes: [] => 라우터 설정
      - routes: [{path: "/", name: "Home", component: Home}] => url 경로, 라우트 고유한 이름, url로 접근했을 때 표시될 컴포넌트(정적임포트방식)
      - vue에서는 라우터 컴포넌트를 pages라는 파일에 만듬
- 정적 임포트 방식 componete:Home
  - 단점 => 필요없는 페이지에 대한 컴포넌트도 모두 불러옴
  - 장점 => 미리 불러와서 리소드에 대한 로딩이 빠름
- 동적 임포트 방식 component: () => import("../pages/Home.vue")
  - 장점 => 필요한 페이지의 컴포넌트만 불러옴
  - 단점 => 라우터로 이동할 때마다 로딩이 발생
- 루트 컴포넌트만 정적 임포트하고 나머지는 동적 임포트해도 지장없다.

- router 폴더에 index.js 파일을 생성하여 라우터 설정을 따로 관리한다.
  - import { createRouter, createWebHistory } from "vue-router";
  - 파일 임포트
  - const router = createRouter({}); => router 인스턴스 생성
- Main.js에서 router를 임포트하고 App을 마운트한다.
  - import router from "./router";
  - const app = createApp(App);
  - app.use(router);
  - app.mount("#app");
- App.vue에서 라우터를 사용한다.

  - <RouterLink to="/">Home</RouterLink> => 라우터로 이동할 링크를 표시
  - <RouterView/> => 라우터로 표시될 컴포넌트를 표시

- `https://www.example.com/user/profile?name=mike&age=28`
  - https:// => 프로토콜
  - www.example.com => 도메인 네임
  - /user/profile => path, 각각은 세그먼트
  - ?name=mike&age=28 => 쿼리스트링 , 키,값 쌍으로 이루어짐

### 동적 경로 매칭

- /user/:id => /user/1, /user/2, /user/3
- useRoute() => 현재 라우터 정보를 가져옴
- const route = useRoute();
- const { id } = route.params; => 동적 경로로 전달된 파라미터를 가져옴
- const { lang } = route.query; => 쿼리스트링으로 전달된 파라미터를 가져옴

- user-:afterUser(.\*) => /user-1, /user-2, /user-3
  - :afterUser => 동적 파라미터
  - (.\*) => 모든 문자열을 의미

```
const hadleMethod = () => {
  router.replace("/"); // 결제 페이지에서 많이씀
  router.back(); // 뒤로가기
  router.forward(); // 앞으로 가기
  router.go(1); // 1단계 앞으로 가기
  router.push("/"); // 라우터로 이동
};
```

### 예외 처리

- {path: "/:pathMatch(._)_", name: "NotFound", component: NotFound} => 모든 경로에 대한 예외 처리

### 프로그래밍 탐색방법

- import { useRouter } from "vue-router";
- const router = useRouter();
- router.push({name: "User", params: {id: 1}}) => 라우터로 이동
- <button @click="router.push('/')">Go Home</button> => 버튼을 클릭하면 라우터로 이동

### 이름이 있는 경로 탐색 방식

- {name: "User", params: {id: 1}} => 이름이 있는 경로로 이동
- router.push({name: "User", params: {id: 1}}) => 이름이 있는 경로로 이동

### 중첩경로 탐색 방식

- children: [] => 중첩 경로 설정
- 중첩경로를 하고 맨처음 페이지에 RouterView를 한번 더 써줘야함
- 일부분의 ui는 냅두고 일부분만 바꾸고 싶을 때 사용

### 이름이 있는 뷰 탐색 방식

```
{
      path: "/dashboard",
      name: "Dashboard",
      components: {
        header: () => import("../components/DashboardHeader.vue"),
        default: () => import("../pages/Dashboard.vue"),
        footer: () => import("../components/DashboardFooter.vue"),
      },
},
```

- components: {} => 이름이 있는 뷰 설정
- App.vue 에서 <RouterView name="header"/> => 이름이 있는 뷰를 표시
- 이름이 있는 뷰는 여러개를 사용할 수 있음

### 여러가지 방법

- props
  - props를 true로 두면 라우터로 전달된 파라미터를 컴포넌트의 props로 전달
  - 근데 쿼리스트링은 props로 전달이 안됨
- redirect
  - /about => /about-new 이렇게 리다이렉트시킬수 있음
  - redirect: "/about-new"
  - redirect: {name: "AboutNew"}
- alias
  - /dash => /dashboard 이렇게 별칭을 설정할 수 있음
  - alias: "/dash"
  - 어디로든 접근하면 /dashboard로 이동

### 고급개념

- 라우터 가드 (전역 가드)

  - 라우팅 과정 중에 특정 지점에서 라우트 전환을 가로채서 사용자 정의 기능을 추가할 때 사용
  - router.beforeEach((to, from, next) => { ... }) => 라우트가 전환되기 전에 실행되는 코드
  - to => 이동할 라우트 정보, from => 현재 라우트 정보, next => 다음 라우트로 이동하는 함수
  - 로그인 여부를 확인하고 로그인이 안되어 있으면 로그인 페이지로 이동시키는 코드를 사용하려고 씀
  - router.beforeResolve((to, from, next) => { ... }) => 라우터가 전환되기 바로 직전에 실행 되는 코드
  - router.afterEach((to, from, failure) => { ... }) => 라우터가 전환된 후에 실행되는 코드

- 라우터별 가드

```
    {
      path: "/about",
      name: "about",
      component: () => import("../views/AboutView.vue"),
      beforeEnter: (to, from, next) => {
        console.log("beforeEnter");
        next(false);
      },
    },
```

- beforeEnter: (to, from, next) => { ... } => 라우트가 전환되기 전에 실행되는 코드

- 컴포넌트 내 가드

  - 1. 라우트를 이동하기 전
    - onBeforeRouteLeave((to, from, next) => { ... }) => 라우트를 이동하기 전에 호출됨
  - 2. 동적 세그먼트의 값이 변경될 때
    - onBeforeRouteUpdate((to, from, next) => { ... }) => 동적 세그먼트의 값이 변경될 때 호출됨

- meta 속성

  - 라우터에 메타데이터를 추가할 수 있음
  - 나만의 값을 추가는 것
  - meta: { requireAuth: true } => 라우터에 메타데이터 추가
    - 보통 로그인 여부를 확인하고 로그인이 안되어 있으면 로그인 페이지로 이동시키는 코드를 사용하려고 씀

- 스크롤 제어
  - scrollBehavior => 스크롤 위치를 제어할 수 있음
  - scrollBehavior(to, from, savedPosition) => 스크롤 위치를 제어하는 함수
  - return { top: 0 } => 스크롤 위치를 맨 위로 이동
  - if (savedPosition) { return savedPosition; } => 이전 스크롤 위치로 이동
  - 내부링크 클릭시 스크롤 위치를 제어할 수 있음
  - <router-link to="#section1">Section 1</router-link>
  - return { el: to.hash, behavior: "smooth" } => 내부링크 클릭시 스크롤 위치를 제어하는 코드

## pinia

- 전역 상태 관리 라이브러리
- npm install pinia

```
// main.js
import { createApp } from "vue";
import { createPinia } from "pinia";
const app = createApp(App);
const pinia = createPinia();
app.use(pinia);
```

```
// store.js
import { defineStore } from "pinia";
import { computed, ref } from "vue";

export const useCountStore = defineStore("countStore", () => {
  const count = ref(0);
  const increment = () => count.value++;
  const doubleCount = computed(() => count.value * 2);
  return { count, increment, doubleCount };
});
```

- defineStore("countStore", () => { ... }) => 상태를 정의하는 코드
- 불러오려면

```
// App.vue

import { useCountStore } from "../stores/countStore";
const countStore = useCountStore();

<template>
  <h1>Home: {{ countStore.count }}</h1>
  <button @click="countStore.increment()">Increment</button>
</template>
```

- 비구조화 할당 방식으로 불러올 수 있음

```
<script setup>
import { useCountStore } from "../stores/countStore";
import { storeToRefs } from "pinia";
const countStore = useCountStore();
const { count } = storeToRefs(countStore);
//메서드는 비구조화 할당이 안됨 storeToRefs로 그래서 따로 해줘야함
const { increment } = countStore;
</script>
<template>
  <h1>Home: {{ count }}</h1>
  <button @click="increment()">Increment</button>
</template>
<style scoped></style>
```

- 그렇지만 새로고침하면 초기화됨 => pinia-plugin-persistedstate 사용
  - react zustand에서는 persist를 사용했지만 vue에서는 pinia-plugin-persistedstate를 사용
  - npm i pinia-plugin-persistedstate
