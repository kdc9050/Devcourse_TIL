## 프론트엔드에 대해서.. 특강

- `static web site`

  - 웹 서버에서 정적인 HTML 파일을 중심으로 제공
  - URL을 통해 해당 디렉토리에 있는 파일을 내려주는 방식
    - 디렉토리와 파일 구조가 곧 URL 구조

- `Common Gateway Interface (CGI)`

  - 정적인 HTML 제공의 한계를 탈피하기 위해 등장
  - Apache, Nginx와 같은 웹 서버와 프로그램 간의 통신을 위한 표준
  - 웹서버에 요청이 들어오면 외부 프로그램을 호출하여 그것을 처리한 결과를 내려줌

- `Server Side Template`
  - Web Server에서 정적인 HTML을 제공하는 게 아닌, Sever Application에서 여러가지 조건과 로직에 따라 HTML을 생성해서 내려주는 방식
  - Sever Application은 java, python 등 다양한 언어로 작성 가능
    - 하나의 언어에서도 다양한 템플릿 존재
  - HTML은 sever에서 내려주고 브라우저에서 랜더링하지만 브라우저에서 랜더린 된 이후 인터랙션 처리등을 js를 client에서 처리
  - 문제점
    - 서버에서 api나 database query등에서 시간이 오래걸릴경우 사용자에게 보여지는 화면이 늦어지는 문제
    - 서버에서 처리하는 부분이 많아질수록 서버의 부하가 커짐
- `Client Side Rendering`

  - 브라우저 성능의 발전과 js 스펙의 고도화로 렌더링을 클라이언트에서 다 처리
  - API와 웹 애플리케이션이 완전히 분리되어 있고 웹 애플리케이션은 HTML, CSS,JS만 있는 형태
    - 정적인 파일만 있기 때문에 static web site와 비슷
    - Application sever가 없기 때문에 신경 써야하는 부분이 적음
    - 배포 속도도 빠름
  - Application sever가 없어서 클라이언트 입장에서는 트래픽에 대응해서 스케일업이나 스케일 아웃을 할 필요가 없음
  - 보통 CDN이 알아서 해줌
    - 근데 트래픽 폭주로 인한 ui처리를 해주긴 해줘야 함
  - 기존 sever side 방식에서 해주던 url에 따른 라우팅 처리도 client에서 처리
    - 이게 바로 SPA(Single Page Application)
  - 문제점
    - Spa로 만들어진 애플리케이션 경우는 어느 페이지를 접속해도 매번 같은 index.html을 내려주기 때문에 meta:og 태그 관련 문제가 발생함
    - 초기에 body가 비어있다가 js가 로딩되고 코드들이 실행되면서 화면이 채워지는 방식이라 초기에 실행되는 js양이 많아질 수 밖에 없는데 체감속도가 생각보다 느리게 느껴질 수 있음
      - 특히 모바일 웹뷰에서.

- `Server Side Rendering`
  - node.js의 발전으로 client와 server에서 같은 언어를 쓸 수 있게 되면서 다시 rendering의 책임을 server로 돌리려는 움직임이 나타남
  - 단점
    - 더이상 서버리스가 아니게 되므로 서버관리 책임이 생김
    - 도커 등으로 말아서 배포할 경우 빌드 및 배포 시간이 csr 대비 길어짐
    - 세팅이 복잡해짐

## headless cms

- strapi
- cms ? => content management system
  - wordpress 나 제로보드 같은것.. velog도 cms
  - headless cms는 content를 표현하는 별도의 화면이 없을을 이야기함
  - headless chrome? => 브라우저를 띄우지 않고도 브라우저를 제어할 수 있는 방법

## 배포에 대한 이야기

- CSR 앱이 배포된다면
- index.html,css,js 같은 정적 파일들을 서버에 올리면 됨
- 정적인 자원만 서빙하면 되기 때문에 어떻게 빠르게 서빙될 수 있는지 체크하는게 중요
- 이 최적화에 따라 사용자가 느끼는 체감속도가 많이 달라질 수 있음
- 하지만 server가 끼어있다면 로컬에선 잘 되는데 배포에 실패하거나 배포한 곳에서만 안되는 경우 대부분 문제가 많이 일어남
- 로컬에서는 직접 서버를 띄워서 요청을 처리하거나 렌더링을 하는데 버셀이나 netlify등에 배포할 경우 serverless 형태로 바꿔서 올리기 때문
- 이 부분은 AWS나 GCP등에서 서버리스가 어떻게 실행되고 있는지 알아야 함
- 거의 대부분은 docker에 말아서 배포함
- 공통적인건
  - CSR,SSR기반은 인프라에 대해서 잘알아야함
  - 네트워크 인프라 관련해서도 알아야함
  - SSR의 기쁨과 슬픔이라는 인프콘 발표가 있음
  - HTTP 완벽 가이드 추천
  - node.js 디자인 패턴 바이블 추천
- 도커는 알아두면 좋음
- 쿠버네티스까지는 안가도 됨
- hydrateRoot
  - 서버에서 렌더링된 html을 클라이언트에서 다시 렌더링하는 것
