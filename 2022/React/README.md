# React

## React를 사용하는 이유

### 1. 컴포넌트 기반의 화면 구성

- 리액트는 화면의 한 부분을 `컴포넌트` 라는 단위로 나눌 수 있고 독립적으로 관리가 가능
- 대규모 웹 애플리케이션에서 컴포넌트는 역할과 기능에 따라 따로 관리하기 용이하며 반복되는 부분 대체가 가능 => 코드 재사용성 up
- 컴포넌트 기반의 화면 구성으로 인해 빠르고 효율적으로 화면 구성 가능

### 2. Virtual DOM으로 인한 빠른 속도

- Virtual DOM은 UI의 이상적인 또는 가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 `실제` DOM과 동기화하는 프로그래밍(===재조정)
- 이러한 접근 방식이 React의 선언적 API를 가능하게 함<br>
  React에게 원하는 UI의 상태를 알려주면 DOM이 그 상태와 일치하도록 처리 => 앱 구축에 사용해야 하는 attribute 조작, event 처리, 수동 DOM 업데이트를 추상화

### 3. SPA(Single Page Application)

- 서버의 자원을 아낄 수 있고 사용자 경험 면에서 좋음
- 하지만 사용자와 인터랙션이 많은 경우에는 서버의 자원이 많이 사용되고 불필요한 트래픽 낭비

### 그래서 리액트를 왜 쓰는가?

1. `component` 를 사용하여 유지보수 용이(필요한 부분의 `component`만 렌더링, 최적화된 렌더링 가능)
2. 생태계가 넒고, 다양한 라이브러리 사용 가능
3. virtual DOM을 활용하여 빠른 렌더링 가능
4. React Native를 이용한 앱 개발도 가능

## Virtual DOM

### DOM(Document Object Model)

- XML이나 HTML문서에 접근하기 위한 일종의 인터페이스
- 문서의 구조화된 표현을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 문서 구조, 스타일, 내용 등을 변경할 수 있도록 도움

- 새로운 요청이 있을 경우 다음과 같은 형태로 리렌더링

```
HTTP response > DOM tree > CSSOM tree > render tree > painting
```

=> DOM의 속도는 느리지 않지만, 매번 새롭게 구성하기 때문에 양이 많으면 퍼포먼스가 떨어질 것임

### Virtual DOM

- 리액트는 Virtual DOM을 사용
- 실제 DOM에 접근하여 조작하는 대신, 이를 추상화한 자바스크립트 객체를 구성하여 사용

1. 전체 UI를 Virtual DOM에 리렌더링
2. 이전 내용과 현재 내용 비교
3. 바뀐 부분만 실제 DOM에 적용

## 클래스형 컴포넌트 vs 함수형 컴포넌트

### 클래스형 컴포넌트

- 객체지향 프로그래밍의 구조
- state를 초기화하기 위해서는 `constructor(생성자)` 함수 필요
- 생성자 함수를 통해 state를 초기화해야하기 때문에 함수형 컴포넌트에 비해 코드가 길고 사이즈가 커질 수 있음
- state 기능 및 라이프 사이클 기능 사용, 임의 메서드 정의 가능
- `render` 함수가 꼭 있어야 하고 `JSX`를 반환해야 함

### 함수형 컴포넌트

- Hooks를 사용하여 생성자 함수 없이 state 사용 가능
- 선언하기 좀 더 편하고 메모리 자원을 덜 사용
- 제공되는 hook 함수뿐만 아니라 커스텀 훅 생성하여 동작 가능
- 프로젝트를 완성하여 빌드한 후 배포할 때 함수형 컴포넌트를 사용한 결과물의 파일 크기가 더 작음
- state와 라이프사이클 API의 사용이 불가능했지만 v16.8 업데이트 이후 적용된 Hooks를 통해 해결함

## props와 state

### props

- 컴포넌트 속성을 설정할 때 사용하는 요소
- props값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정
- props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값이며, 컴포넌트 자신은 해당 props를 읽기 전용으로만 사용 가능
- props를 변경하려면 부모 컴포넌트에서 변경해주어야 함

props를 자식에서 부모에게 전달할 수 있는가?

1. NO. 부모 컴포넌트에서 설정할 수 있으며, 부모에서 자식으로만 데이터를 줄 수 있다.
2. 자식에서 부모로 데이터를 전송하려면 **함수를 이용**해야한다.

- 자식은 props를 사용해서 부모에게 데이터를 건네줄 수 없다.
  따라서 부모가 함수를 넣어 props로 자식에게 넘겨주면, 자식이 데이터를 파라미터로 넣어 호출하는 방식으로 동작한다. 즉, 부모가 props로 함수를 넣어주면 자식이 그 함수를 이용해 값을 건네주는 방식이다.

### state

- 컴포넌트 내부에서 바뀌는 값 의미

### state의 불변성 유지

- 객체는 실제 데이터 값이 아닌 참조 값을 가짐
- 복사하여 동일한 참조 값을 가지는 객체 중 하나라도 변경되면, 모든 객체의 내부 값이 변경됨
- `...`연산자를 통해 복사할 경우 A와 B가 같은 값을 가지더라도 새로운 객체를 할당 받은 상태가 되고 A와 B 내부의 값이 같더라도(같아 보이더라도) 참조하는 객체가 다르기 때문에 무결성 유지 가능
- (이미 복사를 한 프린트 물은 A 인쇄물에 낙서를 하더라도 B 인쇄물에 영향을 미치지 않음)
- 리액트에서는 데이터를 저장할 때 객체 형식 또는 배열 형식의 데이터를 많이 다루게 되는데 원본 배열이 변경되는 경우 의도한 동작과 다르게 동작할 수 있고 어떤 함수에 의해 부수효과(side effect)가 발생했는지 찾기 어려움

```jsx
let A = {
  name: "dahye",
  age: 25,
  job: "student",
};

B = { ...A };

console.log("A", A);
console.log("B", B);
/*
A { name: 'dahye', age: 25, job: 'student' }
B { name: 'dahye', age: 25, job: 'student' }
*/

B = { ...A, job: "frontend developer" };

console.log("A", A);
console.log("B", B);

/*
A { name: 'dahye', age: 25, job: 'student' }
B { name: 'dahye', age: 25, job: 'frontend developer' }
*/
```

## Basic

### ReactDOM.render

- 컴포넌트를 페이지에 렌더링
- `react-dom` 모듈 불러와 사용
- 첫번째 파라미터에는 페이지에 렌더링할 내용을 JSX 형태로 작성
- 두번째 파라미터에는 해당 JSX를 렌더링할 `document` 내부 요소 설정

### React.StrictMode

- 리액트 프로젝트에서 리액트의 레거시 기능들을 사용하지 못하게 함
- 문자열 ref, componentWillMount 등 나중에는 완전히 사라질 옛날 기능 사용 시 경고 출력

```jsx
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
	<React.StrictMode>
		<App />
	<React.StrictMode>,
	document.getElementById('root');
);
```

### function 과 arrow function 에서의 this

```jsx
function BlackDog() {
  this.name = "흰둥이";
  return {
    name: "검둥이",
    bark: function () {
      console.log(this.name + ": 멍멍!");
    },
  };
}
const blackDog = new BlackDog();
blackDog.bark();
```

- '검둥이: 멍멍' 출력

```jsx
function WhiteDog(){
  this.name = '흰둥이';
  return{
    name: '검둥이';
    bark: () => {
      console.log(this.name + ': 멍멍!');
    }
  }
}
```

- '흰둥이: 멍멍' 출력
