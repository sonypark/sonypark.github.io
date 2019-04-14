---
layout: post
title: Call by Value VS Call by Reference
category: Javascript

tags: [Javascript, callByValue, callByReference]
comments: true
---

# Call by value  VS Call by reference in javascript

## **Call by Value**
> 변수의 값(value)을 복사한다.

- Javascript에서 call by value로 전달되는 데이터 타입
    - **primitive types**
    - `String`, `Number`, `Boolean`, `undefined`, `null`

- 변수(variable)에 primitive type 데이터가 할당 되면 값(value) 자체가 할당된다.

- 메모리(Memory)에는 다음과 같이 저장된다.

```javascript
var a = 10;
var b = 'hello';
var c = null;
var d = undefined;
```

Variables | Values 
:--------: | :---------:
a    | 10
b    | 'hello'
c    | null
d    | undefined

- primitive type 데이터가 할당된 변수를 다른 변수에 할당 할 때, `값(value)을 복사(copy)`한다.

```javascript
var x = 10;
var y = 'hello';
var a = x;
var b = y;
console.log(x, y, a, b); // -> 10, 'hello', 10, 'hello'
```  

- 메모리에는 다음과 같이 저장된다.

Variables | Values 
:--------: | :---------:
x    | 10
y    | 'hello'
a    | 10
b    | 'hello'

- 값 자체가 복사되어 변수에 할당된다.
- 각각의 변수는 독립적으로 저장된다.

- 각 변수는 독립적이므로 어느 하나의 값이 바뀌어도 서로에게 영향을 주지 않는다.

```javascript
var x = 10;
var y = 'hello';
var a = x;
var b = y;
a = 5;
b = 'def';
console.log(x, y, a, b); // -> 10, 'hello', 5, 'def'
```
    

## **Call by Reference**
> 변수의 주소값(address)을 복사한다.

- Javascript에서 call by reference로 전달되는 데이터 타입
    - `Array`, `Function`, `Object`
    - 이 세가지 모두 객체(Object)이다.
    - 따라서 객체(Object)는 call by reference로 전달된다는 걸 기억하자.

- 변수(variable)에 `non-primitive value`, 즉 `Object`를 할당하면 해당 Object의 `주소값(address)`을 복사한다.
- 변수에 값이 아닌 `주소값`을 복사한다
- `arr = []` 라고 선언하면 `메모리`에 array `객체(object)를 저장`하고 `변수`에는 그 `객체의 주소값(address)`이 저장된다.
- 주소값(address)은 `<>` 형태로 저장된다. (string이 `''` or `"'` 형태로 저장되는 것처럼)

- 다음을 실행했을 때 메모리에 저장되는 과정을 살펴보자.

```javascript
var arr = []; // (1)
arr.push(1); // (2)
```

-  (1) 실행

Variable | Values | Address | Objects 
:--------: | :---------: | :--------: | :---------:
arr    | <#001>   | #001  | []

- (2) 실행

Variable | Values | Address | Objects 
:--------: | :---------: | :--------: | :---------:
arr    | <#001>   | #001  | [1]

### Assigning by Reference

- 객체(Object: `non-primitive value` or `reference type value`)를 다른 변수에 할당할 때, 해당 객체의 `주소값(address)`을 할당한다.

```javascript
var arr = [1];
var arr2 = arr;
```  

Variables | Values | Address | Objects 
:--------: | :---------: | :--------: | :---------:
arr    | <#001>   | #001  | [1]
arr2    | <#001>

- 두 변수(`arr`,`arr2`)는 같은 주소값을 갖는다.
- 즉, 같은 배열을 참조하고 있다.
- 따라서 배열의 값이 바뀌면 두 변수에 모두 적용된다.

```javascript
arr.push(2);
console.log(arr, arr2); // -> [1, 2], [1, 2]
```
 
Variables | Values | Address | Objects 
:--------: | :---------: | :--------: | :---------:
arr    | <#001>   | #001  | [1,2]
arr2    | <#001>

- 같은 배열의 주소값을 참조하고 있기 때문에 배열의 변경 사항은 두 변수 모두에 적용된다.

### Reassigning a Reference

- 참조 변수(reference variable)에 새로운 객체(object)를 재할당하면 이전의 객체를 대체한다.

- 아래와 같이 객체를 참조 변수에 할당 하면

```javascript
var obj = { first: 'reference' };
```

- 메모리 상에는 다음과 같이 저장된다.
 
Variables | Values | Address | Objects 
:--------: | :---------: | :--------: | :---------:
obj    | <#234>   | #234  | { first: 'reference' }

- 여기서 참조 변수에 새로운 객체(object)를 재할당하면

```javascript
var obj = { first: 'reference' };
obj = { second: 'ref2' }
```

- `obj`에 저장된 `주소값`이 변경된다.
- 기존 객체(first object)도 메모리에 남아있다.

Variables | Values | Address | Objects 
:--------: | :---------: | :--------: | :---------:
obj    | <#678>   | #234  | { first: 'reference' }
       |          |       | #678  | { second: 'ref2' }

- `#234` 주소값을 갖는 객체(first object)를 참조하는 변수가 없다.
- 이러한 객체는 메모리 상에 존재하다가 `Javascript engine`의 `가비지 컬렉터(garbage collector)`에 의해 메모리에서 삭제된다.


#### `===` : 참조값 비교

- 변수가 같은 객체(object)를 참조하는 경우 `===` 연산은 `True`이다. 

```javascript
var arrRef = ['Hi!'];
var arrRef2 = arrRef;
console.log(arrRef === arrRef2); // -> true
```

- 서로 다른 객체를 참조하는 경우 `===` 연산은 `False`이다.

```javascript
var arr1 = ['Hi!'];
var arr2 = ['Hi!'];
console.log(arr1 === arr2); // -> false
``` 

- 만약 서로 다른 객체의 속성값을 비교하고 싶다면 두 객체를 `string`으로 변환한 뒤 비교할 수 있다.
- 이 때 동등 연산자(`===`)는 primitives type 데이터를 비교하는 것처럼 단순히 `값(value)`이 같은지 비교한다.

```javascript
var arr1str = JSON.stringify(arr1);
var arr2str = JSON.stringify(arr2);
console.log(arr1str === arr2str); // true
```

- `JSON.stringify`을 이용하여 객체(object)를 문자열(string)로 바꾼 뒤 비교한다.

## Passing Parameters through Functions

### Pure vs. Impure Function.

#### impure function

```javascript
function changeAgeImpure(person) {
    person.age = 25;
    return person;
}
var alex = {
    name: 'Alex',
    age: 30
};
var changedAlex = changeAgeImpure(alex);
console.log(alex); // -> { name: 'Alex', age: 25 }
console.log(changedAlex); // -> { name: 'Alex', age: 25 }
```
- `changeAgeImpure()` **함수의 인자값으로 객체(object)가 들어간다.**
- 즉, alex 변수가 가리키는 객체의 주소값(address)이 들어간다.
- 따라서 `person.age` 는 `alex.age` 와 같다.
- 그러므로 `person.age`를 변경하면 `alex.age`의 값도 변경된다.
- `changeAgeImpure()` 함수는 `person`이라는 객체를 리턴한다.
- 이 객체는 `changedAlex`라는 변수에 할당 된다.
- 즉, `alex`와 `changedAlex`는 같은 객체의 주소값을 참조한다.


#### pure function

```javascript
function changeAgePure(person) {
    var newPersonObj = JSON.parse(JSON.stringify(person));
    newPersonObj.age = 25;
    return newPersonObj;
}
var alex = {
    name: 'Alex',
    age: 30
};
var alexChanged = changeAgePure(alex);
console.log(alex); // -> { name: 'Alex', age: 30 }
console.log(alexChanged); // -> { name: 'Alex', age: 25 }
```

- `changeAgePure()`함수에서 `JSON.stringify`를 사용하여 **객체(object)를 `string`으로 변환**했다.
- 그리고 또 다시 `JSON.parse`를 통해 객체(object)롤 변환하여 새로운 변수(`var newPersonObj`)에 할당했다.
- 이러한 변환 과정을 통해 새로운 변수에 할당되면 새로운 객체(new object)가 생성된다.
- 즉, `newPersonObj`가 참조하는 객체의 주소값과 `alex`가 참조하는 객체의 주소값은 다르다.
- `changeAgePure()`함수가 리턴한 `newPersonObj`는 `var alexChanged`에 할당된다.
- 따라서 `alex`와 `alexChanged`는 서로 다른 객체를 참조한다.
- 두 참조 변수의 속성을 변경해도 서로 영향을 주지 않는다. 


### 추가 예시

#### Call by Value

```javascript
function callByValue(varOne, varTwo) { 
  console.log("Inside Call by Value Method"); 
  varOne = 100; 
  varTwo = 200; 
  console.log("varOne =" + varOne +"varTwo =" +varTwo); 
} 
let varOne = 10; 
let varTwo = 20; 
console.log("Before Call by Value Method"); 
console.log("varOne =" + varOne +"varTwo =" +varTwo); 
callByValue(varOne, varTwo);
console.log("After Call by Value Method"); 
console.log("varOne =" + varOne +"varTwo =" +varTwo); 
/*
output will be : 
--------------- 
Before Call by Value Method 
varOne =10 varTwo =20 
Inside Call by Value Method 
varOne =100 varTwo =200 
After Call by Value Method 
varOne =10 varTwo =20
*/
``` 

#### Call by Reference

```javascript
function callByReference(varObj) { 
  console.log("Inside Call by Reference Method"); 
  varObj.a = 100; 
  console.log(varObj); 
} 
let varObj = {a:1};
console.log("Before Call by Reference Method"); 
console.log(varObj);
callByReference(varObj);
console.log("After Call by Reference Method"); 
console.log(varObj);

/*
output will be : 
--------------- 
Before Call by Reference Method 
{a: 1} 
Inside Call by Reference Method 
{a: 100} 
After Call by Reference Method 
{a: 100}
*/
```
 
 ```javascript
function changeAgeAndReference(person) {
    person.age = 25;
    person = {
        name: 'John',
        age: 50
    };
    
    return person;
}
var personObj1 = {
    name: 'Alex',
    age: 30
};
var personObj2 = changeAgeAndReference(personObj1);

console.log(personObj1); // -> { name: 'Alex', age: 25 }
console.log(personObj2); // -> { name: 'John', age: 50 }
```
 
 - 함수 파라미터(function parameters)를 통해 할당되는 것은 `=` 으로 할당하는 것과 본질적으로 동일하다.
 - 즉, 아래 코드와 동일하다.
 
 ```javascript
var personObj1 = {
    name: 'Alex',
    age: 30
};
var person = personObj1;
person.age = 25;
person = {
  name: 'john',
  age: 50
};
var personObj2 = person;
console.log(personObj1); // -> { name: 'Alex', age: 25 }
console.log(personObj2); // -> { name: 'John', age: '50' }
```
- 단, 한 가지 차이점이 있다.
- 함수를 이용하면 함수가 종료될 때 `person` 은 스코프(scope)에서 사라진다.
 
 
## Reference

- [[Javascript] Pass By Value And Pass By Reference In JavaScript](https://medium.com/nodesimplified/javascript-pass-by-value-and-pass-by-reference-in-javascript-fcf10305aa9c)
- [Explaining Value vs. Reference in Javascript – codeburst](https://codeburst.io/explaining-value-vs-reference-in-javascript-647a975e12a0)