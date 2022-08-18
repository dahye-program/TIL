# Javascript

## 배열 구조 분해

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
