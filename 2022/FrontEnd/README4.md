# FrontEnd

## event

### event bubbling

- 이벤트가 발생했을 때 상위 요소들로 이벤트가 전달되어가는 특성
- 자식에서 발생한 이벤트가 부모로 전파됨

### event capturing

- 브라우저로부터 이벤트가 발생한 요소까지 이벤트 전달
- 버블링과 정반대 …

  ```jsx
  target.addEventListener("click", function () {}, true);
  // true => 캡처링됨
  ```

### event.stopPropagation()

- 이벤트의 전파 막기

  ```jsx
  target.addEventListener("click", function (e) {
    e.stopPropagation();
  });
  ```

### 이벤트 위임?

- 버블링과 캡처링을 통해 이벤트 위임 …
- 하위 요소의 이벤트를 상위 요소에 위임 === 하위 요소의 이벤트를 상위 요소에서 제어
- 상위 요소에서 계속 감시하다가 하위 요소에서 이벤트 발생 시 상위 요소에서 제어

### event.target

- 부모 요소의 핸들러는 이벤트가 정확히 어디서 발생했는지 알 수 있음
- 이벤트가 발생한 가장 안쪽의 요소는 target 요소, `event.target` 으로 접근
- `event.target` : 실제 이벤트가 시작된 타깃 요소, 버블링이 진행되어도 변하지 X(자식)
- `this(event.currentTarget)` : 현재 요소, 현재 실행중인 **핸들러가 할당된** 요소 참조

### e.preventDefault()

- 브라우저에서 처리되는 기존 액션이 진행되지 않게 ….
- html에서 제공하는 기본 이벤트 방지 (form의 submit 전송 및 새로고침 또는 a의 href 를 통해 특정 사이트로 이동)

  ```jsx
  const handleClick = (test) => (e) => [
    e.preventDefault();
    console.log(e);
    console.log(test);
  }}

  <button onClick={handleClick('test')} />버튼</button>
  ```

### 커링(Currying)

- function(a, b, c) 처럼 단일 호출로 처리하는 함수를 f(a)(b)(c)와 같이 각각의 인수가 호출 가능한 프로세스로 호출된 후 병합되도록 변환하는 것

  ```jsx
  function handle(a) {
    return function (b) {
      console.log(a, b);
      return function (c) {
        console.log(a, b, c);
      };
    };
  }
  // 호출
  handle(1)(2)(3);
  ```

  ```jsx
  const handle = (a) => (b) => (c) => {
    console.log(a, b, c);
  };
  // 호출
  handle(1)(2)(3);
  ```
