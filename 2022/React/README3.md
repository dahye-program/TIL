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

## cloneElement()

```jsx
React.cloneElement(element, [config], [...children]);
```

- `element` 를 기준으로 새로운 `React element`를 복사하고 반환
- `config` 는 `key` , `ref` 그리고 모든 새로운 `props` 포함
- 새로운 `element` 는 원본 `element` 가 가졌던 `props` 가 새로운 `props` 와 얕게 합쳐진 뒤 주어짐
- 새로운 자식들은 기존의 자식들 대체
- `config` 에 `key` 와 `ref` 가 없다면 원본 `element` 의 `key` 와 `ref` 는 그대로 유지

`React.cloneElement()` 는 아래 구문과 거의 동일

```jsx
<element.type {...element.props} {...props}>
  {children}
</element.type>
```

- but, `ref` 들이 유지된다는 점이 다름
  - 조상이 가지고 있을 `ref` 를 사용하여 자식에게 접근하는 것이 허용됨
  - 새로운 `element` 에 덧붙여지는 것과 동일한 `ref` 를 얻을 수 있음
  - 새로운 `ref` 가 있다면 이전 값 대체
