# FrontEnd

## Redux

- 리덕스는 상태관리 라이브러리 중 하나로 여러 가지 상태관리 라이브러리 중 가장 많이 사용되고 있음
- 리덕스는 Store(스토어)라는 변수를 이용하여 전역 상태관리
- 전역으로 상태를 관리하기 때문에 props <-> state를 통해 부모 컴포넌트에서 자식 컴포넌트로, 자식의 자식 컴포넌트로 내려주지 않아도 사용 가능

### Redux의 기본 원칙

1. 응용 프로그램의 전역상태는 단일 저장소 내의 트리에 저장

- Single source of truth
- 동일한 데이터는 항상 같은 곳에서 가지고 온다.
- 스토어라는 하나뿐인 데이터 공간 존재

2. 상태(state)는 읽기 전용

- State is read-only
- 리액트에서는 setState 메소드를 활용하여 상태 변경
- 리덕스에서도 액션이라는 객체를 통해 상태 변경

3. 순수 함수에 의해서 변경되어야 함

- Changes are made with pure function
- 변경은 순수함수로만 가능
- 리듀서와 연관되는 개념
- Store - Action - Reducer
