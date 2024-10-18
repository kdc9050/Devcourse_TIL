# CSS 개념 정리

## 1. 위치 속성 (position)

HTML 요소들이 기본적인 흐름에서 벗어나 좌표값에 의해 배치할 때 사용

- **position: static;** (기본값)
- **position: relative;** (요소를 상대적으로 배치)
  - 예: 줄 서 있을 때, 앞 사람에게 자리 맡아달라고 할 때.
- **position: absolute;** (요소를 절대적으로 배치, 스크롤에 반응)
  - 예: 방향을 한 쪽만 써야 함 (위면 아래는 못 쓰고, 왼쪽이면 오른쪽은 못 씀).
- **position: fixed;** (요소를 절대적으로 배치하지만, 스크롤해도 위치가 고정됨)
  - 예: 위로 가기 버튼 같은 것.
- **position: sticky;** (요소를 절대적으로 배치하지만, 지정한 좌표의 임계점에 이르면 fixed처럼 고정됨)
  - 예: 스크롤을 내리면 계속 따라옴.
- **z-index:** (z축 순서를 정함) - 숫자가 클수록 위에 있음.

### 1.1 좌표 값

- **top, right, bottom, left**: 요소의 위치를 설정하는 값.

### 1.2 float

블록 요소를 한 줄에 배치하고 싶을 때 사용합니다.

- **float: left;** (왼쪽으로 배치)
- **float: right;** (오른쪽으로 배치)
- **float: none;** (기본값)
- **float: clear;** (해제)
  - **clear:** right, both, left, none.

### 1.3 overflow

요소의 크기를 벗어날 때 처리하는 방법입니다.

- **overflow: auto;** - 자동.
- **overflow: hidden;** - 넘치는 부분을 숨김.
- **overflow: scroll;** - 스크롤바를 만듬.

```

.wrap:after{
 content: "";
 display: block;
 clear: both;
}

```

## 2. 전환 속성 (Transition Properties)

전환이 안 되는 속성도 있을 수 있습니다.

- **transition-property:** 전환 효과 대상 속성.
- **transition-duration:** 전환 효과 지속 시간 (초 단위).
- **transition-delay:** 전환 효과 대기 시간.
- **transition-timing-function:** 전환 효과의 진행 속도.
  - **linear:** 일정한 속도로 진행.
  - **ease:** 빠르게 시작해서 느리게 끝남.
  - **ease-in:** 느리게 시작해서 빠르게 끝남.
  - **ease-out:** 빠르게 시작해서 느리게 끝남.
  - **ease-in-out:** 느리게 시작해서 빠르게 끝남.

## 3. transition

요소의 전환 효과를 지정합니다.

- **transition:** 속성 지속시간 지연시간 속도;
  - 예: `transition: all 1s 0.5s ease;`
  - **property:** 전환 효과 대상 속성.
  - **duration:** 전환 효과 지속 시간.
  - **timing-function:** 전환 효과의 진행 속도.
  - **delay:** 전환 효과 대기 시간.

## 4. 애니메이션 (Animation)

- 키 프레임이라는 개념과 반드시 같이 사용해야 합니다.
- **키프레임:** 애니메이션이 진행되는 과정에서 특정 시점에 발생해야 하는 여러 작업을 정의하는 문법.
- **animation:** `<이름> <지속시간> <타이밍함수> <지연시간> <반복횟수> <방향> <채우기모드> <반복대기시간>`.

```

@keyframes 짓고싶은이름 {
  from { 시작 스타일 }
  to { 끝 스타일 }
}

```

### 주요 애니메이션 속성

- **animation-name:** 애니메이션 키프레임을 지정하는 속성.
  - 예: `animation-name: 짓고싶은이름;`.
- **animation-duration:** 애니메이션 지속 시간을 지정하는 속성.
  - 예: `animation-duration: 1s;`.
- **animation-delay:** 애니메이션 지연 시간을 지정하는 속성.
- **animation-fill-mode:** 애니메이션의 전후 상태를 지정하는 속성 (기본값: none).
- **animation-iteration-count:** 애니메이션 반복 횟수를 지정하는 속성.

## 5. 변형 (Transform)

2D, 3D 변형을 제공합니다.

- **translateX, translateY**: 요소를 X축, Y축으로 이동.
- **transform: translate(-50%, -50%);** - 가로, 세로 중앙 정렬.
- **scale(1.5)** - 1.5배로 커짐.
- **rotate(45deg)** - 45도 회전.
- **transform-origin:** 기준점을 변경 (꼭지점을 기준으로 회전).

## 6. Flexbox

- **display: flex;** - 요소를 플렉스박스로 변경합니다.
- **flex-direction:** 요소 배치 방향 설정 (column, row, column-reverse, row-reverse).
- **flex-wrap:** 플렉스 아이템의 줄바꿈 여부 결정 (nowrap, wrap, wrap-reverse).
- **justify-content:** 주축 방향에서 정렬 (flex-start, flex-end, center, space-between, space-around).
- **align-items:** 교차축 방향에서 정렬 (stretch, flex-start, flex-end, center, baseline).

## 7. Grid

- **display: grid;** - 요소를 그리드 컨테이너로 변경합니다.
- **grid-template-columns:** 1fr 1fr - 1:1 비율로 나눔. `repeat(3, 1fr)` - 3개로 나눔.
- **grid-template-rows:** 1fr 1fr - 1:1 비율로 나눔.
- **gap:** 열과 열 사이의 간격.
- **column-gap:** 행과 행 사이의 간격.
- **grid-column:** `1 / span 3;` - 1번째 열부터 3번째 열까지 병합.
- **justify-items:** 아이템의 가로 정렬.
- **align-items:** 아이템의 세로 정렬.
- **align-items:** 부모에게 써야함, **align-self:** 자신에게 써야함.

### Grid 영역 지정

- **grid-template-areas:** `"header header header" "nav main main" "footer footer footer";`
  - 이름을 붙이면 맞는 자리로 배치.
  - `.`을 사용하면 빈 공간을 만들 수 있음.
  ```
  .container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 10px;
    grid-template-areas: "header header header" "nav main main" "footer footer footer";
  }
  ```
