# Javascript

## **Javascript Event Loop**

<aside>
💡 싱글스레드 기반으로 동작하는 Javascript,
이벤트 루프를 기반으로 하는 싱글스레드 NodeJS
</aside>

**Environment** - Javascript가 **동작**하는 환경

**Engine** - Javascript를 **해석하고 실행**시키는 엔진

**Javascript Engine**: Javascript로 작성한 코드를 해석, 실행하는 인터프리터(최근 Node가 등장하면서 server side에선 V8(구글) 이용)

**Rendering Engine**: HTML, CSS로 작성된 마크업 관련한 코드들을 콘텐츠로서 웹 페이지에 렌더링

## Javascript Engine

> **Call Stack, Task Queue(Event queue), Heap 영역으로 나뉨**
>

**Event Loop**가 Task Queue에 들어가는 task들을 관리

### Call Stack

- JS는 하나의 Call Stack을 사용

  ⇒ Run to Completion(하나의 함수가 실행되면 해당 함수의 실행이 끝날 때까지 다른 어떤 task도 수행될 수 없음)

  ⇒ 요청이 들어올때마다 해당 요청을 순차적으로 Call Stack에 담아 처리(push/pop)


### Task Queue(Event Queue)

- JS의 런타임 환경에서는 처리해야하는 task들을 임시 저장하는 대기 큐(Task Queue or Event Queue) 존재
- Call Stack이 비어졌을 때, Task Queue에 들어온 순서대로 수행
- Task Queue(Event Queue)에서 대기하고 있는 Event들은 한 번에 하나씩 Call Stack으로 호출되어 처리됨

```jsx
setTimeout(function(){
	console.log('first');
},0);
console.log('second');

----------출력--------------
second
first
```

- JS에서 비동기로 호출되는 함수들은 Call Stack에 쌓이지 않고 Task Queue에 enqueue됨
    - 이벤트에 의해 실행되는 함수(핸들러)
    - JS 엔진이 아닌 Web API영역에 따로 정의되어있는 함수

Ex)

```jsx
function test1(){
	console.log('test1');
	test2();
}

function test2(){
	let timer = setTimeout(function(){
		console.log('test2');
	},0);
	test3();
}

function test3(){
	console.log('test3');
}

test1(); 

----------출력--------------
test1
test3
test2
```

⇒ test1함수가 호출되며 Call Stack에 push 되어 실행 ‘test1’ 출력

⇒ test2함수 호출되어 콜스택에 push , setTimeout함수는 실행되지 않음

⇒ test2함수의 내부 핸들러(익명함수)는 Task Queue(Event Queue)에 enqueue됨

⇒ test3함수가 Call Stack에 push되고 실행되어 ‘test3’ 출력, pop됨

⇒ test2함수, test1함수도 pop

⇒ Call Stack이 비어지고 Task Queue의 head에서 하나의 event(setTimeout함수)가 dequeue되어 Call Stack에 push

⇒ setTimeout함수 실행되어 ‘test2’ 출력

- 이벤트에 걸려있는 핸들러는 절대 먼저 실행될 수 없음

### Event Loop

- 현재 실행중인 task가 있는지 없는지 확인
- Task Queue에 task가 있는지 없는지 확인