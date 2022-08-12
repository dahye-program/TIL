## JSX

```jsx
const element = <h1>Hello World</h1>;
```

- 문자열도, html도 아님
- Javascript 확장 문법으로, React element를 생성
- React에서는 본질적으로 렌더링 로직이 UI 로직(이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등)과 연결됨

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(element, document.getElementById('root'));
```

- 중괄호 안에 표현식
- 컴파일이 끝나면 JSX 표현식이 정규 JS 함수 호출이 되고, JS 객체로 인식됨
- 속성에 따옴표를 이용하여 문자열 리터럴 정의 가능
  `const element = <a href="https://www.reactjs.org"> link </a>;`
- 중괄호를 사용하여 속성에 JS 표현식 삽입 가능
  ``const element = <img src={user.avatarUrl}></img>;`
- `Babel` 은 JSX를 `React.createElement()` 호출로 컴파일
  ```jsx
  const element = <h1 className="greeting">Hello, world!</h1>;
  ////////////////////////////////
  const element = React.createElement(
    'h1',
    { className: 'greeting' },
    'Hello, world!'
  );
  ```

## element rendering

- `element` 는 React 의 가장 작은 단위
- 화면에 표시할 내용 기술
- 브라우저 DOM element와 달리 React element는 일반 객체이며 쉽게 생성 가능
- React element는 **불변객체**
- 생성한 이후에는 해당 element의 자식이나 속성 변경 불가능
- React DOM은 해당 element와 그 자식 element를 이전의 element와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트

## Components와 Props

- 컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나눔
- 함수 컴포넌트
  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```
  - 데이터를 가진 하나의 `props` 객체 인자를 받아 React element를 반환
- 클래스 컴포넌트

  ```jsx
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
  ```

  - 위의 유형의 컴포넌트들은 동일한 것

  ### 컴포넌트 렌더링

  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }

  const element = <Welcome name="Sara" />;
  ReactDOM.render(element, document.getElementById('root'));
  ```

  1. `<Welcome name="Sara" />` 엘리먼트로 `ReactDOM.render()`를 호출
  2. React는 `{name: 'Sara'}`를 props로 하여 `Welcome` 컴포넌트를 호출
  3. `Welcome` 컴포넌트는 결과적으로 `<h1>Hello, Sara</h1>` 엘리먼트를 반환
  4. React DOM은 `<h1>Hello, Sara</h1>` 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트

  - 컴포넌트 이름은 항상 대문자

  ### 컴포넌트 합성

  - 컴포넌트들은 자신의 출력에 다른 컴포넌트들 참조 가능

  ```jsx
  // Welcome을 여러번 렌더링
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }

  function App() {
    return (
      <div>
        <Welcome name="Sara" />
        <Welcome name="Cahal" />
        <Welcome name="Edite" />
      </div>
    );
  }

  ReactDOM.render(<App />, document.getElementById('root'));
  ```

  ### Props는 읽기 전용

  - 모든 컴포넌트는 컴포넌트 자체의 props를 수정하면 안됨
  - 모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 함

  ```jsx
  function sum(a, b) {
    return a + b;
  }
  ```

  - 순수 함수 - 동일한 입력값에 대해 동일한 결과 반환

  ```jsx
  function withdraw(account, amount) {
    account.total -= amount;
  }
  ```

  - 순수 함수가 아닌 예
