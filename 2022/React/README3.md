## 고차 컴포넌트(hoc, Higher Order Component)

- 컴포넌트 로직을 재사용하기 위한 React의 고급 기술
- 컴포넌트를 가져와 새 컴포넌트를 반환하는 함수

- React API의 일부가 아닌, React의 구성적 특성에서 나오는 패턴
- 컴포넌트는 props를 UI로 변환하는 반면, 고차 컴포넌트는 컴포넌트를 새로운 컴포넌트로 변환
- 리덕스의 `connect`와 Relay의 `createFragmentContainer` 와 같은 서드파티 라이브러리에서 흔히 볼 수 있음
- 파라미터로 컴포넌트를 받아오고, 함수 내부에서 새 컴포넌트를 만들고, 해당 컴포넌트 안에서 파라미터로 받아온 컴포넌트를 렌더링하는 것
- 받아온 props들은 그대로 파라미터로 받아온 컴포넌트에 넣어주고, 필요에 따라 props도 추가됨
- 이름은 `with___` 형태

## defaultValue (비제어 컴포넌트)

- React 렌더링 생명주기에서 폼 엘리먼트의 `value` 는 DOM의 `value` 를 대체
- 비제어 컴포넌트는 React의 초깃값을 지정, 그 이후의 업데이트는 제어하지 않는게 좋음

  ⇒ 이러한 경우 `defaultValue` 사용

  ⇒ 컴포넌트가 마운트된 후에 `defaultValue` 속성을 변경해도 DOM의 값이 업데이트 되지 않음

- `<input type=”checkbox”>`, `<input type=”radio”>` 는 `defaultChecked`
- `<select>, <area>` 는 `defaultValue` 지원
