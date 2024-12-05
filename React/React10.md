## json-server

- npm install json-server@0.17.0
- db.json 파일 생성
- package.json 파일에 "scripts" 추가
  - "db": "npx json-server --watch db/db.json --port 3001",
  - "db_delay": "npx json-server --watch db/db.json --port 3001 --delay 2000"

## 데이터 통신

- 에러 상황 2가지

  - 주소가 잘못되었을 때
  - fetch(http://localhost:3001/postsddd) => res.ok가 false일 때
  - fetch(http://ddd:3001/posts) => catch로 떨어짐

- 커스텀 훅
  - 단점은 커스텀 훅도 훅(hook)이기 때문에 함수 안에서는 호출할 수 없다는 점
  - 그래서 GET 이외에는 활용할 수 없음

### CRUD

- CRUD란 Create, Read, Update, Delete의 약자
  - Create : POST
  - Read : GET
  - Update : PUT, PATCH
  - Delete : DELETE
- fetch(url) => then을 2번 사용
- axios.get(url) => then을 1번 사용
- GET
  - 데이터를 가져올 때 사용
  - fetch(url) => then을 2번 사용
  - axios.get(url) => then을 1번 사용
- POST
  - HTTP POST은 서버에 새로운 데이터를 추가할 때 사용
  - fetch(url, { method: "POST", body: JSON.stringify(data) })
- DELETE
  - 리소스를 삭제할 때 사용
  - fetch(url, { method: "DELETE" })
- PUT
  - 리소스를 업데이트할 때 사용
  - fetch(url, { method: "PUT", body: JSON.stringify(data) })
- PATCH
  - 리소스의 일부를 업데이트할 때 사용, 모든 걸 바꾸지 않고 하나, 두개만 바꿀 때 사용
  - 근데 대부분 지키지 않고 막 사용함
  - fetch(url, { method: "PATCH", body: JSON.stringify(data) })

## react-router

- 설치

  - npm install react-router

- BrowserRouter
  - 라우터를 사용할 때 사용 (/posts, /posts/1)
  - 브라우저에서 사용할 때 사용
  - <BrowserRouter> 안에 <Route>를 사용
  - <BrowserRouter> 안에 <Link>를 사용
  - <BrowserRouter> 안에 <Switch>를 사용
- HashRouter
  - 브라우저에서 사용할 때 사용 (/#/posts, /#/posts/1)
  - <HashRouter> 안에 <Route>를 사용
  - <HashRouter> 안에 <Link>를 사용
  - <HashRouter> 안에 <Switch>를 사용

### Route

- Routes
  - 여러 개의 Route를 사용할 때 사용
  - <Routes> 안에 <Route>를 사용
  ```jsx
  <Routes>
    <Route path="/" element={<h1>Main</h1>} />
    <Route path="/about" element={<h1>About</h1>} />
  </Routes>
  ```
- path

  - 경로를 지정
  - ex) <Route path="/posts" element={<Posts />} />

- element

  - 해당 경로로 이동했을 때 보여줄 컴포넌트
  - ex) <Route path="/posts" element={<Posts />} />

- Route Prefixes

  - 아무런 조치가 필요없음
  - ex) <Route path="/posts" />

- outlet

  - 중첩된 라우트를 렌더링할 때 사용
  - ex) <Outlet />

- 동적 세크먼트 (Dynamic Segments)
  - ex) <Route path="team/:teamId" element={<h1>Team</h1>} />

### Link

- to
  - 이동할 경로
  - ex) <Link to="/about">About</Link>
- Link
  - a 태그로 변환
  - ex) <Link to="/about">About</Link>
- NavLink
  - ex) <NavLink to="/about">About</NavLink>
- navLink vs Link

  - 현재 활성화된 값을 받아 올 수 있냐 없냐 차이
  - navLink는 현재 활성화된 값을 받아 올 수 있음

    - 함수형으로 쓸 수 있음
    - ex) <NavLink to="/about" className="active" style={{ color: "red" }}>About</NavLink>

  - Link는 현재 활성화된 값을 받아 올 수 없음

- https://reactrouter.com/start/library/routing

## jwt-token

- 웹에서 사용하는 암호화된 토큰

- access token
  - 서버에서 발급
  - 유효기간이 짧음
  - 서버에서 검증
- refresh token

  - 서버에서 발급
  - 유효기간이 길음
  - 서버에서 검증

  1. 팀원들이 모두 달려들어서 APi 종류 파악
     1.1 뭐가 있고, 무슨 기능 할 수 있고
  2. 컨셉 회의 => 뭐 만들지
  3. 기술 스택 => 뭐 쓸지
  4. 깃 레포 생성
  5. 업무 분담 =>
     5.1. 퍼블리싱하는 사람
     5.2. API모의 호출 코드 만드는 사람
     5.3. 1,2 처리가 되면 참조해서 역할 나누고 개발을 함

  6. 머지, 정리, 확인
