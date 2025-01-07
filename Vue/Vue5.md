## vue 컴포넌트 
### 컴포넌트 등록 방법
- 1. 전역 컴포넌트 등록
  - 어디서든 그냥 불러와서 사용하기만 하면 됨됨
  - main.js에서 등록
  - app.component("컴포넌트 이름", 컴포넌트)
  - app.mount("#app")
  ```vue
  import { createApp } from "vue";
  import App from "./App.vue";
  import Frist from "./components/Frist.vue";

  const app = createApp(App);
  app.component("First", Frist).component("Second", Second); // 연속으로 체이닝 가능
  app.mount("#app");
  ```
  - 단점 : 컴포넌트가 필요없어도 불러옴
  - 모델컴포넌트, 라우터 등 전역으로 사용할 컴포넌트는 전역으로 등록
  
- 2. 지역 컴포넌트 등록
  - 필요한 곳에서만 불러와서 사용
  - 컴포넌트 내에서 등록
  ```vue
  <script>
  import First from "./components/First.vue";
  import Second from "./components/Second.vue";

  export default {
    name: "App",
    components: {
      First,
      Second,
    },
    data() {
      return {};
    },
  };
  </script>
  ```

## vue 컴포넌트 props
- 지역으로 불러와서 id, title같은 값 주면 그 컴포넌트 루트 태그에 자동으로 붙음
  -`<First id="first" title="first" />` => <div id="first" title="first">...</div>`
  - 이걸 어떻게 받아서 쓰냐 => props
  - props : 컴포넌트에게 전달하는 값
  - props : ["id", "title"] 
  - 이렇게 받아서 사용 => {{id}}, {{title}}
  - 숫자를 넘기고 싶을땐 => v-bind:id="1"

## vue 라이프 사이클
- 컴포넌트가 생성되고 사라질때까지의 과정
- beforeCreate : 컴포넌트 생성 전
- created : 컴포넌트 생성 후
- beforeMount : 컴포넌트가 DOM에 추가되기 전
- mounted : 컴포넌트가 DOM에 추가된 후
- beforeUpdate : 컴포넌트가 업데이트 되기 전
- updated : 컴포넌트가 업데이트 된 후
- beforeUnmount : 컴포넌트가 DOM에서 제거되기 전
- unmounted : 컴포넌트가 DOM에서 제거된 후
- 이벤트를 등록하고 제거할때 사용
- beforeUpdate, updated : 데이터가 변경될때 사용
- beforeUnmount, unmounted : 컴포넌트가 DOM에서 제거될때 사용
- beforeCreate, created : 데이터를 불러오거나 초기화할때 사용
- beforeMount, mounted : DOM에 추가되거나 추가된 후에 사용

## 감시자 속성
- 데이터가 변경될때마다 실행되는 함수
```
watch : {
  변수명 : function(newValue, oldValue) {
    console.log(newValue, oldValue);
  }
}
```
- 변수명이 변경될때마다 newValue, oldValue를 출력
- 변수명을 변경하면 watch가 실행됨
- watch는 변수가 변경될때마다 실행됨
- computed는 변수가 변경될때만 실행됨
- 그래서 특정 데이터의 변경여부를 감시함
### 참조자료형 감시 
- 깊은 사용법 
```
watch : {
  arr: {
    handler: function() {
      console.log("arr changed");
    },
    deep: true,
  },
}
```
- arr의 값이 변경될때마다 실행
- deep : true로 설정하면 arr안의 값이 변경될때마다 실행됨
