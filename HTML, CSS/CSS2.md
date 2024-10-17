# CSS 필수 개념2

## 1. 기본 스타일 시트
   
   1.1 웹 브라우저가 기본으로 가지고 있는 스타일 시트(css)  
   1.2 reset (고여있는 퍼블리셔들은 자신만의 reset css를 가지고 있다.)

## 2. 적용 우선순위
   - css는 똑같은 속성이 중복되어 있으면 중복된 값 중 하나만 선택해서 적용 / 점수가 높은 것이 적용
   - 전체 선택자 - 0점
   - 태그 선택자, 가상 요소 선택자(::before, ::after) - 1점  
   - 클래스 선택자, 가상 클래스 선택자(:hover, :visited, :link) - 10점
   - 아이디 선택자 - 100점
   - 인라인 스타일 - 1000점
   - !important - 10000점 (가장 높은 우선순위) 
     - important가 여러 개일 경우, 원래 점수가 높은 것이 적용됨
     - ex) `<div style="color: red !important;">` -> 10000점 

## 3. 상속 (inheritance)
  - 부모 요소에 있는 속성이 자식 요소에게 상속됨
  - 상속되는 속성 -> color, font-size, font-family, line-height, text-align, visibility, white-space, text-indent, text-transform, text-decoration, letter-spacing, word-spacing
## 4. 단위
   4.1 절대 단위
   - px (픽셀) - 고정값  
   4.2 상대 단위
   - %, em, rem, vw, vh - 반응형 할 때 주로 rem
   - width, height  -> vw, vh
     - 부모 요소의 폰트 크기에 따라 달라짐
     - 부모 요소의 폰트 크기가 16px, 1em = 16px * 1 = 16px
     - 32px = 32px * 1em = 30px
     - 16px * 1 = 16px
     
## 5. 색상 표기법
   - 키워드 표기법 -> 색상을 영문 이름으로 표기
   - 16진수 표기법 -> #000000 ~ #ffffff
   - rgb 표기법 -> rgb(0, 0, 0) ~ rgb(255, 255, 255)
   - rgba 표기법 -> rgba(0, 0, 0, 0) ~ rgba(255, 255, 255, 1)
   - HLSA 표기법 -> hsla(색상, 채도, 명도, 투명도) -> 몰라도 됨
   
## 6. 텍스트 속성
   - font-size -> 글자 크기
   - font-weight -> 글자 굵기 700 이상은 bold, 400 이하는 normal 
   - font-style -> 글자 스타일 -> italic, oblique, normal(기본값)
   - font-family -> 글꼴
   - color -> 글자 색상
   - font-variant -> 소문자, 대문자 변환 -> small-caps, normal
   - text-align -> 텍스트 정렬 -> left, right, center, justify
   - text-decoration -> 텍스트 장식 -> underline, overline, line-through, none
   - letter-spacing -> 글자 간격 -> px, em, rem
   - line-height -> 줄 간격 -> px, em, rem

## 7. 박스 모델
   - 모든 HTML 요소는 사각형 박스 형태로 구성되어 있음
   - margin -> 요소의 외부 여백 - margin-top, margin-right, margin-bottom, margin-left -> 특정 방향으로만 적용 가능
   - padding -> 요소의 내부 여백
   - border -> 요소의 테두리
   - width, height -> 요소의 너비, 높이
   - box-sizing -> width, height의 기준 -> content-box, border-box 모든 요소의 크기 기준을 보더까지 잡음  
```css
   * {
       box-sizing: border-box;
       margin: 0;
       padding: 0;
   } -> 초기화 코드
```

## 8. background
- background-color -> 배경 색상
- background-image -> 배경 이미지
- background-image: url("경로");
- background-size: cover; /* 이미지를 늘리거나 줄여서 요소에 꽉 채움 */
- background-position: center center; /* 이미지의 위치를 조절 */
- background-repeat: no-repeat; /* 이미지 반복을 막음 */
- aria-label -> 웹 접근성을 위한 속성
## 번외 
- display: inline 하면 ul이 있으면 여기에 font-size: 0px 주고 li에 따로 사이즈 추가 해야 버그 해결
### BEM (block__element--modifier) 방법론 -> 최근에 많이 사용하는 방법론
  - BEM은 CSS 클래스 이름을 작성하는 방법론 중 하나
  - 어떤 식으로? -> `block__element--modifier `
  -> ` .header__logo--big `
- block -> 컴포넌트의 이름
- element -> 컴포넌트의 요소
- modifier -> 컴포넌트의 상태