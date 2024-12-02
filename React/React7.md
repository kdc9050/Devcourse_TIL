## useReducer

- 로컬 상태를 정의할 때 사용, useState와 비슷
- reducer함수는 상태를 업데이트(변경)하는 로직을 수행하는 함수
- 타입에러 수정이 제일 어려움
- reducer함수는 두개의 인자를 무조건 받음
  - state는 현재 상태를 가리킴
  - 반드시 상태를 업데이트하는 로직을 수행한 후에는 상태를 반환해야함
  - action은 상태를 업데이트할 때 참조하는 값 (보통운 객체)
- 상태를 업데이트하는 로직을 reducer함수에서 수행
- reducer, type을 다른 파일로 분리하는 것이 좋음
- reducer함수는 switch문을 사용하여 코드 가독성을 높이는 것이 좋음
- reducer를 타입을 any로 지정한 뒤 다 적용해보고 타입을 수정하는 것이 좋음

```tsx
// useState
//장점: 간단하게 상태를 관리할 수 있음
//단점: 상태가 업데이트가 되는것을 예측하기 어려움
const [상태, 상태업데이트함수] = useState(초기상태);

// useReducer
//장점: 상태 업데이트가 예측 가능함=> 상태 업데이트 로직이 리듀서함수에서 존재하기 때문
//단점: 문법이 어려움
const [상태, 액션발생함수] = useReducer(리듀서함수, 초기상태);
const [state, dispatch] = useReducer(reducer, initialState);
```

- 계산된 속성
  - 타입스크립트에서는 객체의 속성을 계산된 속성으로 정의할 수 있음
  - 객체 형식으로 폼을 관리할 때 유용
  - `[action.field!]: action.value,`이런식으로 사용
- 결국에는 useState와 useReducer는 둘 중 하나 사용해도 되지만 개발자 선호도에 따라 다름
  - 상태를 업데이트하는 로직이 복잡하다면 useReducer를 사용하는 것이 좋음
  - 상태를 업데이트하는 로직이 간단하다면 useState를 사용하는 것이 좋음
