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

## Scope

- 현재 실행되는 컨텍스트
  - context: 값과 표현식이 표현되거나 참조될 수 있음을 의미
- 만약 변수 또는 다른 표현식이 해당 스코프 내에 있지 않다면 사용할 수 없음
- 또한 계층적인 구조를 가져 하위 스코프는 상위 스코프에 접근할 수 있지만 반대는 불가능함

**함수 레벨 스코프**

- 함수 내에서 선언된 변수는 함수 내에서만 유효
- 함수 외부에서 참조할 수 없음
- 함수 내부에서 선언한 변수 = 지역 변수
- 함수 외부에서 선언한 변수 = 전역 변수

**블록 레벨 스코프**

- 모든 코드 블록(함수, If, for, while, try/catch 등) 내에서 선언된 변수는 코드 블록 내에서만 유효
- 코드 블록 외부에서 참조 불가능
- 코드 블록 내부에서 선언한 변수 = 지역 변수

<aside>
💡 일시적 사각지대(TDZ: Temporal Dead Zone): 변수 선언부터 초기화 사이의 지대

</aside>

## Closure

- **Closure는 두 개의 함수로 만들어진 환경으로 이루어진 특별한 객체의 한 종류**

  환경: 클로저가 생성될 때 그 범위에 있던 여러 지역 변수들이 포함된 `context`

  ⇒ private 속성, 메소드, public 속성, 메소드 구현 가능

- **외부 함수 호출이 종료되더라도 외부 함수의 지역 변수 및 변수 스코프 객체의 체인 관계를 유지할 수 있는 구조, 외부 함수에 의해 반환되는 내부 함수를 가리키는 것**

### 클로저 생성

<클로저 생성 조건>

1. 내부 함수가 익명 함수로 되어 외부 함수의 **반환값**으로 사용
2. 내부 함수는 외부 함수의 실행 환경(execution environment)에서 실행
3. 내부 함수에서 사용되는 **변수 x는 외부 함수의 변수 스코프**에 있음

```jsx
function outer() {
  var name = `closure`;
  function inner() {
    console.log(name);
  }
  inner();
}
outer();
```

`outer` 함수를 실행시키는 `context` 에는 `name` 이라는 변수가 존재하지 않는 것 확인

```jsx
var name = `Warning`;
function outer() {
  var name = `closure`;
  return function inner() {
    console.log(name);
  };
}

var callFunc = outer();
callFunc();
```

`callFunc` 는 Closure

`callFunc` 호출에 의해 `name` 값이 콘솔에 찍히는데, 찍히는 값은 `warning` 이 아니라 `closure` 라는 값으로 즉, `outer` 함수의 `context` 에 속해있는 변수를 참조하는 것

`outer` 함수의 지역변수로 존재하는 `name` 변수는 `free variable(자유변수)`

## this

- JS에서 모든 함수는 실행될 때마다 함수 내부에 `this` 라는 객체가 추가됨
- `arguments` 라는 유사 배열 객체와 함께 함수 내부로 암묵적으로 전달되는 것

### 1. 객체의 메소드 호출

객체의 프로퍼티가 함수일 경우 === 메소드

`this` 는 함수를 실행할 때 함수를 소유하고 있는 객체(메소드를 포함하고 있는 인스턴스)를 참조, 즉 해당 메소드를 호출한 객체로 바인딩

`A.B` 일 때 `B` 함수 내부에서의 `this` 는 `A` 를 가리키는 것

```jsx
var myObject = {
  name: "foo",
  sayName: function() {
    console.log(this);
  }
};
myObject.sayName();

----------출력--------------
Object {name: "foo", sayName: sayName()}
```

### 2. 함수 호출

특정 객체의 메소드가 아닌 함수를 호출하면, 해당 함수 내부 코드에서 사용된 `this` 는 전역 객체에 바인딩됨, `A.B` 일 때 `A` 가 전역 객체가 되므로 `B` 함수 내부에서의 `this` 는 당연히 전역 객체에 바인딩 됨

```jsx
var value = 100;
var myObj = {
  value: 1,
  func1: function() {
    console.log(`func1's this.value: ${this.value}`);

    var func2 = function() {
      console.log(`func2's this.value ${this.value}`);
    };
    func2();
  }
};

myObj.func1();

----------출력--------------
func1's this.value: 1
func2's this.value: 100
```

`func1` 에서의 `this` 는 `1. 객체의 메소드 호출` 과 같음

⇒ `myObj` 가 `this` 로 바인딩되고 `myObj` 의 `value` 값 1이 출력됨

`func2` 는 함수 호출의 경우로, `A.B` 구조에서 `A` 가 없기 때문에 함수 내부에서 `this` 가 전역 객체를 참조하게 되고 `value` 값 100이 출력됨

### 3. 생성자 함수를 통해 객체 생성

`new` 키워드를 통해 생성자 함수를 호출할 때 호출된 함수 내부에서의 `this` 는 객체 자신을 가리킴, 생성자 함수가 동작하는 방식을 통해 이해할 수 있음

`new` 키워드를 통해 함수를 생성자로 호출하게 되면 빈 객체가 생성되고 `this` 가 바인딩 됨

이 객체는 함수를 통해 생성된 객체로, 자신의 부모인 프로토타입 객체와 연결되어있음

`return` 문이 명시되어있지 않은 경우 `this` 로 바인딩 된 새로 생성한 객체가 리턴됨

```jsx
var Person = function(name) {
  console.log(this);
  this.name = name;
};

var foo = new Person("foo"); // Person
console.log(foo.name);

----------출력--------------
foo
```

## Promise

- JS에서는 대부분의 작업들이 비동기로 이루어짐
- 콜백함수로 처리하면 됐었지만, 프론트엔드의 규모가 커지면서 코드의 복잡도가 높아지는 상황이 발생 ⇒ 콜백이 중첩되는 경우(콜백 지옥)
- 이를 해결할 방안으로 등장한 `Promise`
- **비동기 작업들을 순차적으로 진행, 병렬로 진행하는 등의 컨트롤이 수월**해짐
- **예외처리에 대한 구조가 존재**하기 때문에 **오류 처리 등에 대하여 보다 가시적 관리 가능**
- ES6 정식 포함됨
- `promise` 객체를 반환
- `.then` , `.catch` 로 예외처리

```jsx
// Promise 선언
var _promise = function(param){
	return new Promise(function (resolve, reject){
		window.setTimeout(function (){
			if(param){
				resolve('success');
			}else{
				reject(Error('failed'));
			}
		},3000);
	});
};

// Promise 실행
_promise(true)
	.then(function (text){
			console.log(text);
	}, function (error){
			console.error(error);
});

----------출력--------------
success
```

`promise` 상태

- `pending`(대기) 상태: promise를 수행 중인 상태(fulfilled or reject가 되기 전)
- `fulfilled`(이행) 상태: promise를 성공적으로 완료한 상태
- `rejected`(거부) 상태: 실패한 상태

## async/await

- 비동기 코드를 작성하는 새로운 방법
- `promise` 기반으로 `promise` 로 만족하지 못하고 더 훌륭한 방법을 고안해낸 것
- 사용법이 간단하고 이해하기 쉬움
- 함수 키워드 앞에 `async` 를 붙여주면 되고 함수 내부의 `promise` 를 반환하는 비동기 처리 함수 앞에 `await` 를 붙여주면 됨 (`promise` 객체를 반환하지만 `await` 가 반환 객체를 까주어 `try/catch` 를 사용할 수 있게함
- `promise` 보다 겉보기에 깔끔함
- ES8
- `try` , `catch` 로 예외 처리

`promise` 로 구현

```jsx
function makeRequest() {
  return getData()
    .then((data) => {
      if (data && data.needMoreRequest) {
        return makeMoreRequest(data)
          .then((moreData) => {
            console.log(moreData);
            return moreData;
          })
          .catch((error) => {
            console.log('Error while makeMoreRequest', error);
          });
      } else {
        console.log(data);
        return data;
      }
    })
    .catch((error) => {
      console.log('Error while getData', error);
    });
}
```

`async/await` 로 구현

```jsx
async function makeRequest() {
  try {
    const data = await getData();
    if (data && data.needMoreRequest) {
      const moreData = await makeMoreRequest(data);
      console.log(moreData);
      return moreData;
    } else {
      console.log(data);
      return data;
    }
  } catch (error) {
    console.log('Error while getData', error);
  }
}
```

## Arrow Function

- 기존 `function` 표현 방식보다 간결하게 함수 표현 가능
- 항상 익명
- 자신의 `this` , `arguments` , `super` , `[new.target](http://new.target)` 을 바인딩하지 않음 ⇒ 생성자로 사용 X
- 화살표 함수 도입 영향: 짧은 함수, 상위 스코프 `this`

### 짧은 함수

기존의 function 생략 ⇒로 대체 표현

```jsx
var materials = ['Hydrogen', 'Helium', 'Lithium', 'Beryllium'];

materials.map(function (material) {
  return material.length;
}); // [8, 6, 7, 9]

materials.map((material) => {
  return material.length;
}); // [8, 6, 7, 9]

materials.map(({ length }) => length); // [8, 6, 7, 9]
```

### 상위 스코프 `this`

일반 함수에서 `this` 는 자기 자신을 정의

화살표 함수의 `this` 는 Person의 `this` 와 동일한 값

`setInterval` 로 전달된 `this` 는 Person의 `this` 를 가리키며 Person객체의 age에 접근

```jsx
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++; // |this|는 person 객체를 참조
  }, 1000);
}

var p = new Person();
```

## undefined과 null의 차이

### undefined과 null의 공통점

- 타입명의 값이 유일
- undefined 타입의 값은 undefined가 유일
- null 타입의 값은 null이 유일

### undefined

- 원시자료형 undefined로 분류됨
- 아무것도 할당받지 않은 상태를 의미
- var 키워드로 선언한 변수는 암묵적으로 undefined로 초기화 됨
- 변수 선언에 의해 확보된 메모리 공간을 처음 할당이 이루어질 때까지 빈 상태로 내버려두지 않고 js엔진이 undefined로 초기화함
- 따라서 변수를 선언한 이후 값을 할당하지 않은 변수를 참조하면 undefined가 반환됨
- 변수를 참조했을 때 undefined가 반환된다면 선언 이후 값이 할당되지 않은 , 초기화되지 않은 변수인 것
- 개발자가 의도적으로 할당하기 위한 값이 아니라 js엔진이 변수를 초기화할 때 사용하는 값
  ```jsx
  var a;
  console.log(a);
  console.log(typeof a);
  ```

### null

- 원시자료형 null로 분류됨
- js는 대소문자를 구분하기 때문에 Null, NULL 과 다름
- 프로그래밍 언어에서 null은 변수에 값이 없다는 것을 의도적으로 명시할 때 사용
- 변수에 null을 할당하는 것은 변수가 이전에 참조하던 값을 더 이상 참조하지 않겠다는 의미
- 이는 이전에 할당되어 있던 값에 대한 참조를 명시적으로 제거하는 것 의미
- js엔진은 누구도 참조하지 않은 메모리 공간에 대해 가비지 콜렉션 수행

## Object.assign()

- 출처 객체들의 모든 열거 가능한 자체 속성을 복사하여 대상 객체에 붙여넣고 객체 반환됨

```jsx
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }
```
