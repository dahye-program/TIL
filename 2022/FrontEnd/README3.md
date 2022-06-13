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
