# HTML 기초 정리1

## 1. HTML 기본 구조

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Document Title</title>
  </head>
  <body>
    <!-- 문서의 내용이 들어가는 부분 -->
  </body>
</html>
```

- html: HTML 문서의 루트 요소.
- head: 문서 메타데이터와 외부 리소스 링크.
- meta: 메타데이터(예: 문자셋, 뷰포트 설정).
- title: 브라우저 탭에 표시되는 제목.
- body: 웹 페이지의 실제 콘텐츠가 들어가는 부분.

### 1.1 DTD(Document Type Definition)와 HTML 문서 구조

1. DTD란 무엇인가?
   **문서형 정의(DTD, Document Type Definition)**는 웹 브라우저에게 해당 문서가 어떤 형식을 따라야 하는지 알려주는 역할. DTD는 HTML이나 XML 문서의 유효성을 검증하는 기준이 되며, 브라우저가 문서를 올바르게 해석하고 렌더링할 수 있도록 도와줌.
   HTML 문서를 작성할 때, `<!DOCTYPE>` 선언은 항상 문서의 가장 첫 부분에 위치함

2. DTD의 역할
   DTD는 브라우저에게 현재 문서가 어떤 HTML 또는 XHTML 표준을 따르는지 명확하게 알려줌.

## 2. 주요 HTML 태그

- h1~h6: 제목 태그로, 숫자가 작을수록 큰 제목.

```
<h1>Heading Level 1</h1>
<h2>Heading Level 2</h2>
<h3>Heading Level 3</h3>
<h4>Heading Level 4</h4>
<h5>Heading Level 5</h5>
<h6>Heading Level 6</h6>
```

- p: 문단을 나타내는 태그.

```
<p>문단 내용</p>
```

- br: 줄바꿈을 나타내는 태그 (리액트 JSX에서는 </br>로 사용).

```
<p>첫 번째 줄<br>두 번째 줄</p>
```

- blockquote: 인용문을 나타내는 태그로, cite 속성을 통해 출처를 표시.

```
<blockquote cite="https://example.com">
  <p>인용된 문장입니다.</p>
  <cite>출처: Example</cite>
</blockquote>
```

- q: 짧은 인용문을 나타내는 인라인 요소.

```
<q cite="https://example.com">짧은 인용문</q>
```

## 3. 텍스트 추가 및 삭제

- ins: 새로 추가된 텍스트.

```
<p><ins>새로 추가된 내용</ins></p>
```

- del: 삭제된 텍스트.

```
<p><del>삭제된 내용</del></p>
```

## 4. 첨자 태그

- sub: 아랫첨자.

```
<p>H<sub>2</sub>O</p>
```

- sup: 윗첨자.

```
<p>10<sup>2</sup></p>
```

## 5. 강조 태그

- strong: 중요성을 나타내는 텍스트 (굵은 글씨로 강조).

```
<p><strong>중요한 텍스트</strong></p>
```

- em: 의미를 강조하는 텍스트 (기울임체).

```
<p><em>강조된 텍스트</em></p>
```

- b, i: 굵은 글씨(b)와 기울임체(i), 시맨틱을 갖지 않는 태그.

```
<p><b>굵은 글씨</b>와 <i>기울임체</i></p>
```

## 6. 공간 분할 태그

- div: 블록 요소로, 전체 레이아웃을 나눌 때 사용.

```
<div>
  <p>블록 요소 내 문단</p>
</div>
```

- span: 인라인 요소로, 문서 내에서 텍스트를 그룹화할 때 사용.

```
<p>문장 내에서 <span>인라인 요소</span>를 사용할 수 있습니다.</p>
```

## 7. 블록 요소와 인라인 요소

- 블록 요소: 한 줄을 다 차지하고, 새로운 줄에서 시작함 (예: div, h1~h6, p, blockquote).

```
<div>블록 요소</div>
<p>문단 요소</p>
```

- 인라인 요소: 한 줄을 다 차지하지 않고, 다른 요소들과 같은 줄에 표시됨 (예: span, a, img, strong, em).

```
<span>인라인 요소</span>
```

## 8. 부모, 자식, 형제 개념

- 부모 요소: 다른 요소를 감싸는 요소.
- 자식 요소: 부모 요소 안에 포함된 요소.
- 형제 요소: 같은 부모를 가진 요소들.

```
<div> <!-- 부모 요소 -->
  <p>자식 요소 1</p>
  <p>자식 요소 2 (형제 요소)</p>
</div>
```
