2019년 4월 8일

# Rest Parameters
> rest parameter를 이용하면 무한개의 인자를 배열로 받을 수 있다.

- ex) 1부터 n까지의 합을 구하는 함수

```javascript
function sum(...theArgs) {
  return theArgs.reduce((previous, current) => {
    return previous + current;
  });
}

console.log(sum(1, 2, 3));
// expected output: 6

console.log(sum(1, 2, 3, 4));
// expected output: 10
```

- `rest parameter`는 함수의 마지막 파라미터에 `...`을 붙여 표현한다.
- 함수의 마지막 파라미터만 `rest parameter`가 될 수 있다.
  
```javascript
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a); 
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs); 
}

myFun("one", "two", "three", "four", "five", "six");

// Console Output:
// a, one
// b, two
// manyMoreArgs, [three, four, five, six]
```
___
## arguments object 와 차이점!

- **입력받는 인자**: `arguments object`는 입력한 모든 인자값을 받지만 `rest parameter`는 정해진 파라미터 이외의 인자값만 받는다. 
- **Array**: `rest parameter`는 Array이지만 `arguments object`는 Array가 아니다(Array의 속성인 `length`와 `index`만 갖고 있는 유사 배열이다.)

```javascript
// arguments object를 Array로 변환하는 방법 세 가지
function f(a, b) {

  var normalArray = Array.prototype.slice.call(arguments);
  // -- or --
  var normalArray = [].slice.call(arguments);
  // -- or --
  var normalArray = Array.from(arguments);

  var first = normalArray.shift(); // normalArray[0]값 삭제 후 리턴, (Array로 변환했기 때문에 배열 함수인 shift()함수를 쓸 수 있다.) 
  var first = arguments.shift(); // ERROR (arguments는 배열이 아니기 때문에 shift()함수를 쓸 수 없다.)

}

// rest paramters를 이용하면 쉽게 인자값을 배열로 받을 수 있다.
function f(...args) {
  var normalArray = args;
  var first = normalArray.shift(); // normalArray[0]값 삭제 후 리턴
}
```
___

## Destructuring rest parameters

```javascript
function f(...[a, b, c]) {
  return a + b + c;
}

f(1)          // NaN (b and c are undefined)
f(1, 2, 3)    // 6
f(1, 2, 3, 4) // 6 (the fourth parameter is not destructured)
```
___
## Example

```javascript
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a); 
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs); 
}

myFun("one", "two", "three", "four", "five", "six");

// a, one
// b, two
// manyMoreArgs, [three, four, five, six]
```
- 첫번째 인자값은 a로 두번째 인자값은 b로 나머지는 `rest parameters`로 들어간다.


```javascript
// 위와 같은 함수
myFun("one", "two", "three");

// a, one
// b, two
// manyMoreArgs, [three]
```
- `rest parameter`가 하나뿐이라도 배열에 담긴다.

```javascript
// 위와 같은 함수
myFun("one", "two");

// a, one
// b, two
// manyMoreArgs, []
```
- `rest parameter`가 없으면 `rest parameter`는 빈 배열이 된다.

```javascript
function fun1(...theArgs) {
  console.log(theArgs.length);
}

fun1();  // 0
fun1(5); // 1
fun1(5, 6, 7); // 3
```
- `length`를 이용해 입력받은 인자의 갯수를 알 수 있다.


```javascript
function multiply(multiplier, ...theArgs) {
  return theArgs.map(function(element) {
    return multiplier * element;
  });
}

var arr = multiply(2, 1, 2, 3); 
console.log(arr); // [2, 4, 6]
```
- 첫번째 인자값을 배수로 하여 `rest parameters`의 각 요소에 곱한 배열을 리턴하는 함수


```javascript
function sortRestArgs(...theArgs) {
  var sortedArgs = theArgs.sort();
  return sortedArgs;
}

console.log(sortRestArgs(5, 3, 7, 1)); // 1, 3, 5, 7

function sortArguments() {
  var sortedArgs = arguments.sort(); 
  return sortedArgs; // this will never happen
}

console.log(sortArguments(5, 3, 7, 1)); // TypeError (arguments.sort is not a function)
```
- `arguments object`는 배열이 아니기 때문 Array methods를 쓸 수 없지만 `rest paramters`는 Array methods를 쓸 수 있다. 

```javascript
function sortArguments() {
  var args = Array.from(arguments);
  var sortedArgs = args.sort();
  return sortedArgs;
}
console.log(sortArguments(5, 3, 7, 1)); // 1, 3, 5, 7
```
- `arguments`에서 Array methods를 쓰려면 배열로 변환해야한다.
___
### Reference

- [MDN, Rest Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
