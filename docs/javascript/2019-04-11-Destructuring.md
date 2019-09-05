2019년 4월 11일

# Destructuring

---

> Destructuring은 배열 또는 객체에서 필요한 값만 추출하여 변수에 할당하는 것을 말한다.

## 1. Array destructuring

- 배열 디스트럭처링의 추출 / 할당 기준은 **배열의 인덱스**이다.

### ES5

```javascript
// ES5 Destructuring
var arr = [1, 2, 3];

var one   = arr[0];
var two   = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3
```

### ES6

```javascript
// ES6 Destructuring
const arr = [1, 2, 3];

// 배열의 인덱스를 기준으로 배열로부터 요소를 추출하여 변수에 할당
const [one, two, three] = arr;

console.log(one, two, three); // 1 2 3
```

```javascript
let a, b, c;
[a, b, c] = [1, 2, 3];

// 위의 구문과 동일하다
let [a, b, c] = [1, 2, 3];
```

```javascript
let a, b, c;

[a, b] = [1, 2];
console.log(a, b); // 1 2

[a, b] = [1];
console.log(a, b); // 1 undefined

[a, b] = [1, 2, 3];
console.log(a, b); // 1 2

[a, , c] = [1, 2, 3];
console.log(a, c); // 1 3

// 기본값
[a, b, c = 3] = [1, 2];
console.log(a, b, c); // 1 2 3

[a, b = 10, c = 3] = [1, 2];
console.log(a, b, c); // 1 2 3

// spread 연산자
[a, ...c] = [1, 2, 3];
console.log(a, b); // 1 [ 2, 3 ]
```

- ES6의 배열 디스트럭처링은 배열에서 필요한 요소만 추출하여 변수에 할당하고 싶은 경우에 유용하다. 
- 아래의 코드는 Date 객체에서 년도, 월, 일을 추출하는 예제이다.

```javascript
const today = new Date();
console.log(today); // 2019-05-01T15:38:25.837Z
const formattedDate = today.toISOString().substring(0, 10);
console.log(formattedDate); // 2019-05-01
const [year, month, day] = formattedDate.split('-');
console.log([year, month, day]); // [ '2019', '05', '01' ]
```



## 2. Object destructuring

- 객체 디스트럭처링의 추출 / 할당 기준은 **객체의 키(key)값**이다.

```javascript
// ES5 Destructuring
var obj = { firstName: 'Sony', lastName: 'Park' };

var firstName = obj.firstName;
var lastName  = obj.lastName;

console.log(firstName, lastName); // Sony Park
```

```java
// ES6 Destructuring
const obj = { firstName: 'Sony', lastName: 'Park' };

const { firstName, lastName } = obj;

console.log(firstName, lastName); // Sony Park
```



```javascript
const { key1, key2 } = { key1 : 'a', key2 : 'b' };
console.log({ key1, key2 }); // { key1 : 'a', key2 : 'b' }

//defalut value
const { key1, key2, key3 = 'c' } = { key1 : 'a', key2 : 'b' };
console.log({ key1, key2, key3 }); // { key1 : 'a', key2 : 'b', key3 : 'c' }
```

- Array.prototype.filter 메소드의 콜백 함수는 대상 배열(todos)을 순회하며 첫 번째 인자로 대상 배열의 요소를 받는다. 이때 필요한 프로퍼티(key)(completed 프로퍼티)만을 추출할 수 있다.
```javascript
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: false },
  { id: 3, content: 'JS', completed: false }
];

// todos 배열의 요소인 객체로부터 completed 프로퍼티만을 추출한다.
const completedTodos = todos.filter(({ completed }) => completed);
console.log(completedTodos); // [ { id: 1, content: 'HTML', completed: true } ]
```

- 중첩 객체의 경우 다음과 같이 사용한다.

```javascript
const person = {
  name: 'Sony',
  address: {
    zipCode: '06219',
    city: 'Seoul'
  }
};

const { address: { city } } = person;
console.log(city); // 'Seoul'
```

---

## Reference

- [Destructuring | PoiemaWeb](https://poiemaweb.com/es6-destructuring)
- [ECMAScript 6](http://www.ecma-international.org/ecma-262/6.0/ECMA-262.pdf)