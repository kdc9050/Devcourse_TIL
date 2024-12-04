## 1. redux

- 리액트에서 전역상태관리??
  - Context API
  - Redux
  - zustand
  - recoil
  - mobx
- Redux는 리액트를 위한 라이브러리가 아니다.
  - JavaScript를 위한 라이브러리
  - 살아남은 이유? => 많은 기업에서 사용하고 있기 때문에
  - Redux는 중앙집중식 상태관리 라이브러리
- Redux 설치

  - npm install @reduxjs/toolkit
  - npm install react-redux

- 폴더 구조
  - -src
    - -components
    - -store
      - -store.ts
      - -slice
        - -counterSlice.ts
        - -authSlice.ts

### store

- 상태 => 데이터
- 상태는 무조건 하나여서 store.ts는 하나 파일만 있어야함
- 액션 => 상태를 변경하기 위해서 조작하는 함수

```ts
export const store = configureStore({
  reducer: {
    // 여기에 슬라이스를 넣어준다.
  },
});

// 상태를 위한 타입
export type RootState = ReturnType<typeof store.getState>;
// 액션을 위한 타입
export type AppDispatch = typeof store.dispatch;
// 이 둘은 그냥 외우고 사용하면 된다.
```

### 슬라이스 => 상태와 액션을 공급하는 하나의 단위 (컨텍스트 느낌)

- 여러 개 있을 수 있음
- name, initialState, reducers => 필수
- name => 슬라이스의 이름
- initialState => 슬라이스의 초기 상태
- reducers => 액션을 정의하는 객체 (함수)
- payload => 액션을 실행할 때 넘겨주는 값

```ts
export const counterSlice = createSlice({
  name: " 이름",
  initialState: {
    // 초기 상태
  },
  reducers: {
    // 액션
  },
});
```

```ts
    incrementByAmount: (state, action) => {
      state.count = state.count + action.payload;
    }, // payload를 사용할 수 있음 => action은 고정
    // useReducer에서 사용하는 것과 비슷한 방식
```

- Immer => 불변성을 유지하는 라이브러리, 그렇지만 권장하지 않음

```ts
//reducers 안에 있는 함수들은 immer를 사용하고 있음
increment: (state) => {
      state.count = state.count + 1; // state = {...state, count: state.count + 1} 이게 원래 코드
},
```

### 내보내기

- 슬라이스 자체 내보내기
- 액션들 내보내기

```ts
export const { increment, decrement, reset, incrementByAmount } =
  counterSlice.actions;
export default counterSlice.reducer;
```

### 사용

- useSelector => 상태를 가져오는 훅
- useDispatch => 액션을 사용하는 훅

```ts
<button
        onClick={() =>
          dispatch({ type: "counterSlice/incrementByAmount", payload: 10 })
}
> // name을 아래처럼 사용할 수도 있음
<button
        onClick={() =>
          dispatch(incrementByAmount(10))
} // 둘 중 하나를 사용하면 됨 밑에는 내보내기를 해야함
```

- Redux 장점 => RTK 때문에 얻는 장점
  - 메모이제이션이 자동으로 됨
  - 알아서 최적화가 됨
  - 타입을 자동으로 추론해줌
  - 불변성을 신경쓰지 않아도 됨

### Redux 정리

- redux를 사용하는 방법은 엄밀히 따지면 RTK를 사용하는 방법임
  - RTK를 사용하지 않으면 의미 없음
  - RTK는 중앙 스토어를 만들고 슬라이스라는 팩을 끼워서 제공하는 방식

---

## 2. zustand

- zustand와 비슷한 라이브러리는 recoil, 그런데 recoil은 요즘 많이 사용하지 않음
- 전역 상태 관리 라이브러리 중 가장 쉬운 라이브러리
- Redux의 장점과 Context API의 장점을 뽑아옴
  - store를 만들어서 사용하는 방식
- 설치
  - npm install zustand

### store

- store를 만들어서 사용
- create 함수를 사용해서 store를 만듦
- set 함수를 사용해서 상태를 변경

````ts
import { create } from "zustand";
export const useCounterStore = create((set)=>{
// create 함수를 사용해서 store를 만듦
});

### 사용
- useCounterStore를 사용해서 상태를 가져옴
- set을 사용해서 상태를 변경
```ts
const increment = useCounterStore((state) => state.increment);
<button onClick={increment}>증가</button>
````

## 3. react 데이터 통신

- fetch API, axios 둘 중 하나를 사용

### fetch API

- 브라우저에 내장되어 있는 API
- fetch("주소", {옵션})
  - 옵션은 method, headers, body 등이 있음

```ts
fetch("https://jsonplaceholder.typicode.com/users")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

- {JSON.stringify(data, null, 2)} => JSON을 문자열로 변환, 들여쓰기 2칸
- useEffect를 사용해서 데이터를 가져옴
- 로딩중일 때 null 값이 뜨는데 이를 해결하기 위해서
  - 로딩 상태를 만들어서 해결 => error 도 마찬가지
  - `if (loading) return <div>로딩중...</div>;`
- useEffect는 async를 사용할 수 없음
- async를 사용하려면 함수를 만들어서 사용해야함
  - 이걸 더 많이 사용함

```ts
const getData = async () => {
  try {
    // 데이터를 가져오는 코드
  } catch {
    // 에러가 발생했을 때
  }
};
useEffect(() => {
  getData();
}, []);
```

### axios

- 설치
  - npm install axios
- fetch API보다 사용하기 편함
- axios.get("주소", {옵션})
  - 옵션은 headers, params 등이 있음

```ts
axios
  .get("https://jsonplaceholder.typicode.com/users")
  .then((res) => console.log(res.data));
```

- axios를 사용해서 데이터를 가져옴
- axios를 사용할 때는 async를 사용

```ts
const getData = async () => {
  try {
    const res = await axios.get("https://jsonplaceholder.typicode.com/users");
    console.log(res.data);
  } catch {
    console.error("에러 발생");
  }
};
useEffect(() => {
  getData();
}, []);
```
