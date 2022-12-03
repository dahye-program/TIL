# Javascript

## 구조분해할당

### 배열 구조 분해

- 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있도록 함

```jsx
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// expected output: 10

console.log(b);
// expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// expected output: Array [30,40,50]

var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2
```

**기본 변수 할당**

```jsx
let foo = ['one', 'two', 'three'];

let [red, yellow, green] = foo;
console.log(red); // "one"
console.log(yellow); // "two"
console.log(green); // "three"
```

**선언에서 분리한 할당**

```jsx
let a, b;

[a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2
```

**하나의 구조 분해 표현식만으로 두 변수의 값 교환 가능**

```jsx
let a = 1;
let b = 3;

[a, b] = [b, a];
console.log(a); // 3
console.log(b); // 1
```

**함수가 반환한 배열**

```jsx
function f() {
  return [1, 2];
}

let a, b;
[a, b] = f();
console.log(a); // 1
console.log(b); // 2
```

**일부 반환 값 무시**

```jsx
function f() {
  return [1, 2, 3];
}

var [a, , b] = f();
console.log(a); // 1
console.log(b); // 3
```

변수에 배열의 나머지 할당

- 배열을 구조 분해하는 경우, 나머지 구문 이용하여 분해하고 남은 부분을 하나의 변수에 할당 가능

```jsx
let [a, ...b] = [1, 2, 3];
console.log(a); // 1
console.log(b); // [2, 3]
```

### 객체 구조 분해

```jsx
let o = { p: 42, q: true };
let { p, q } = o;

console.log(p); // 42
console.log(q); // true
```

**선언없이 할당**

```jsx
let a, b;
({ a, b } = { a: 1, b: 2 });
```

**새로운 변수 이름으로 할당**

```jsx
let o = { p: 42, q: true };
let { p: foo, q: bar } = o;

console.log(foo); // 42
console.log(bar); // true
```

**객체로부터 해체된 값이 `undefined` 인 경우 변수에 기본값 할당 가능**

```jsx
let { a = 10, b = 5 } = { a: 3 };

console.log(a); // 3
console.log(b); // 5
```

기본값 가지는 새로운 이름의 변수에 할당

- 새로운 변수명 할당과 기본값 할당 한번에 가능

```jsx
let { a: aa = 10, b: bb = 5 } = { a: 3 };

console.log(aa); // 3
console.log(bb); // 5
```

## javascript array copy

- slice(), concat(), spread 연산자, Array.from()

### 얕은 복사(shallow copy)

- 참조 주소 공유
- 얕은 복사는 alias로 인해 같은 주소를 공유하기 때문에 복사한 객체를 변경하면 기존 객체도 변경되는 문제가 발생할 수 있음
- 기존 배열 arr1을 얕은 복사한 arr2의 값을 변경 시, arr1의 값도 같이 변경됨

  ```jsx
  let arr1 = [{ name: 'a' }, { name: 'b' }];
  let arr2 = arr1;

  arr2[0].name = 'c';
  console.log(arr1, arr2);
  // {name: "c"}, {name: "b"}, {name: "c"}, {name: "b"}
  ```

### 깊은 복사(deep copy)

- `JSON.parse(JSON.stringify())`
- 참조 주소 공유 X, 참조 공간도 복사됨

```jsx
let deepArr = JSON.parse(JSON.stringify(arr1));
```

- JSON.stringify()로 string으로 타입캐스팅 후 다시 JSON.parse로 object로 바꿈 ⇒ 완전히 다른 객체로 생성되며 깊은 복사 가능

## 배열 합치기 push, concat, …(spread operator)

- push()
  - 배열 끝에 요소 추가, 배열의 새로운 길이 반환
- concat()

  - 기존 배열에 합쳐서 새로운 배열 리턴

  ```jsx
  const arr = [1, 2, 3];
  const newArr = arr.concat('a', ['b', 'c'], 'abc');

  console.log(newArr);
  // 1, 2, 3, a, b, c, abc
  // 파라미터가 배열인 경우 배열 안의 원소들을 꺼내 새로운 배열에 포함
  ```

- … (spread operator, 전개연산자)

  - 배열에서 전개연산자는 배열의 원소들을 분해해서 개별요소로 만들어줌

  ```jsx
  const arr1 = [1, 2, 3];
  const arr2 = [4, 5, 6];
  const arr3 = [7, 8, 9];

  const newArr = [...arr1, ...arr2, ...arr3];

  console.log(newArr);
  // 1, 2, 3, 4, 5, 6, 7, 8, 9
  ```

## Map

- key가 있는 데이터 저장
- object와 유사하지만, object와 달리 key에 다양한 자료형을 허용한다는 차이점 존재
  - object는 키를 문자형으로 변환하지만 Map은 타입 변환 없이 그대로 유지

### Map - Method

```jsx
// (1) key의 다양한 자료형
let map = new Map();

map.set('1', 'str'); // string
map.set(1, 'num'); // number

console.log(map.get(1)); // 'num'
console.log(map.get('1')); // 'str'

// (2) key로 object 사용
let dahye = { name: 'dahye' };
let map = new Map();
map.set(dahye, 123);

console.log(map.get(dahye)); // 123
```

- `new Map()` : 맵 생성
- `map.set(key,value)` : `key` 를 이용하여 `value` 저장
- `map.get(key)` : `key` 에 해당하는 값 반환, `key` 가 존재하지 않으면 `undefined` 반환
- `map.has(key)` : `key` 가 존재하면 `true` , `key` 가 존재하지 않으면 `false` 반환
- `map.delete(key)` : `key` 에 해당하는 값 삭제
- `map.clear()` : 맵 안의 모든 요소 제거
- `map.size` : 맵 요소의 개수 반환

### Map - Iteration

```jsx
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion', 50],
]);

// 키(vegetable)를 대상으로 순회
for (let vegetable of recipeMap.keys()) {
  console.log(vegetable); // cucumber, tomatoes, onion
}

// 값(amount)을 대상으로 순회
for (let amount of recipeMap.values()) {
  console.log(amount); // 500, 350, 50
}

// [키, 값] 쌍을 대상으로 순회
for (let entry of recipeMap) {
  // recipeMap.entries()와 동일
  console.log(entry); // cucumber,500 ...
}
```

- `map.keys()` : 각 요소의 `key` 를 모은 반복 가능한(`iterable object`)객체를 반환
- `map.values()` : 각요소의 `value` 를 모은 `iterable object` 객체를 반환
- `map.entries()` : 요소의 `[key, value]` 를 한 쌍으로 하는 `iterable object` 객체를 반환 ⇒ 이 객체는 `for..of` 반복문의 기초로 쓰임

### Map - Conversion

```jsx
// (1) Convert object to map
let obj = {
  name: 'dahye',
  age: 24,
};

let map = new Map(Object.entries(obj));
console.log(map.get('name')); // dahye

// (2) Convert map to object
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map);
// obj = { banana: 1, orange: 2, meat: 4 }

console.log(prices.orange); // 2
```

- `object.entries` : `object` 를 `map` 으로 변환
- `object.fromEntries` : `map` 을 `object` 로 변환

## 연산자
### 논리연산자 ! (NOT)
- 인수를 하나 받아서 아래 연산 수행
  - 피연산자를 `불린형(true/false)`로 변환
  - 1에서 변환된 값의 역을 반환
  ```
  console.log(!true) // false 
  console.log(!0) // true
  ```
- `NOT` 을 두 개 연달아 사용하면 값을 불린형으로 변환 가능
  ```
  let str = 'hello';
  console.log(!!str); // true
  console.log(!!null); // false
  ```
- 첫 번째 `NOT` 연산자는 피연산자로 받은 값을 불린형으로 변환한 후 이 값의 역을 반환 
- 두 번째 `NOT` 연산자는 첫 번째 NOT 연산자가 반환한 값의 역을 반환
- 이렇게 `NOT` 연산자를 연달아 사용하면 특정 값을 불린형으로 변환 가능
+ 내장함수 `Boolean` 형을 사용하면 `!!` 을 사용한 것과 같은 결과 도출
+ `NOT` 연산자의 우선순위는 모든 논리연산자 중에서 가장 높기 때문에 항상 `&&`, `||` 보다 먼저 실행됨