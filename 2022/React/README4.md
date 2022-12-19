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

### useMutation

- `useQuery` 와 다르게 `mutation` 은 데이터를 생성, 업데이트, 삭제할 때 사용

  ```jsx
  // 1
  const mutation = useMutation(mutationFn);
  const mutation = useMutation(()=> axios.post('',data),{
  	onSuccess: () => {
  		console.log('성공');
  	},

  	onError: () => {
  		console.log('실패');
  	},
  	onSettled: () => {
  		console.log('onSettled'); // 성공이든 실패이든 ...
  	}

  // 2
  const mutation = useMutation({
  	mutationFn: mutationFn
  })
  const mutation = useMutation({
  	mutation: () => axios.post('', data),
  		onSuccess: () => {
  		console.log('성공');
  	},

  	onError: () => {
  		console.log('실패');
  	},
  	onSettled: () => {
  		console.log('onSettled'); // 성공이든 실패이든 ...
  	}
  })

  ```

  ```jsx
  // useMutation
  const {
    data,
    error,
    isError,
    isIdle,
    isLoading,
    isPaused,
    isSuccess,
    mutate,
    mutateAsync,
    reset,
    status,
  } = useMutation(mutationFn, {
    cacheTime,
    mutationKey,
    networkMode,
    onError,
    onMutate,
    onSettled,
    onSuccess,
    retry,
    retryDelay,
    useErrorBoundary,
    meta,
  });

  // mutate함수
  mutate(variables, {
    onError,
    onSettled,
    onSuccess,
  });
  ```

- 파라미터로 쿼리 키를 받지 않고 `mutationFn` 을 받음
- `mutationFn` 은 `promise` 처리가 이루어지는 함수
- `mutate` 는 `useMutation` 을 통해 작성한 내용들이 실행될 수 있도록 도와주는 `trigger` 역할

**invalidateQueries**

- `useQuery` 에는 `staleTime` 과 `cacheTime` 개념 존재
- 정해진 시간에 도달하지 않으면 새로운 데이터가 적재되어도 `useQuery` 는 변동없이 동일한 데이터를 화면에 보여줌
- 이를 해결해주는 `invalidateQueries`
- `invalidateQueries` 는 `useQuery` 에서 사용되는 `query key` 의 유효성을 제거
- 유효성을 제거하는 이유는 서버로부터 다시 데이터를 조회해오기 위함
- `const queryClient = useQueryClient();` → `queryClient.invalidateQueries('쿼리키');`

**setQueryData**

- `invalidateQueries` 말고도 데이터 업데이트해주는 방법
- 기존에 `query key` 에 매핑되어있는 데이터를 새롭게 정의

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

## react-dnd

- Flux 및 Redux 아키텍처와 유사

### Items and Types

- 드래그할 때 컴포넌트나 DOM 노드가 드래그되고있다고 말하지 않음
  - 특정 유형의 항목이 드래그되고있다고 말함
- 항목은 드래그되는 항목을 설명하는 일반 JS 개체
- 끌어온 데이터를 일반 개체로 설명하면 구성 요소를 분리된 상태로 유지하고 서로를 인식하지 못하는데 도움이 됨
- **유형**은 애플리케이션에서 전체 항목 클래스를 고유하게 식별하는 문자열 또는 기호

### Monitors

- 모니터를 통해 끌어서 놓기 상태 변화에 대응하여 구성 요소의 props를 업데이트할 수 있음
- 드래그 작업이 진행중, 진행중이 아님
- 현재 유형과 현재 항목이 있다, 없다
- _React DnD는_ 모니터라는 내부 상태 저장소에 대한 몇 개의 작은 래퍼를 통해 이 상태를 구성 요소에 노출

### Connectors

- 커넥터를 사용하면 미리 정의된 역할(드래그 소스, 드래그 미리보기 또는 드롭 대상) 중 하나를 렌더링 함수의 DOM 노드에 할당할 수 있음

ex)

- drag 대상

  ```jsx
  import { useDrag } from 'react-dnd';

  function Box() {
    const [{ isDragging }, drag] = useDrag({
      type: 'BOX',
      collect: (monitor) => ({
        isDragging: monitor.isDragging(),
      }),
    });

    return (
      <div ref={drag} style={{ opcity: isDragging ? 0.5 : 1 }}>
        {name}
        {isDragging && 'ㅋㅋ'}
      </div>
    );
  }
  ```

- drop 대상

  ```jsx
  import Box from './Box';
  import {useDrop} from 'react-dnd';

  function Basket(){
    const [{canDrop, isOver}, drop] = useDrop({
      accept: 'BOX',
      collect: (monitor) => ({
        isOver: monitor.isOver(),
        canDrop: monitor.canDrop(),
      }),
    });

  return(
    <Box/>
    <div
      ref={drop}
      role={'Dustbin'} // ??
      style={{backgroundColor: isOver ? 'gray' : 'red'}}>
    {canDrop ? 'Release to drop' : 'Drag a box here'}
    </div>
  ```

- App

  ```jsx
  import React from 'react';

  import { DndProvider } from 'react-dnd';
  import { HTML5Backend } from 'react-dnd-html5-backend';

  import Basket from './components/dnd/Basket';

  function App() {
    return (
      <DndProvider backend={HTML5Backend}>
        <Basket />
      </DndProvider>
    );
  }

  export default App;
  ```
