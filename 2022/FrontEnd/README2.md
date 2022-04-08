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