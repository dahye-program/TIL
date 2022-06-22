# FrontEnd

## Redux

- 리덕스는 상태관리 라이브러리 중 하나로 여러 가지 상태관리 라이브러리 중 가장 많이 사용되고 있음
- 리덕스는 Store(스토어)라는 변수를 이용하여 전역 상태관리
- 전역으로 상태를 관리하기 때문에 props <-> state를 통해 부모 컴포넌트에서 자식 컴포넌트로, 자식의 자식 컴포넌트로 내려주지 않아도 사용 가능

### Redux의 기본 원칙

1. 응용 프로그램의 전역상태는 단일 저장소 내의 트리에 저장

- Single source of truth
- 동일한 데이터는 항상 같은 곳에서 가지고 온다.
- 스토어라는 하나뿐인 데이터 공간 존재

2. 상태(state)는 읽기 전용

- State is read-only
- 리액트에서는 setState 메소드를 활용하여 상태 변경
- 리덕스에서도 액션이라는 객체를 통해 상태 변경

3. 순수 함수에 의해서 변경되어야 함

- Changes are made with pure function
- 변경은 순수함수로만 가능
- 리듀서와 연관되는 개념
- Store - Action - Reducer

## 웹팩(Webpack)

### GitHub 가 소개하는 webpack

> webpack is a module bundler. Its main purpose is to bundle JavaScript files for usage in a browser, yet it is also capable of transforming, bundling, or packaging just about any resource or asset.

⇒ webpack은 **모듈 번들러(묶음체)**이다. **브라우저에서 자바스크립트 파일들을 묶어서 사용하는 것을 목적**으로, 어떠한 자원(js, css, png, jpg)이나 자산 등을 **전송, 구축, 패키징이 가능하게 만드는 유용한 도구**이다.

즉, webpack은 **브라우저 상에서 자바스크립트 코드로 구성된 프로그램을 실행할 때 이에 필요한 자원들을 프로그램의 목적에 맞게 '모듈(Module)화'된 내용으로 제공**해주는 것

## 구성 요소

### 1) Entry

JavaScript (또는 HTML, CSS, png) 파일로 이루어진 **여러 모듈들을 포함하고 있는 파일을 정의**할 때 사용

만약 **애플리케이션이 App.js라는 파일 내부에 선언된 여러 모듈들로 실행된다면, App.js가 webpack의 Entry 파일**

→ 각 모듈들이 바라보는 **최상위 자바스크립트 파일(App.js)를 중심으로 번들링** 되는 것

→ 선언 방법 : **루트 경로(node_modules이 설치된 directory)**에 `webpack.config.js `파일 생성해서, 내부에 정의

```jsx
// 파일명: webpack.config.js
module.exports = {
  entry: "./App.js",
};
```

### 2) Output

webpack의 **번들링 결과물을 어디에 만들어낼 것인지, 어떤 이름을 만들 것인지 정의**할 때 사용

→ 선언 방법: **Entry와 동일한 루트 directory에 dist 폴더 생성**해두고, `bundle.js`라는 이름으로 **output 지정**

```jsx
// 파일명: webpack.config.js
module.exports = {
  entry: "./App.js",
  output: {
    path: "./dist",
    filename: "bundle.js",
  },
};
```

### 3) Loader

**webpack은 js 또는 JSON만 이해 가능한데, 이외의 다른 타입(HTML, CSS, png 등)의 파일들을 webpack이 이해할 수 있도록 변환해주는 역할**

```jsx
module.exports = {
  entry: "./App.js",
  output: {
    path: "./dist",
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.txt$/, // 적용할 파일의 타입 선언
        exclued: /node_modules/, // 로더 적용 제외
        use: "raw-loader", // 적용할 로더 정의
      },
    ],
  },
};
```

### 4) Plugin

**번들링(Bundling) 된 결과물에 대해서 적용**할 수 있는 속성 - **난독화**를 하거나, **번들된 css, js 파일들을 html 파일에 주입하는 역할**

로더(Loader)의 경우, 파일 단위로 작업이 이루어짐

```jsx
module.exports = {
  entry: "./App.js",
  output: {
    path: "./dist",
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.txt$/, // 적용할 파일의 타입 선언
        exclued: /node_modules/, // 로더 적용 제외
        use: "raw-loader", // 적용할 로더 정의
      },
    ],
  },
  plugins: [new HtmlWebpackPlugin()],
};
```

### webpack 장점

- 의존 모듈이 하나의 파일로 번들링되기 때문에 별도의 모듈 로더가 필요X
- HTML 파일에서 `script` 태그로 다수의 자바스크립트 파일을 로드해야 하는 번거로움을 줄일 수 있음

```html
<script src="/js/test.js"></script>
<script src="/js/api.js"></script>
<script src="/js/tags.js"></script>
<script src="/js/time.js"></script>
<script src="/js/search-box.js"></script>
<script src="/js/fragments.js"></script>
<script src="/js/testjs.js"></script>
```

⇒ 이렇게 모든 페이지마다 일일이 필요한 js파일들을 하드코딩 해야함..

- 모듈 시스템 관리
- 로더 사용
  (webpack은 js밖에 모르는데, js파일 뿐만 아니라 이미지, 폰트 등도 전부 모듈로 관리. js가 아닌 파일을 webpack이 이해할 수 있게 변경하는 역할이 로더)
- 빠른 컴파일

소프트웨어가 커지면 커질수록 각각의 세분화된 모듈 파일이 늘어나고, 모듈 단위의 파일들을 호출할 때 신경써야하는 각 변수들의 스코프 문제, 그리고 호출할 때 생겨나는 네트워크도 신경써야 한다.

⇒ 이러한 문제를 바탕으로 나온 것이 웹팩의 번들링 개념

### 번들링(Bundling)이란?

"어떤 것들을 묶는다" 라는 뜻으로, 기능별로 모듈화하나 js 파일들을 묶어주는 것

⇒ 여러 개로 흩어져 있는 파일들을 압축, 난독화 등을 하여 하나의 파일로 모아주는 역할(=번들러)

**⇒ 서로 연관(의존성)있는 여러 js 파일들을 하나의 번들 파일로 묶어주는 것**

**(꼭 js파일만이 아닌, 웹팩의 주요 구성요소인 로더(Loader)를 통해 다양한 타입의 파일들도 번들링 가능)**

#### 장점

- 이전에는 각 파일들마다 서버에 요청하여 자원을 얻어와야했던 반면, 같은 타입(html, css, js 등)의 파일을 묶어서 요청/응답을 받기 때문에 네트워크 코스트가 줄게 됨

- webpack 4버전 이상부터는 [development], [production] 두 가지의 mode 지원을 하면서, 특히 production 모드로 번들링을 진행할 경우, 코드 난독화, 압축, 최적화(Tree Shaking) 작업을 지원하기도 한다. (= 상용화된 프로그램을 사용자가 느끼기에 더욱 쾌적한 환경 및 보안까지 신경쓰면서 노출 시킬 수 있음)

- webpack의 주요 구성요소인 로더(Loader)가 일부 브라우저에서 지원이 되지 않는 ES6 형식의 js 파일을 ES5로 변환하여 사용 가능하게 함. 웹 개발 시 크롬 같은 대중적 브라우저만 고려하는 것이 아닌, 다른 브라우저들에 대해서도 커버 가능

## Babel : Javascript transpiler

어떤 특정 언어로 작성된 소스 코드를 다른 소스 코드로 변환하는 것

### transpiler가 필요한 이유?

모든 브라우저가 ES6+의 기능을 제공하지 않기 때문에 이를 ES5 코드로 변환시키는 과정 필요(Babel)

### compile과의 차이

**Compile**

- 입력과 출력의 추상화 수준이 다름
- C언어로 작성된 소스코드를 기계어로 변환

**Transpile**

- 입력과 출력의 추상화 수준이 비슷함
- Typescript → Javascript, C++ → C, CoffeScript → Javascript

## 쿠키

- 클라이언트(브라우저) 로컬에 저장되는 키와 값이 들어있는 작은 데이터 파일
- `document.cookie` ⇒ 현재 쿠키 정보
- 사용자 인증이 유효한 시간 명시, 유효 시간이 정해지면 브라우저가 종료되어도 인증 유지됨
- 쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조
- 클라이언트에 300개까지 쿠키 저장 가능, 하나의 도메인 당 20개의 값만 가질 수 있음, 하나의 쿠키값은 4KB까지 저장
- `Response Header` 에 Set-Cookie 속성 사용하면 클라이언트에 쿠키 만들 수 있음
- 쿠키는 사용자가 따로 요청하지 않아도 브라우저가 Request 시 Request Header를 넣어 자동으로 서버에 전송
- 쿠키는 만료 기한이 있는 키-값 저장소
- 서버는 요청 자체만으로는 그 요청이 누구에게서 오는 지 알 수 없어서 응답을 보낼 수 없음(이 때 쿠키에 나에 대한 정보를 담아 서버로 보내면 서버는 쿠키를 읽어 내가 누군지 파악, 쿠키는 처음부터 서버와 클라이언트 간의 지속적인 데이터 교환을 위해 만들어졌기 때문에 서버로 계속 전송됨)

### 쿠키 구성 요소

- 이름(Name) : 각각의 쿠키를 구별하는데 사용되는 이름
- 값(Value) : 쿠키의 이름과 관련된 값
- 유효시간(Expires) : 쿠키의 유지시간
- 도메인(Domain) : 쿠키를 전송할 도메인
- 경로(Path) : 쿠키를 전송할 요청 경로

### 쿠키 동작 방식

1. 클라이언트가 서버에게 페이지 요청
2. 서버에서 쿠키 생성
3. HTTP 헤더에 쿠키 포함시켜 응답
4. 브라우저가 종료되어도 쿠키 만료 기간이 있다면 클라이언트에서 보관
5. 같은 요청을 할 경우 HTTP 헤더에 쿠키를 함께 전송
6. 서버에서 쿠키를 읽어 이전 상태 정보를 변경할 필요가 있을 때 쿠키를 업데이트하여 변경된 쿠키를 HTTP 헤더에 포함시켜 응답

### 쿠키 사용 예

- 방문 사이트에서 로그인 시, “아이디와 비밀번호를 저장하시겠습니까?”
- 쇼핑몰의 장바구니 기능
- 자동 로그인
- 팝업 “오늘 더 이상 이 창을 보지 않음”
