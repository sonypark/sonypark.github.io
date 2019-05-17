2019년 4월 8일

# The arguments object
> 주의) ES6에서는 함수 내에 `arguments` 객체가 없다. 따라서 `rest parameters`를 써야 한다.

> The arguments object is a local variable available within all `non-arrow` functions.

- **arguments** 는 함수에 **입력된 인자값**을 **배열 형태로 저장**하는 객체이다.

- **하지만 배열은 아니다**. 배열의 속성 중 하나인 `length`와 `index` 속성은 갖고 있지만 배열의 메서드인 `forEach()`, `map()` 등은 사용 할 수 없다.
 
  
 ```javascript
function func1(a, b, c) {
  console.log(arguments[0]);
  // expected output: 1

  console.log(arguments[1]);
  // expected output: 2

  console.log(arguments[2]);
  // expected output: 3
  
  console.log(arguments.length)
  // expected output: 3
}

func1(1, 2, 3);
```

```javascript
arguments[0] // first argument
arguments[1] // second argument
arguments[2] // third argument
```

- argument 에 새로운 값을 **입력(set)** 하거나 **재할당(reassigned)** 도 **가능**하다. 

```javascript
arguments[1] = 'new value';
```

- `arguments`는 `Array`가 아니다.
- 하지만 다음과 같은 방법으로 `Array`로 변환할 수 있다.

```javascript
var args = Array.prototype.slice.call(arguments);
// Using an array literal is shorter than above but allocates an empty array
var args = [].slice.call(arguments);
```

- ES6문법 `Array.from()` 또는 `spread syntax` 를 사용해 `Array`로 변환 할 수 있다.

```javascript
var args = Array.from(arguments);
var args = [...arguments];
```

- `arguments` 객체는 `Math.min()`과 같이 인자값으로 몇개가 들어올지 모르는 함수에 사용할 때 유용하다.
- 다음 함수는 입력받은 문자열 중 가장 길이가 긴 문자열을 리턴한다.

```javascript
function longestString() {
  var longest = '';
  for (var i=0; i < arguments.length; i++) {
    if (arguments[i].length > longest.length) {
      longest = arguments[i];
    }
  }
  return longest;
}
```

### arguments.length 와 function.length 의 차이점!

- **arguments.length**: 함수에 실제로 입력받은 인자 갯수(number of arguments)를 리턴한다.
- **function.length**: 함수에 필요한 파라미터 갯수(number of formal parameters)를 리턴한다.

```javascript
function func1() {}
function func2(a, b) {}

console.log(func1.length);
// expected output: 0

console.log(func2.length);
// expected output: 2
```

- 이처럼 함수를 실행하기 위해 필요한 파라미터 갯수를 리턴한다.
- `rest parameter`는 무시한다.

```javascript
console.log(Function.length); /* 1 */

console.log((function()        {}).length); /* 0 */
console.log((function(a)       {}).length); /* 1 */
console.log((function(a, b)    {}).length); /* 2 */

console.log((function(...args) {}).length); 
// 0, rest parameter is not counted

console.log((function(a, b = 1, c) {}).length);
// 1, only parameters before the first one with 
// a default value is counted
// 디폴트 값이 정의된 파라미터 전까지의 갯수를 리턴한다.
```


### Reference

- [MDN, The arguments object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments#Description)
- [MDN, Function.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/length)