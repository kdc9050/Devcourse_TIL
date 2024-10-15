# HTML 기초 정리2

## 1. 목록 태그

### 1.1 ul (비순서형 목록)와 li

- ul: unordered list (비순서형 목록).
- li: list item (목록 항목).
- type 속성: disc, circle, square로 목록의 기호를 설정.

```
<ul type="disc">
  <li>사과</li>
  <li>바나나</li>
  <li>체리</li>
</ul>
```

### 1.2 ol (순서형 목록)와 li

- ol: ordered list (순서형 목록).
- type 속성: 1, A, a, I, i로 숫자, 대문자, 소문자 등을 지정.

```
<ol type="a">
  <li>아침 먹기</li>
  <li>점심 먹기</li>
  <li>저녁 먹기</li>
</ol>
```

### 1.3 dl (정의형 목록), dt (정의 항목), dd (정의 설명)

- dl: definition list (정의형 목록).
- dt: definition term (정의 항목).
- dd: definition description (정의 설명).

```
<dl>
  <dt>HTML</dt>
  <dd>HTML은 웹 페이지의 구조를 만드는 언어입니다.</dd>
  <dt>CSS</dt>
  <dd>CSS는 웹 페이지의 디자인을 담당하는 언어입니다.</dd>
</dl>
```

## 2. 링크 태그

- a: 링크를 나타내는 태그.
- href: 연결할 URL 경로를 지정.
- target: 링크를 열 위치를 지정 (\_blank, \_self, \_parent, \_top).

```
<a href="https://www.google.com" target="_blank">구글</a>
```

- 보안 속성
  `rel="noreferrer"`: 보안상의 이유로 이전 페이지 정보를 숨김.
  `rel="noopener"`: 부모 창의 URL을 알 수 없도록 방지.
- document.referrer:

```
<a href="javascript:alert(document.referrer)">이전 페이지</a>
```

-> 그래서 target="\_blank"와 함께 사용

- `window.opener.location` : 사용하면 부모창의 주소를 알 수 있음, 해킹에 사용될 수 있음
- `rel="noopener"` : 보안상의 이유로 사용 - 안전하게 링크를 열기 -> 최종적으로 blank쓸때는 rel="noreferrer noopener"를 사용

```
<a href="https://www.google.com" target="_blank" rel="noreferrer noopener">구글</a>
```

## 3. 이미지 태그

### 3.1 src 속성: 이미지 경로 설정

```
<img src="1.webp" width="100" height="100" alt="다리">
```

### 3.2 상대적 경로

- 현재 디렉토리: ./이미지파일명.
- 상위 디렉토리: ../이미지파일명.
- 루트 디렉토리: /이미지파일명.

### 3.3 절대적 경로

- 웹상의 URL로 경로를 지정.

```
<img src="http://example.com/images/1.jpg" alt="이미지">
```

### 3.4 alt 속성: 이미지 대체 텍스트

```
<img src="1.webp" width="100" height="100" alt="다리">
```

## 4. 폼 태그 및 관련 요소

### 4.1 form: 폼을 시작하는 태그

- action: 데이터를 전송할 서버의 URL.
- method: 폼 데이터를 전송하는 방식 (GET, POST).

```
<form action="/submit" method="POST">
  <!-- 폼 내용 -->
</form>
```

### 4.2 input: 사용자 입력 요소

- type 속성: text, password, email, radio, checkbox 등.

```
<label for="id">아이디</label>
<input type="text" id="id" placeholder="아이디">
<br>
<label for="password">비밀번호</label>
<input type="password" id="password" placeholder="비밀번호">
<br>
<input type="submit" value="로그인">
```

### 4.3 textarea: 여러 줄의 텍스트를 입력받는 요소

```
<textarea placeholder="여러 줄의 텍스트를 입력하세요."></textarea>
```

### 4.4 button: 클릭 가능한 버튼

- type 속성: submit, reset, button.

```
<button type="submit">제출</button>
<button type="reset">초기화</button>
<button type="button">일반 버튼</button>
```

### 4.5 fieldset과 legend

- fieldset: 폼 요소들을 그룹화할 때 사용.
- legend: 그룹의 제목을 나타냄.

```
<form>
  <fieldset>
    <legend>회원 가입</legend>
    <label for="username">사용자 이름:</label>
    <input type="text" id="username" name="username" placeholder="사용자 이름">
    <br>
    <label for="email">이메일:</label>
    <input type="email" id="email" name="email" placeholder="이메일">
    <br>
    <label for="age">나이:</label>
    <input type="number" id="age" name="age" placeholder="나이">
    <br>
    <input type="submit" value="가입하기">
  </fieldset>
</form>
```

### 4.6 select: 드롭다운 목록

```
<select name="cars">
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="mercedes">Mercedes</option>
  <option value="audi">Audi</option>
</select>
```

#### 4.6.1 optgroup: 옵션을 그룹화하는 요소

```
<select>
  <optgroup label="과일">
    <option value="사과">사과</option>
    <option value="바나나">바나나</option>
  </optgroup>
  <optgroup label="채소">
    <option value="당근">당근</option>
    <option value="브로콜리">브로콜리</option>
  </optgroup>
</select>
```

#### 4.6.2 option: 드롭다운 목록의 옵션을 생성하는 요소

- value 속성: 서버로 전송되는 값
- size 속성: 보여지는 옵션의 개수
- multiple 속성: 여러 옵션을 선택할 수 있도록 하는 속성
- selected 속성: 기본으로 선택되어 있는 옵션을 지정하는 속성

```
<select multiple size="3">
  <option value="사과">사과</option>
  <option value="바나나" selected>바나나</option>
  <option value="체리">체리</option>
</select>
```

### 4.7 form 속성

- disabled 속성: 비활성화 상태로 만드는 속성
- readonly 속성: 읽기 전용 상태로 만드는 속성
- maxlength 속성: 입력할 수 있는 최대 글자 수를 지정하는 속성
- placeholder 속성: 입력란에 힌트를 제공하는 속성

```
<input type="text" placeholder="이메일" maxlength="30" readonly>
```

## 5. 표 (table)

- 행과 열로 이루어진 이차원 데이터 구조 / 테이블은 기본적으로 반응형임

### 5.1 행(row)과 열(column)로 이루어짐

### 5.2 필수 태그: table, tr, td

- table: 표 전체를 감싸는 태그
- th (table header): 제목 셀을 나타내는 태그
- tr (table row): 행을 나타내는 태그
- td (table data): 셀을 나타내는 태그
  => th, td는 열(column)을 나타냄

```
<table border="1">
  <caption>과일 목록</caption>
  <thead>
    <tr>
      <th>과일 이름</th>
      <th>가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>사과</td>
      <td>1000원</td>
    </tr>
    <tr>
      <td>바나나</td>
      <td>800원</td>
    </tr>
  </tbody>
</table>
```

- border 속성: 표의 테두리를 지정하는 속성 (예: border="1")
- colspan 속성: 셀을 합치는 속성 (가로) (예: colspan="2")
- rowspan 속성: 셀을 합치는 속성 (세로) (예: rowspan="2")

```
<table border="1">
  <tr>
    <th colspan="2">과일 목록</th>
  </tr>
  <tr>
    <td rowspan="2">사과</td>
    <td>1000원</td>
  </tr>
  <tr>
    <td>1000원</td>
  </tr>
</table>
```

### 5.3 caption: 표의 제목을 나타내는 태그

```
<table>
  <caption>과일 가격표</caption>
  ...
</table>
```

### 5.4 thead, tbody, tfoot: 표의 구조를 나타내는 태그

- thead: 표의 머리글을 나타내는 태그
- tbody: 표의 본문을 나타내는 태그
- tfoot: 표의 바닥글을 나타내는 태그

```
<table>
  <thead>
    <tr>
      <th>과일</th>
      <th>가격</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>사과</td>
      <td>1000원</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>총합</td>
      <td>1000원</td>
    </tr>
  </tfoot>
</table>
```

- `그룹화 해주는 이유: 웹 접근성을 높이기 위해서 → 스크린 리더 사용자가 표의 구조를 이해하기 쉽게 하기 위해서`

### 5.5 colgroup, col: 열을 그룹화하는 태그

- colgroup: 열을 그룹화하는 태그
- col: 열을 나타내는 태그

```
<table>
  <colgroup>
    <col span="2" style="background-color: yellow">
    <col style="background-color: red">
  </colgroup>
  <tr>
    <td>사과</td>
    <td>1000원</td>
    <td>2000원</td>
  </tr>
</table>
```

### 5.6 scope 속성: th 요소의 범위를 지정하는 속성

- row: 행을 나타냄
- col: 열을 나타냄
- rowgroup: 행 그룹을 나타냄
- colgroup: 열 그룹을 나타냄

```
<table>
  <tr>
    <th scope="col">과일</th>
    <th scope="col">가격</th>
  </tr>
</table>
```

- `쓰는 이유: 방향을 지정하면 스크린 리더가 읽을 때 표의 구조를 이해하기 쉽게 함`
