# React

## Hooks

### useState

- 가장 기본적인 Hook(배열 비구조화 할당 이용 함수)
- 함수 컴포넌트에서도 가변적인 상태를 지닐 수 있도록 해줌
- `const [value, setValue] = useState('0');` 0 => 기본값
- `useState` 함수가 호출되면 배열을 반환
- 첫 번째 원소는 상태 값, 두 번째 원소는 상태를 설정하는 함수(Setter 함수)
- Setter 함수에 파라미터를 넣어 호출하면 전달받은 파라미터로 값이 바뀌고 컴포넌트가 리렌더링됨
