# React

## Hooks

### useState

- 가장 기본적인 Hook(배열 비구조화 할당 이용 함수)
- 함수 컴포넌트에서도 가변적인 상태를 지닐 수 있도록 해줌
- `const [value, setValue] = useState('0');` 0 => 기본값
- `useState` 함수가 호출되면 배열을 반환
- 첫 번째 원소는 상태 값, 두 번째 원소는 상태를 설정하는 함수(Setter 함수)
- Setter 함수에 파라미터를 넣어 호출하면 전달받은 파라미터로 값이 바뀌고 컴포넌트가 리렌더링됨

  ```jsx
  const [state, setState] = useState(initialState);
  ```

  이전 `state` 를 사용해서 새로운 `state` 를 계산하는 경우, 이전 값을 받아 갱신된 값을 반환

  ```jsx
  const [state, setState] = useState(initialState);

  function handleClick() {
    setState((prevState) => prevState + 1);
  }

  // 또는
  const [focused, setFocused] = useState(false);

  function handleFocused() {
    setFocused((prevFocused) => !prevFocused);
  }
  ```

  - 갱신 객체를 자동으로 합치지는 않음

  ```jsx
  const [state, setState] = useState({});
  setState((prevState) => {
    return { ...prevState, ...updatedValues };
  });
  ```

  - 초기 `state` 가 고비용 계산의 결과라면,, 초기 렌더링시에만 실행될 함수를 대신 제공

  ```jsx
  const [state, setState] = useState(() => {
    const initialState = ff(props);
    return initialState;
  });
  ```

### useEffect

- 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정
- `useEffect(()=>{console.log('렌더링될 때마다 출력')});`

1. 마운트될 때만 실행

- 컴포넌트가 화면에 맨 처음 렌더링될 때만 실행
- 업데이트 시에는 실행 X
- 두 번째 파라미터로 비어있는 배열 삽입
- `useEffect(()=>{console.log('마운트될 때만 출력');}, []);`

2. 특정 값이 업데이트될 때만 실행

- 특정 값이 변경될 때만 호출
- 두 번째 파라미터로 전달되는 배열 안에 검사하고 싶은 값 삽입
- `useEffect(()=>{console.log(name);}, [name]);

  ```jsx
  useEffect(() => {
    // === componentDidMount
    const subscription = props.source.subscribe();
    return () => {
      // componentWillUnmount
      subscription.unsubscribe();
    };
  }, [props.source]);
  // props.source 가 변경시에만 동작
  ```

  - 두 번째 인자로 dependency
  - 한 번만 실행시 두 번째 인자로 [] (빈 배열) ⇒ 의존하지 않으므로 다시 실행할 필요가 없다는 뜻

### useReducer

- useState보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트 할 때 사용
- 리듀서는 현재 상태와 업데이트를 위해 필요한 정보를 담은 액션(action)값을 전달받아 새로운 상태를 반환하는 함수
- 리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 지켜주어야 함
- 리덕스에서 사용하는 액션 객체에는 `type` 필드가 꼭 있어야 하지만, useReducer에서 사용하는 액션 객체는 반드시 `type` 을 지니고 있을 필요가 없고 객체가 아니라 문자열, 숫자도 가능
- useReducer의 첫 번째 파라미터에는 리듀서 함수, 두 번째 파라미터에는 해당 리듀서의 기본값 삽입
- 해당 Hook은 `state` 값과 `dispatch` 함수를 받아오는데 이 때, `state` 는 현재 가리키고 있는 상태, `dispatch` 는 액션을 발생시키는 함수 ⇒ `dispatch(action)` 과 같은 형태
- 가장 큰 장점은 컴포넌트 업데이트 로직을 컴포넌트 바깥으로 빼낼 수 있다는 것

  ```jsx
  import { useReducer } from 'react';

  function reducer(state, action) {
    switch (action.type) {
      case 'INCREMENT':
        return { value: state.value + 1 };
      case 'DECREMENT':
        return { value: state.value - 1 };
      default:
        return state;
    }
  }

  const Counter = () => {
    const [state, dispatch] = useReducer(reducer, { value: 0 });
    return (
      <div>
        <p>현재 카운터 값은 {state.value}</p>
        <button onClick={() => dispatch({ type: 'INCREMENT' })}>+1</button>
        <button onClick={() => dispatch({ type: 'DECREMENT' })}>-1</button>
      </div>
    );
  };
  ```

### useMemo

- 함수 컴포넌트 내부에서 발생하는 연산 최적화
- 렌더링 과정에서 특정 값이 바뀌었을 때만 연산 실행, 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식

  ```jsx
  const getAverage = (numbers) => {
    // 평균값 계산
  };

  const Average = () => {
    const [list, setList] = useState([]);
    const avg = useMemo(() => getAverage(list), [list]);
    // list의 값 변화가 있을 때만 getAverage 함수 호출
  };
  ```

- **메모이제이션**된 값 반환
- dependency가 변경되었을 때 메모이제이션된 값만 다시 계산
- 이 최적화는 모든 렌더링 시의 고비용 계산 방지

  ```jsx
  // a에 b+1값을 넣어주고, b값이 변할 때마다 실행됨
  const a = useMemo((return b+1)=>{}, [b])
  ```

### useCallback

- `useMemo` 와 비슷
- 렌더링 성능 최적화
- 첫 번째 파라미터에 생성하고 싶은 함수, 두 번째 파라미터에 배열 삽입
- 두 번째 파라미터에 삽입되는 배열은 어떤 값이 바뀌었을 때 함수를 새로 생성해야 하는지 명시
- 비어있는 배열을 넣게 되면 컴포넌트가 렌더링될 때 만들었던 함수를 계속해서 재사용
- 어떤 배열을 넣으면 해당 배열의 변화가 있을 때 새로 만들어진 함수 사용
- 함수 내부에서 상태 값에 의존해야 할 때는 그 값을 두 번째 파라미터 안에 포함해줘야 함

  ```jsx
  const Average = () => {
    const [list, setList] = useState([]);
    const [number, setNumber] = useState('');

    const onChange = useCallback(e=>{
      setNumber(e.target.value);
    }, []); // 컴포넌트가 처음 렌더링될 때만 함수 생성

    const onInsert = useCallback(e=>{
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
    }, [number, list]); // number 또는 list가 바뀌었을 때만 함수 생성

    return(
      <div>
        <input value={number} onChange={onChange} />
        <button onClick={onInsert}등록</button>
        <ul>
          {list.map((value, index) => (
            <li key={index}>{value}</li>
          ))}
        </ul>
    );
  };
  ```

- 메모이제이션된 콜백함수 반환
- `useCallback(fn, deps)` 은 `useMemo(()=>fn, deps)` 와 같음

  ```jsx
  const memoizedCallback = useCallback(() => {
    doSomething(a, b);
  }, [a, b]);
  ```

### useRef

- 함수 컴포넌트에서 ref를 쉽게 사용할 수 있도록 함
- 렌더링과 상관없이

  ```jsx
  const Average = () => {
    const [list, setList] = useState([]);
    const [number, setNumber] = useState('');
    const inputEl = useRef(null);

    const onChange = useCallback(e=>{
      setNumber(e.target.value);
    }, []); // 컴포넌트가 처음 렌더링될 때만 함수 생성

    const onInsert = useCallback(e=>{
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber('');
      inputEl.current.focus();
    }, [number, list]); // number 또는 list가 바뀌었을 때만 함수 생성

    return(
      <div>
        <input value={number} onChange={onChange} ref={inputEl} />
        <button onClick={onInsert} 등록</button>
        <ul>
          {list.map((value, index) => (
            <li key={index}>{value}</li>
          ))}
        </ul>
    );
  };
  ```
