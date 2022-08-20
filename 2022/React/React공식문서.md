# React

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
  // 순수 함수 - 동일한 입력값에 대해 동일한 결과 반환
  function sum(a, b) {
    return a + b;
  }
  ```

  ```jsx
  // 순수 함수가 아닌 예
  function withdraw(account, amount) {
    account.total -= amount;
  }
  ```

## event 처리

- React의 이벤트 처리는 DOM 방식의 이벤트 처리와 매우 유사
- React의 이벤트는 카멜 케이스(camelCase) 사용
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러 전달

  ```jsx
  <button onclick="onclickfunc()">버튼</button>
  =>
  <button onClick={onClickFunc}>버튼</button>
  ```

- false를 반환하더라도 기본 동작 방지 불가능
- `preventDefault` 을 명시적으로 호출해야 함

  ```jsx
  // js에서는
  <form onsubmit="console.log('You clicked submit.'); return false">
    <button type="submit">Submit</button>
  </form>;

  // React에서는
  function Form() {
    function handleSubmit(e) {
      e.preventDefault();
      console.log('You clicked submit.');
    }

    return (
      <form onSubmit={handleSubmit}>
        <button type="submit">Submit</button>
      </form>
    );
  }
  ```

- react에서 e는 합성 이벤트
- 브라우저 고유 이벤트와 정확히 동일하게 동작하지는 않음
- React를 사용할 때 DOM 엘리먼트가 생성된 후 리스너를 추가하기 위해 `addEventListener`
  를 호출할 필요 없음. 대신, 엘리먼트가 처음 렌더링될 때 리스너를 제공하면 됨
- 일반적으로 `onClick={this.handleClick}`과 같이 뒤에 `()`를 사용하지 않고 메서드를 참조할 경우, 해당 메서드를 바인딩해야함
- `bind` 를 호출하는 것이 불편하다면, 콜백에 화살표함수 사용
  - `<button onClick={() => handleClick()}>`

## 조건부 렌더링

- React 에서는 원하는 동작을 캡슐화하는 컴포넌트를 생성할 수 있음
- `true && expression` ⇒ 항상 `expression` 으로 표현
- `false && expression` ⇒ 항상 `false`
- `조건 ? 참 : 거짓`
- 컴포넌트 렌더링 막기 ⇒ 렌더링 결과 출력 대신 `null` 반환
  - 컴포넌트의 `render` 메서드로부터 `null`을 반환하는 것은 생명주기 메서드 호출에 영향을 주지 않음

## 리스트와 key

- `map` 함수를 사용하여 배열을 각 항목에 대하여 `<li>` 엘리먼트를 반환하여 렌더링
- 위와 같이 실행하면 리스트의 각 항목에 `key` 를 넣어야 한다는 경고가 표시됨
- `key` 는 엘리먼트 리스트를 만들때 포함해야 하는 특수한 문자열 속성

### key

- key는 리액트가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 도움
- 엘리먼트에 안정적인 고유성 부여
- 해당 항목을 고유하게 식별할 수 있는 문자열을 사용, 대부분 데이터의 ID를 key로 사용
- 배열 안에서 형제 사이에 고유해야 하고 전체 범위에서 고유할 필요 X
- 두개의 다른 배열을 만들 때 동일한 key 사용 가능
