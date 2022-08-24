# React

## react-query

- `server` 값을 `client`에 가져오거나 캐싱, 값 업데이트, 에러 핸들링 등 비동기 과정을 편하게 하는데 사용
- 캐싱
- `get` 한 데이터에 대하여 `update` 하면 자동으로 `get` 수행
- 데이터가 오래되었다고 판단되면 다시 `get` (`invalidateQueries`)
- 동일 데이터 여러번 요청 시 한번만 요청
- 무한 스크롤(`Infinite Queries`)
- 비동기 과정을 선언적으로 관리

react query는 기본적으로 캐싱된 데이터를 `stale` 한 상태로 여김

`stale` : ‘신선하지 않은' 이라는 뜻으로 서버에서 조회한 데이터는 그 당시의 데이터 snapshot이고, 외부 요쳥으로 서버 데이터가 변경되었다면 내 브라우저가 가진 데이터는 이미 오래된 낡은 데이터가 되었으므로 `stale` 하다고 표현 ⇒ 즉 최신화가 필요한 데이터라는 의미

다음의 경우 `refetch` 가 됨

- 새로운 `query instance` 가 마운트 될 때(페이지 이동했다가 왔을 때)
- 브라우저 화면을 이탈했다가 다시 `focus` 할 때
- 네트워크 재연결
- 특별히 설정한 `refetch interval` 에 의한 경우(`refetchInterval`)

`query` 에 별다른 `action` 이 없으면 `inactive` 상태로 캐시에 남아있다가 5분 뒤 메모리에서 사라짐

⇒ `cacheTime` 옵션을 설정해서 이 시간을 조정할 수 있음

### useQuery

- 데이터 `get` 하기 위한 api
- `post`, `update` 는 `useMutation` 사용
- 첫번째 파라미터로 `unique key` , 두번째 파라미터로 비동기 함수(api 호출 함수)
- 첫번째 파라미터로 설정한 `unique key` 는 다른 컴포넌트에서도 해당 키를 사용하면 호출 가능, `unique key` 는 string 과 배열을 받음
  - 배열로 넘기면 0번 값은 string값으로 다른 컴포넌트에서 부를 값이 들어가고 두번째 값을 넣으면 query 함수 내부에 파라미터로 해당 값 전달됨
- 리턴값은 api의 성공, 실패여부, api return값을 포함한 객체
- `useQuery` 는 비동기로 작동
  - 한 컴포넌트에 여러개의 `useQuery` 가 있다면 하나 끝나고 다음이 실행되는 것이 아닌 두개의 `useQuery` 가 동시에 실행
  - 여러개의 비동기 query가 있다면 `useQueries` 권유
- `enabled` 를 사용하면 `useQuery` 를 동기적으로 사용 가능

### Nullish coalescing operator(널 병합 연산자)

- **널 병합 연산자 (`??`)**는 왼쪽 피연산자가 `null` 또는 `undefined`일 때 오른쪽 피연산자를 반환하고, 그렇지 않으면 왼쪽 피연산자를 반환하는 논리 연산자
- `false` 에 해당할 경우 오른쪽 피연산자를 반환하는 `||` 와는 대조됨
- 우선순위는 `||` 의 바로 아래, 삼항 연산자의 바로 위

  ```jsx
  let foo;

  let text = foo || 'hello';
  ```

- `||` 의 경우 `boolean` 논리 연산자 때문에 강제 변환되어 `falsy` 한 값 `0, '', NaN, null, undefined` 은 반환되지 않음

### Optional chaning(?.)

- `null` 또는 `undefined` 일 수 있는 객체의 속성에 접근할 때 유용

  ```jsx
  let foo = {fooProp: 'hi'}

  console.log(foo.fooProp?.toUpperCase()); // HI
  console.log(foo.testProp?.toUpperCase()); // undefined

  -------------------------------
  onChange?.(props);
  ```

### `{...props}`

```jsx
return (
  <NavLink
    key={route.path}
    {...{
      href: route.path,
      label: route.name,
      active: navigation.current.parent.path === route.path,
      ...(route.path === '/' && { currentDateHtml }),
    }}
  />
);
```

```jsx
<NavLink
  key={route.path}
  {…{
  href: route.path,
  label: route.name,
  active: navigation.current.parent.path === route.path,
  …(route.path === ‘/’ && {currentDateHtml}),
  }}
/>
⇒
href={route.path}
label={route.name}
active={navigation.current.parent.path === route.path}
(route.path === ‘/’ 가 참일 경우)
currentDateHtml={currentDateHtml}
`...(route.path === '/' && {currentDateHtml})`
…(조건 && 실행문)
⇒ route.path === ‘/’ 이 참이면 {currentDateHtml: currentDataHtml}
obj ⇒ key, value가 이름이 같을 경우 생략
```
