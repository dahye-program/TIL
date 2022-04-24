# React
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

