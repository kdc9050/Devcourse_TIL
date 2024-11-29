## 이미지 렌더링

- npm run build
- npm run preview
- 개발경로랑 빌드경로가 다르다. 그래서 빌드할때는 이미지 경로를 절대경로로 바꿔줘야한다.

```tsx
<img src="../src/assets/images/snow.jpg " />; // 개발경로
// 밑에꺼로 바꿔줘야한다.
import snow from "./assets/images/snow.jpg"; // 빌드경로
<img src={snow} />;
```

```tsx
<div className="w-60 h-60" style={{ backgroundImage: `url(${snow})` }}></div>
//src에 있었을 때..
```

```tsx
<div
  className="w-60 h-60"
  style={{ backgroundImage: `url(`/snow_p.jpg` }}
></div>
//public에 있었을 때..
```

- 이미지를 불러올때는 import를 사용한다. => 빌드도구가 관여해서
- public 과 src의 차이점
  - public은 빌드도구가 관여하지 않는다. => 번들링이 안된다.
  - src는 빌드할때 번들링된다.
- public에 이미지를 넣으면 빌드할때 그대로 복사되기 때문에 이미지 경로를 절대경로로 쓰면된다.
- src

  - src에 이미지를 넣으면 빌드할때 번들링되기 때문에 import를 사용해서 이미지를 불러와야한다.
  - 번들링된 파일은 웹팩이 관리한다. => 번들링된 파일은 브라우저가 이해할 수 있는 형태로 변환된다. => 번들링된 파일은 브라우저에서 실행된다.
  - 트리쉐이킹이 일어난다. => 사용하지 않는 이미지는 번들링되지 않는다.
  - 이미지 용량을 줄일 수 있다. => 웹팩이 이미지를 최적화 해준다.

- `public vs src`
- src/

  - 빌드 도구가 관리한다. 최적화 및 트리쉐이킹
  - import 리소스 불러와서 추가해야 함
  - 고정된 이미지를 렌더링 할 때, assets 관리 해야함

- public/

  - 빌드 도구가 관리하지 않는다. 최적화 및 트리쉐이킹이 일어나지 않는다.
  - /이미지 경로 (절대경로)
  - 파비콘 말고는 거의 사용하지 않는다. => 파비콘을 빌드과정에서 이름이 손상되지 말라고 public에 넣는다.

- 이미지 최적화
  - src 폴더 안에 images.ts 파일을 만들어서 임포트를 다 함
  - 그 다음 불러 올때 images.ts 파일을 불러와서 사용한다.
  - ex) {imgaes.snow}

```tsx
// src/assets/images.ts
import snow from "./snow.jpg";
import snow_p from "./snow_p.jpg";

export const images = {
  snow,
  snow_p,
};

// app.tsx
import { images } from "./assets/images";
<img src={images.snow} />;
```

- css로 넣기

```tsx
.logo {
  background-image: url("../images/react-logo.svg");
}
<div className="logo w-40 h-40 bg-cover"></div>
```

## 리액트 훅

- 변수를 선언할 때
  - 화면의 렌더링에 영향을 주는 변수인지
    - 상태(state) -> 리액트 훅 -> 16.8버전 이후에 나온 것
    - useState -> 상태를 관리하는 훅
  - 화면의 렌더링에 영향을 주지 않는 변수인지
    - let, const

### useState

- 상태와 상태를 변경하는 함수를 배열로 반환한다.
  - ex) const [count, setCount] = useState<number>(0);
- count: 상태(현재 값), setCount: 상태를 변경하는 함수, <number>: 상태의 타입, 0: 초기값
- setState
  - setState(값) -> 값으로 바로 변경
  - setState((현상태) => 값) -> 이전값을 참조할 수 있다.
  - 이전값을 참조할 때 콜백(2)아닐 때 값(1)으로 참조한다.
- <number>를 생략하면 타입스크립트가 타입을 추론한다.
- 상태-> 불변성을 지켜야한다. => 불변성을 지키지 않으면 리렌더링이 일어나지 않는다.
  - 불변성이란 값이 한 번 생성되면 변경할 수 없다는 것이다.

```tsx
import { useState } from "react";

export default function App() {
  const [students, setStudents] = useState(["james", "john", "jane"]);

  const addStudent = () => {
    setStudents((students) => [...students, "new student"]);
  };
  return (
    <>
      <div className="text-3xl">
        <ul>
          {students.map((student, index) => (
            <li key={index}>{student}</li>
          ))}
        </ul>
        <button onClick={addStudent}>학생 추가</button>
      </div>
    </>
  );
}
```

```tsx
import { useState } from "react";

interface User {
  name: string;
  age: number;
  gender?: string;
}

export default function App() {
  const [user, setUser] = useState<User>({ name: "john", age: 25 });
  const changUser = () => {
    setUser((user) => ({ ...user, gender: "nn" }));
  };
  return (
    <>
      <div className="text-3xl">
        <h1>{user.name}</h1>
        <h1>{user.age}</h1>
        <h1>{user.gender}</h1>
        <button onClick={changUser}>Change User</button>
      </div>
    </>
  );
}
```

### 폼을 제어 하는 방법

- 폼 요소를 제어하는 방법
  - 제어 컨트롤러
    - 상태를 정의하여 폼요소를 제어하는 방법
    - 실시간으로 폼 요소를 제어할 수 있다는 특징이 있다.
    - value와 onChange 가 세트라고 생각하면 된다. => value에 상태를 넣고 onChange에 상태를 변경하는 함수를 넣는다.
      - ex) input => <input value={name} onChange={(e) => setName(e.target.value)} />

```tsx
import { useState } from "react";

export default function App() {
  const [input, setInput] = useState("");
  const [select, setSelect] = useState("banana");
  const [checked, setChecked] = useState(false);
  const [radio, setRadio] = useState("apple");
  const [textarea, setTextarea] = useState("");
  return (
    <>
      <div className="text-3xl">
        <form>
          <h1>{input}</h1>
          <input
            type="text"
            onChange={(e) => {
              setInput(e.target.value);
            }}
            value={input}
          />

          <h1>{select}</h1>
          <select
            value={select}
            onChange={(e) => {
              setSelect(e.target.value);
            }}
          >
            <option value="apple">Apple</option>
            <option value="banana">Banana</option>
            <option value="cherry">Cherry</option>
          </select>

          <h1>{checked ? "Checked" : "Unchecked"}</h1>
          <input
            type="checkbox"
            checked={checked}
            onChange={(e) => {
              setChecked(e.target.checked);
            }}
          />

          <h1>{radio}</h1>
          <input
            type="radio"
            checked={radio === "apple"}
            onChange={() => {
              setRadio("apple");
            }}
            defaultChecked
          />
          <input
            type="radio"
            checked={radio === "banana"}
            onChange={() => {
              setRadio("banana");
            }}
          />
          <input
            type="radio"
            value="cherry"
            checked={radio === "cherry"}
            onChange={() => {
              setRadio("cherry");
            }}
          />
          <h1>{textarea}</h1>
          <textarea
            value={textarea}
            onChange={(e) => {
              setTextarea(e.target.value);
            }}
          ></textarea>
        </form>
      </div>
    </>
  );
}
```

- 비제어 컨트롤러
  - DOM에 직접적으로 접근해서 요소를 제어하는 방법
  - useRef를 사용하여 DOM에 접근한다.
  - 실시간으로 폼 요소를 제어할 수 없다.

### useRef

- DOM을 직접 참조해서 폼 요소를 제어
- 실시간으로 폼 요소를 제어할 수 없다.
- 하나의 요소만 참조할 수 있다.
- radio 같은 경우에는 배열로 참조해야한다. => radioRef.current.find((el) => el.checked)
- js => document.querySelector("input")
- react => useRef 사용

```tsx
import { useRef } from "react";

export default function App() {
  const idRef = useRef<HTMLInputElement>(null);
  const pwRef = useRef<HTMLInputElement>(null);
  const checkRef = useRef<HTMLInputElement>(null);
  const radioRef = useRef<HTMLInputElement[]>([]);

  const submitHandler = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    console.log(idRef.current?.value);
    console.log(pwRef.current?.value);
    console.log(checkRef.current?.checked);
    const selectedRadio = radioRef.current.find((el) => el.checked);
    console.log(selectedRadio?.value);
  };
  return (
    <>
      <form onSubmit={submitHandler}>
        <input type="text" ref={idRef} placeholder="아이디" />
        <input type="password" ref={pwRef} placeholder="비밀번호" />
        <input type="checkbox" ref={checkRef} />
        <input
          type="radio"
          name="gender"
          ref={(el) => {
            if (el) radioRef.current[0] = el;
          }}
          value="male"
          defaultChecked
        />
        Male
        <input
          type="radio"
          name="gender"
          ref={(el) => {
            if (el) radioRef.current[1] = el;
          }}
          value="female"
        />
        female
        <button type="submit">로그인</button>
      </form>
    </>
  );
}
```

- tailwind는 부분치환을 허용하지 않음
  - ex) bg-[${color}] => bg-red-500 // x
  - ex) bg-red-500 // o
