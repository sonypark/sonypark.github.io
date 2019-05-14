2019년 4월 10일

# Scope in Javascript
> 스코프는 참조 대상 식별자(identifier)를 찾아내기 위한 규칙이다.
-  `identifier`: 변수, 함수의 이름과 같이 **어떤 대상을 식별할 수 있는 유일한 이름**
> 자바스크립트는 이 규칙대로 식별자를 찾는다.

- **전역 변수(Global Variable)**
    - 전역에서 선언된 변수: 어디에서든 참조할 수 있다.

- **지역 변수(Local Variable)**
    - 지역(함수) 내에서 선언된 변수: 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.

## Javascript Scope의 특징
> 자바스크립트의 스코프는 타 언어와는 다른 특징을 가지고 있다.

- 대부분의 C 계열 언어는 **블록 레벨 스코프(block-level scope)** 를 갖는다.
- `블록 레벨 스코프`: `코드 블록({…})`내에서 유효한 스코프
- 유효하다 = 참조할 수 있다.

- **하지만** 자바스크립트는 **함수 레벨 스코프(function-level scope)** 를 따른다. 
- `함수 레벨 스코프`: 함수 코드 블록 내에서 선언된 변수는 `함수 코드 블록` 내에서만 유효하고 함수 외부에서는 유효하지 않다.
- 단, ES6에 도입된 `let keyword`를 사용하면 `블록 레벨 스코프`를 사용할 수 있다.

## 스코프(scope)
> 스코프는 **변수의 수명**을 의미한다.

#### **전역변수**
- **함수 밖**에서 **변수를 선언**하면 그 변수는 **전역변수**가 된다.
- 전역변수는 어플리케이션 **전역에서 접근 가능**한 변수이다.

#### **지역변수**
- **함수 안**에서 **변수를 선언**하면 그 변수는 **지역변수**가 된다.
- 지역변수는 **선언된 함수 내에서 접근 가능**하다.

## 전역 변수와 지역 변수 비교

```javascript
var global = 'global';

function foo() {
  var local = 'local';
  console.log(global); // global
  console.log(local); // local
}
foo();

console.log(global); // global
console.log(local); // Uncaught ReferenceError: local is not defined
```

- 지역변수로 선언된 변수 `local`은 해당 스코프(함수) 밖에서 접근 할 수 없다.

```javascript
var vscope = 'global';
function fscope(){
    var vscope = 'local';
    console.log('함수 안 '+vscope); // local
}
fscope();
console.log('함수 밖 '+vscope); // global
```

- **같은 이름**의 지역변수와 전역변수가 **동시에 정의**되어 있다면 **지역변수**가 **우선**한다

##  var를 쓰는 것과 쓰지 않는 것의 차이

```javascript
var vscope = 'global';
function fscope(){
    vscope = 'local';
    console.log('함수 안'+vscope); // local
}
fscope();
console.log('함수 밖'+vscope); // local
```

- 함수 밖에서도 `vscope의 값`이 `local`로 출력 된다.
- 이유는 fscope 함수내에서 지역변수 `vscope`를 선언할 때 `var`를 사용하지 않았기 때문이다.
- **var를 사용하지 않은 지역변수는 전역변수가 된다.**
- 따라서 `전역 변수 vscope`의 값을 `local`로 변경하게 된 것이다.


```javascript
function a (){
    var i = 0;
}
for(var i = 0; i < 5; i++){
    a();
    console.log(i);  // 01234
}
```

- 위 예제의 결과값은 `01234`가 출력된다.
- 함수 a의 지역변수 i와 for 문의 변수 i (전역 변수)는 서로 다른 변수이기 때문이다.
- 그런데 다음과 같은 경우 문제가 발생한다.

```javascript
function a (){
    i = 0;
}
for(i = 0; i < 5; i++){
    a(); // i = 0 으로 초기화된다.
    console.log(i); // ...무한 반복 
}
```

- 위 예제는 결과값이 나오지 않고 **무한루프**를 돈다.
- 그 이유는 `함수 a 내의 변수 i`를 선언할 때 **var를 사용하지 않았기 때문**이다.
- 즉 `함수 a의 변수 i`는 **전역 변수**가 되고 `for 문의 변수 i`도 **전역 변수**이기 때문에 같은 값을 참조한다.
- 결국 for문 안에서 i = 0으로 계속 초기화 되기 때문에 무한루프에 빠지게 된다. 


- **전역 변수**의 사용은 가능한 **자제하자.**
    - **변수 이름**이 **중복**될 수 있다.
    - **의도치 않은 재할당에 의한 상태 변화**로 코드를 예측하기 어렵게 만든다.

- **변수를 선언**할 때는 꼭 **var** keyword를 붙이는 것을 **습관화**해야 한다.
> ES6에서는 let, const 로 선언 하는 것을 습관화하자.

- 전역변수를 사용해야 하는 경우라면 그것을 사용하는 이유를 명확히 알고 있을 때 사용하도록 하자.

- 불가피하게 전역변수를 사용해야 하는 경우는 하나의 객체를 전역변수로 만들고 객체의 속성으로 변수를 관리하는 방법을 사용한다.

```javascript
MYAPP = {}
MYAPP.calculator = {
    'left' : null,
    'right' : null
}
MYAPP.coordinate = {
    'left' : null,
    'right' : null
}
 
MYAPP.calculator.left = 10;
MYAPP.calculator.right = 20;
function sum(){
    return MYAPP.calculator.left + MYAPP.calculator.right;
}
console.log(sum());
```

- 전역변수를 사용하고 싶지 않다면 아래와 같이 익명함수를 호출함으로서 이러한 목적을 달성할 수 있다.

```javascript
(function(){
    var MYAPP = {}
    MYAPP.calculator = {
        'left' : null,
        'right' : null
    }
    MYAPP.coordinate = {
        'left' : null,
        'right' : null
    }
    MYAPP.calculator.left = 10;
    MYAPP.calculator.right = 20;
    function sum(){
        return MYAPP.calculator.left + MYAPP.calculator.right;
    }
    console.log(sum());
}())
```

- 위와 같은 방법은 자바스크립트에서 로직을 모듈화하는 일반적인 방법이다.

## 비 블록 레벨 스코프(Non block-level scope)
> Javascript는 함수 레벨 스코프 이다.

```javascript
if (true) {
  var x = 5;
}
console.log(x); // 5
```
- 변수 x는 함수가 아닌 코드 블록 내에서 선언되었다.
- `비 블록 레벨 스코프`: 함수 밖에서 선언된 변수는 코드 블록 내에서 선언되었다할지라도 모두 전역 스코프을 갖게된다. 
- 따라서 변수 x는 전역 변수이다.

```java
for(int i = 0; i < 10; i++){
    String name = "egoing";
}
System.out.println(name); // error: name을 참조할 수 없음
```

- Java는 블록 레벨 스코프를 따르기 때문에 위 예제는 에러가 난다.
- for 문 블록 내에서 선언된 변수 `name`은 for 문 밖에서는 참조할 수 없다.

```javascript
for(var i = 0; i < 1; i++){
    var name = 'coding everybody';
}
console.log(name); // coding everybody
```

- 자바스크립트의 경우 비 블록 레벨 스코프이기 때문에 위 예제에서 변수 `name`에 해당하는 값이 제대로 출력된다.
- for 문 블록 안에서 선언한 변수 `name`은 전역 변수로 선언되기 때문이다.

## 함수 레벨 스코프(Function-level scope)
> Javascript의 지역변수는 함수 안에서만 유효하다. 

```javascript
var a = 10;     // 전역변수

(function () {
  var b = 20;   // 지역변수
})();

console.log(a); // 10
console.log(b); // "b" is not defined
```
- 함수 내에 선언된 변수 b는 지역 변수가 된다.

```javascript
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x);
}

foo();          // local
console.log(x); // global
```
- 변수 x가 같은 이름을 중복 선언되었다.
- 전역 영역에서는 전역 변수만 참고 가능하다.
- 지역 영역에서는 지역 변수와 전역 변수 모두 참조 가능하다.
    - 이 경우 `지역 변수를 우선 참조`한다.

```javascript
var x = 'global';

function foo() {
  var x = 'local';
  console.log(x);

  function bar() {  // 내부함수
    console.log(x); // local
  }

  bar();
}
foo();
console.log(x); // global
```
- 내부함수는 자신을 포함하고 있는 외부함수의 변수에 접근할 수 있다.
- 함수 bar에서 참조하는 변수 x는 함수 foo에서 선언된 지역변수이다.
- 이는 실행 컨텍스트의 스코프 체인에 의해 참조 순위에서 전역변수 x가 뒤로 밀렸기 때문이다.
- `중첩 스코프`는 `가장 인접한 지역을 우선하여 참조`한다.

```javascript
var foo = function ( ) {

  var a = 3, b = 5;

  var bar = function ( ) {
    var b = 7, c = 11;

// 이 시점에서 a는 3, b는 7, c는 11

    a += b + c;

// 이 시점에서 a는 21, b는 7, c는 11

  };

// 이 시점에서 a는 3, b는 5, c는 not defined

  bar( );

// 이 시점에서 a는 21, b는 5

};
```

## 렉시컬 스코프(Lexical Scope)
> 렉시컬 스코프는 함수를 어디서 호출하는지가 아니라 어디에 **선언**하였는지에 따라 결정된다. 

- 프로그래밍 언어는 두 가지 방식 중 하나의 방식으로 함수의 상위 스코프를 결정한다.
    1. **동적 스코프(Dynamic scope)**: 함수를 어디서 **호출**하였는지에 따라 상위 스코프를 결정
    2. **렉시컬 스코프(Lexical scope)**: 함수를 어디서 **선언**하였는지에 따라 상위 스코프를 결정

- **자바스크립트**는 **렉시컬 스코프**를 따르므로 함수를 **선언**한 시점에 상위 스코프가 결정된다.
- 함수를 어디에서 호출하였는지는 스코프 결정에 아무런 의미를 주지 않는다.

```javascript
var x = 1;

function foo() {
  var x = 10;
  bar(); // bar가 호출된 시점
}

function bar() { // bar가 선언된 시
  console.log(x); 
}

bar(); // 1
```
- 위 예제의 함수 bar는 전역에 선언되었다. 
- 그러므로 함수 bar의 상위 스코프는 전역 스코프이다.
- 따라서 전역 변수 x의 값 1을 두번 출력한다.

```javascript
var i = 5;
  
 function a(){
     var i = 10;
     b(); // b가 호출 된 시점
 }
  
 function b(){ // b가 선언된 시점
     console.log(i);
 }
  
 a(); // 5
```

- `함수 b`가 **선언된 시점**을 **기준**에서 **유효범위(scope)** 를 갖는다.
- `함수 b`의 **상위 스코프**는 **전역**이므로 **전역변수 i(=5)** 를 **참조**한다.
- `함수 b`가 `함수 a` 안에서 호출되었다고 해서 `함수 a`의 `지역변수 i(=10)`가 호출되지 않는다.
- 함수의 **호출 시점**은 상위 스코프 결정에 **영향을 주지 않는다.** 

#### 자바스크립트는 함수가 선언된 시점에서의 유효범위를 갖는다.

- 이러한 유효범위 방식을 정적 유효범위(static scoping), 또는 렉시컬(lexical scoping)이라고 한다. 

## 암묵적 전역 변수(Implicit Global)
```javascript
function foo() {
  x = 10;
}

foo();
console.log(x); // 10
```
- 전역 스코프에 변수 x가 존재하지 않기 때문에 `ReferenceError`를 발생시킬 것 같지만 전역 변수x 를 `암묵적으로 생성`하고 `값을 할당`한다. 
- 이와 같이 `var 키워드를 생략한 변수`는 `암묵적으로 전역 변수`가 된다. 
- 암묵적 전역 변수는 오류의 발생 원인이 될 가능성이 크다.
- 따라서 변수를 선언할 때는 **반드시 변수 키워드(var, let, const)를 사용하자.**


## Reference

- [생활코딩: javascript 유효범위](https://opentutorials.org/course/743/6495)
- [poiemaweb.com/function-level-scope](https://poiemaweb.com/js-scope#3-function-level-scope)