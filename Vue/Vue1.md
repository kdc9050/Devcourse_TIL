## Vue의 탄생 배경

- 뷰는 기본적으로 프레임워크 리액트는 라이브러리로 소개함
- 프로그레시브(점진적인) 자바스크립트 프레임워크라고 소개
- MVVM 패턴의 뷰모델 레이어에 초점을 맞춤
  - 뷰와 모델 사이에 뷰모델이라는 계층이 있음
  - 보여주는 뷰(view) 영역과 데이터를 처리하는 모델(model) 사이에 데이터를 중개하는 뷰 모델(view model) 계층을 두어 UI와 데이터 처리 로직의 상호 의존성을 줄이는 아키텍처 패턴

### Vue.js 탄생 배경 요약

1. **창시자 배경**  
   Vue.js는 중국 출신 개발자 **에반 유**가 AngularJS의 복잡성과 무거움을 개선하기 위해 개발했음  
   그는 구글에서 AngularJS를 사용하며 간단하고 유연한 프레임워크의 필요성을 느꼈음

2. **초기 목표**  
   Vue.js는 2013년에 시작되어 **가볍고 직관적인 프레임워크**를 목표로 개발되었음  
   AngularJS의 좋은 점(양방향 데이터 바인딩, 컴포넌트 구조 등)을 유지하면서 복잡성을 제거했음

3. **설계 철학**

   - **간단하고 직관적인 API**: 초보자도 쉽게 접근 가능했음
   - **컴포넌트 기반 아키텍처**: 재사용성과 유지보수성을 강조했음
   - **반응형 데이터 바인딩**: 데이터와 UI가 자동으로 동기화되었음
   - **경량화**: 빠른 로딩과 적은 번들 크기를 자랑했음
   - **점진적 채택 가능**: 기존 프로젝트에 부분적으로 통합 가능했음

4. **발전 과정**
   - **Vue 1.0 (2014)**: 초기 간단한 뷰 레이어로 시작되었음
   - **Vue 2.0 (2016)**: 성능 향상과 컴포넌트 시스템을 강화했음
   - **Vue 3.0 (2020)**: Composition API와 타입스크립트 지원을 추가하며 대규모 애플리케이션에 적합해졌음

## Vue.js 특징 및 장단점 요약

### 특징

1. **가상 DOM**
   - 가상 DOM에서 변화를 추적해 최적화된 결과를 실제 DOM에 반영하여 성능을 향상.
2. **양방향 바인딩**
   - `v-model`을 통해 데이터와 UI를 쉽게 동기화.
3. **간단한 설치**
   - CDN이나 보일러플레이트로 빠르게 시작 가능.
4. **낮은 학습 곡선**
   - HTML, CSS, JavaScript만 알면 쉽게 학습 가능.
5. **한국어 지원**
   - 공식 문서의 한국어 번역이 완벽에 가까움.

### 장점

- 빠르고 간단하게 설치 및 사용 가능.
- 직관적이고 쉬운 문법.
- 한국어로 된 학습 자료 및 공식 문서의 완벽한 지원.

### 단점

- **작은 커뮤니티**
  - 리액트 대비 개발 생태계 및 커뮤니티 규모가 작음.
- **후원처 부재**
  - 특정 대기업의 지원 없이 운영.
- **플러그인 부족**
  - 일부 기능은 플러그인을 직접 만들어야 할 수도 있음.

### 사용 사례

- 카카오, 바이브, 하나투어, 줌 등 다양한 국내외 사이트에서 사용.

## vue 사용법

### cdn

- vue.js를 사용하기 위해서는 vue.js 파일을 다운로드 받아서 사용할 수도 있지만, CDN을 사용하는 것이 가장 간단하다.
- CDN을 사용하면 외부 서버에 있는 파일을 가져와 사용할 수 있다.
- <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

### vite

- npm create vite@latest . => vue 선택 => js 선택 => npm install => npm run dev
- 익스텐션 깔아줘야함 : Vue-Official

### vue

- npm create vue@latest . => npm install => npm run dev
- vue 방식을 현업에서 제일 많이 사용함
  - toggle vue devtools