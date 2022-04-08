# FrontEnd
## HTML
### DOCTYPE

- HTML이 어떤 버전으로 작성되었는지 미리 선언
- 웹 브라우저가 내용을 올바르게 표시할 수 있도록 해주는 것
- **문서 형식 정의**

### meta 태그

- HTML 문서가 어떤 내용을 담고 있고, 키워드는 무엇이며, 누가 만들었는지에 대한 정보를 담고 있는 태그

### meta 태그의 요소

**charset**

```html
<meta charset = "utf-8" />
```

- 문서에서 허용하는 문자 집합에 대해 간단히 표시
- `utf-8` 은 전세계적인 character 집합으로 많은 언어의 문자들을 포함
- 웹 페이지에서 어떤 문자라도 취급할 수 있음을 의미

name

- 메타 요소가 어떤 정보의 형태를 가지고 있는지 표시
- `content` 요소는 실제 메타 데이터의 컨텐츠
- 머릿말 요약하는데 유용

```html
<meta name="author" content="Chris Mills" />

<meta
  name="description"
  content="The MDN Web Docs site provides information about Open Web technologies including HTML, CSS, and APIs for both Web sites and progressive web apps."
/>
```

- MDN 웹 페이지에 등록된 메타 태그의 `name` 과 `content` 속성
- 구글에 MDN을 검색하면 검색 엔진이 메타 태그의 `content` 내용을 검색 결과와 함께 추가적으로 보여줌


검색 엔진 최적화를 위한 메타 태그

```html
<head>
  <meta charset="UTF-8" />
  <meta name="keyword" content="HTML, meta, tag, element, reference" />
  <meta name="description" content="HTML meta tag page" />
  <meta name="author" content="TCPSchool" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>HTML meta tag</title>
</head>
```

1. 검색 엔진을 위한 키워드 정의

    ```html
    <meta name="keyword" content="HTML, meta, tag, element, reference" />
    ```

2. 웹 페이지에 대한 설명(description) 정의

    ```html
    <meta name="description" content="HTML meta tag page" />
    ```

3. 문서의 저자(author) 정의

    ```html
    <meta name="author" content="TCPSchool" />
    ```

4. 5초 뒤에 다른 페이지로 리다이렉트(redirect)

    ```html
    <meta http-equiv="refresh" content="5;url=http://www.tcpschool.com" />
    ```

5. 모든 장치에서 웹 사이트가 잘보이도록 뷰포트(viewport) 설정

    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    ```

## 웹 표준 및 웹 접근성

### 웹 표준

- 웹 상에서 표준적으로 사용되는 기술
- 웹 사이트를 어떠한 운영체제나 어떠한 브라우저에서 보더라도 동일하게 보여지도록 W3C(World Wide Web Consortium) 기구 표준에 맞추는 것
- 다양한 브라우저, 휴대폰 PDA, 장애인 지원용 프로그램에서도 대응이 가능하여 접근선 향상, 장애인과 고령자 등을 포함한 사용자층도 확대 가능
- 최신 웹 표준 버전은 HTML5, CSS3

### HTML5에서 추가된 내용

- `canvas` 기능 추가
    - JS를 통해 다양한 그림을 그릴 수 있는 공간 제공
    - WebGL과 같은 3D 기술의 구현이 웹 브라우저를 통해서도 가능해짐
- 모든 디바이스에서 웹페이지와 호환이 가능해짐
- 시멘틱 웹 기술 지원

### 웹 접근성

- 특정 대상에 한정되어있지 않고 모든 사용자가 웹사이트를 이용함에 있어 불편함이 없어야 함
- 모든 사람(장애인, 비장애인, 노인 등)이 차별 없이 웹사이트를 자유롭게 이용할 수 있게 하는 권리

### 웹 접근성에 맞는 마크업 예시

- 이미지는 `alt`, `IR` 로 대체 텍스트 제공(이미지에 대한 설명)
- 동영상은 대본이나 자막을 제공하고 자동재생 X
- title을 사용해 a태그에 대한 정보를 적절히 제공
- input태그에는 적절한 label 제공
- table에는 caption, summary, thead, tbody, th 등 사용
- 컨텐츠는 위에서 아래로 읽을 수 있는 선형구조(ex. 명확한 헤딩구조(h1~h6))

### 시멘틱 태그

- 의미 요소(HTML로 만든 문서에 추가적으로 의미 부여)
- 서로 관계가 있는 정보를 파악하고 콘텐츠가 어떤 맥락 안에 있는지 알기 쉽게 해줌
- 시멘틱 태그를 잘 사용 ⇒ 검색엔진을 통해 검색이 잘 될 수 있도록 도와줌


- header - 헤더
- nav - 내비게이션 바
- aside - 사이드 위치 공간
- section - 여러 중심 내용을 감싸는 공간
- article - 글자가 많이 들어가는 부분
- footer - 푸터

### 텍스트 관련 태그

**줄바꿈O 태그**

- `<h1>~<h6>` : 제목 표시
- `<hr>` : 수평줄(주제가 바뀔때)
- `<pre>` : 표시한 공백이 그대로 표시 (white space 속성의 pre 와 동일 in CSS)
- `<blockquote>` : 태그 안쪽 텍스트가 인용문임을 알리는 태그(전체적으로 들여쓰기됨)

**줄바꿈X 태그**

- `<strong>` : 중요한 내용임을 의미하며 볼드
- `<b>` : 중요하다는 의미를 가지지는 않지만 볼드
- `<em>` : 강조하고자 하는 내용을 의미하며 기울여 표시
- `<i>` : 특정 의미 담지 않고 기울여 표시
- `<q>` : 단락과 문장 중간에 줄바꿈 없이 인용문 표시 (따옴표)
- `<mark>` : 노란색 형광펜 표시

### SEO(Search Engine Optimization)

- 검색 엔진 최적화
- 검색 엔진이 웹페이지의 자료를 수집하거나 순위를 방식에 맞게 웹페이지를 구성하여 검색 결과의 상위에 올 수 있도록 함
- 검색어를 페이지에 적절하게 배치해야함
- 검색 엔진은 결과를 보여줄 때 HTML의 태그들을 분석
- 시멘틱한 문서가 유의미한 결과를 낳음

### 버튼 태그의 Default type

- `submit`
- form 태그 안에 form data와 관련 없는 버튼 태그를 만든 후 그 버튼을 누르면 form이 전송되는 경우가 있으니 버튼 태그는 꼭 type 명시
    - `submit` : 폼 제출
    - `reset` : 폼 안의 작성 내용 초기화
    - click 이벤트와 연결시켜 JS 활용

### section 태그와 article 태그의 차이

- `section` : 페이지의 주요부분 의미, 긴 글의 세부사항과 같은 관련 컨텐츠의 묶음 또는 탭 키 사용을 요하는 인터페이스를 가진 웹 어플리케이션에서의 페이지 묶음 단위 의미
- `article` : 문서나 사이트에서 독립된 컨텐츠 영역 지정, 이 부분을 다른 곳에 옮기더라도 분리되고 의미가 통해야 함