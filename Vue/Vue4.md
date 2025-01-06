## vue 이벤트 처리

- methods 객체에 함수를 정의하고, 템플릿에서 이벤트를 처리할 때 함수를 호출
- v-on:click="함수명" 또는 @click="함수명" 으로 이벤트를 처리
- $event 객체를 이용하여 이벤트 객체를 전달할 수 있음=> @click="함수명($event)"

### 이벤트 수식어

- 뷰에서만 존재하는 기능
- stop, prevent, capture, self, once, passive 등의 수식어를 사용할 수 있음
  - `@click.stop` : 이벤트 전파 중지
  - `@click.prevent` : 기본 이벤트 중지
  - `@click.capture` : 이벤트 캡처링
  - `@click.self` : 자기 자신에게만 이벤트 처리
  - `@click.once` : 이벤트 한 번만 처리
  - `@click.passive` : 스크롤 이벤트 성능 향상
  - `@click.native` : 네이티브 이벤트 처리
- prevent, passive 이게 중요함

### 입력키 수식어

- 키보드 이벤트를 처리할 때 사용
- `@keyup.enter` : enter 키를 눌렀을 때 이벤트 처리
  - @keyup.ctrl.enter : ctrl + enter 키를 눌렀을 때 이벤트 처리
- `@keyup.esc`, `@keyup.tab`, `@keyup.delete`, `@keyup.space` 등의 키 수식어 사용 가능
- enter 중요

### v-memo

- 메모이제이션 기능을 하는 디렉티브
- 메모이제이션 하고 싶은 영역에 v-memo 디렉티브를 사용
  - `<div v-memo="{name}"></div>`

## 계산된 속성과 감시자 속성

### computed 속성

- 변수처럼 사용할 수 있음
- 한 번 렌더링이 되면 그 다음 부터 캐싱된 값을 사용
- 특정 변수가 변경되었을 때만 다시 계산
- 계산된 속성을 사용할 때는 함수 형태로 사용
- 템플릿에서는 변수처럼 사용
- 계산된 속성은 캐싱이 되기 때문에 성능이 좋음
- 계산된 속성은 데이터 속성을 사용할 수 없음
- 데이터 속성을 사용하려면 methods 객체에 함수를 정의하여 사용
- 기본적으로 읽기전용임 => setter 함수를 사용하여 읽기/쓰기 가능
