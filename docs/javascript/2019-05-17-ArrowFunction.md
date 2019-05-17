2019년 5월 17일
# Arrow Function & this
___
## this

- function 키워드로 생성한 **일반 함수**와 **화살표 함수(arrow function)**의 **가장 큰 차이점**은 **this**이다.

## 함수 호출 방식과 this 바인딩

- function 키워드로 생성한 **일반 함수**의 경우 **호출 방식**에 의해 **this**에 **바인딩** 될 **객체**가 **동적**으로 **결정**된다.

- **this** 키워드는 **자신을 호출한 객체**를 가리킨다.
> 참고: [this keyword](https://sonypark.github.io/#/./docs/javascript/2019-04-28-JS_OOP?id=this-keyword)


 1. **일반 함수**에서 **`this`**는 **`window`**를 가리킨다.
    - **생성자 함수**와 **객체의 메서드**를 **제외**한 **모든 함수**(내부 함수, 콜백 함수 포함) **내부**의 **this**는 **전역 객체**를 가리킨다.
 2. **객체의 메서드**에서 **`this`**는 **`해당 객체`**를 가리킨다.
 3. **생성자 함수**에서 **`this`**는 **`생성자를 통해 생성된 객체`**를 가리킨다. 



## 화살표 함수(Arrow function)의 this

- **Arrow function**의 **`this`**는 항상 **`상위 스코프의 this`**를 가리킨다. - **`Lexical this`**
-  **Arrow function**은 **`Lexical this`**를 지원하므로 **콜백 함수**로 사용하기 편리하다.

```javascript
function Greet(greeting) {
  this.greeting = greeting;
}

Greet.prototype.greetArray = function (arr) {
  // this는 상위 스코프인 greetArray 메서드 내의 this를 가리킨다.
  return arr.map(x => `${this.greeting}  ${x}`);
};

const greet = new Greet('Hello');
console.log(greet.greetArray(['Sony', 'Park'])); // ['Hello Sony', 'Hello Park']
```





## Arrow function을 사용하면 안 되는 경우



### 1. 객체의 메서드

```javascript
// Bad
const person = {
  name: 'Sony',
  sayHi: () => console.log(`Hi ${this.name}`),
  printThis: () => console.log(`${this}`)
};

person.sayHi(); // Hi undefined
person.printThis(); // window
```

- **객체의 메서드**로 **Arrow function**을 사용하면 `this`는 `window`를 가리킨다.
- 따라서 객체의 메서드는 일반함수로 써야한다.

```javascript
// Good
const person = {
  name: 'Sony',
  sayHi: function(){console.log(`Hi ${this.name}`)},
  printThis: function(){ console.log(`${this}`)}
};

person.sayHi(); // Hi Sony
person.printThis(); // Object
```

- **객체의 메서드** 를 **일반함수**로 선언하면  `this`는 `해당 객체`를 가리킨다. 



### 2. prototype

```javascript
// Bad
const person = {
  name: 'Sony',
};

Object.prototype.sayHi = () => console.log(`Hi ${this.name}`);
Object.prototype.printThis = () => console.log(`${this}`);

person.sayHi(); // Hi undefined
person.printThis(); // window
```

-  **Arrow function**으로 정의한 메서드를 `prototype`에 할당하면 `this`는 `window`를 가리킨다.
- 따라서 `prototype`에 할당하는 메서드는 **일반함수**를 사용한다.

```javascript
// Good
const person = {
  name: 'Sony',
};

Object.prototype.sayHi = function(){console.log(`Hi ${this.name}`)};
Object.prototype.printThis = function(){console.log(`${this}`)};

person.sayHi(); // Hi Sony
person.printThis(); // Object
```



### 3. 생성자 함수

- 생성자 함수는 `prototype` 프로퍼티를 갖는다.
  - 새로운 객체를 생성할 때 `prototype` 프로퍼티가 가리키는 프로토타입 객체의 `constructor`를 사용한다.
- 하지만 **Arrow function**은 `prototype` **프로퍼티를 갖고 있지 않다.**
- 따라서 **Arrow function**은 **생성자 함수로 사용할 수 없다.**

```javascript
const Foo = () => {};

// 화살표 함수는 prototype 프로퍼티가 없다
console.log(Foo.hasOwnProperty('prototype')); // false

const foo = new Foo(); // TypeError: Foo is not a constructor
```

- **생성자 함수**에는 **일반 함수**를 사용한다.

```javascript
const Foo = function() {};

console.log(Foo.hasOwnProperty('prototype')); // true

const foo = new Foo();
```



### 4. addEventListener 함수의 콜백 함수

- **addEventListener** 함수의 콜백 함수를 화살표 함수로 정의하면 `this`가 상위 컨택스트인 전역 객체 `window`를 가리킨다.

```javascript
// Bad
var button = document.getElementById('myButton');

button.addEventListener('click', () => {
  console.log(this === window); // => true
  this.innerHTML = 'Clicked button';
});
```



- **addEventListener** 함수의 콜백 함수 내에서 `this`를 사용하는 경우, function 키워드로 정의한 **일반 함수**를 사용해야 한다.
- 일반 함수로 정의된 **addEventListener** 함수의 콜백 함수 내부의 `this`는 이벤트 리스너에 바인딩된 요소(`currentTarget`)를 가리킨다.

```javascript
// Good
var button = document.getElementById('myButton');

button.addEventListener('click', function() {
  console.log(this === button); // => true
  this.innerHTML = 'Clicked button';
});
```



## Exercise

> 출처: [인사이드 자바스크립트](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788968480652)



### 내부 함수의 this 바인딩 동작을 보여주는 예제 코드

- **내부 함수**의 `this`는 전역 객체 `window`를 가리킨다.
- **생성자 함수**와 **객체의 메서드**를 **제외**한 **모든 함수**(내부 함수, 콜백 함수 포함) **내부** 의  **this** 는 **전역 객체** 를 가리킨다.

```javascript
// 전역 변수 value 선언
var value = 100;

// myObject 객체 생성
var myObject = {
    value: 1,
    func1: function () {
        this.value += 1;
        console.log('func1() called. this.value : ' + this.value);

        //func2 내부 함수
        func2 = function () {
            this.value += 1;
            console.log('func2() called. this : ' + this);
            console.log('func2() called. this.value : ' + this.value);
            
            //func3 내부 함수
            func3 = function () {
                this.value += 1;
                console.log('func3() called. this : ' + this);
                console.log('func3() called. this.value : ' + this.value);
            };
            func3(); // func3() 내부 함수 호출
        };
        func2(); // func2() 내부 함수 호출
    }
};
myObject.func1(); // func1() 메서드 호출

// output:
// func1() called. this.value : 2
// func2() called. this : [object window]
// func2() called. this.value : 101
// func3() called. this : [object window]
// func3() called. this.value : 102
```


- **Arrow function**을 이용하면 내부함수의 `this`가 `myObject`를 가리키게 할 수 있다.

```javascript
// 전역 변수 value 선언
var value = 100;

// myObject 객체 생성
var myObject = {
    value: 1,
    func1: function () {
        this.value += 1;
        console.log('func1() called. this.value : ' + this.value);

        //func2 내부 함수
        func2 = () => {
            this.value += 1;
            console.log('func2() called. this : ' + this);
            console.log('func2() called. this.value : ' + this.value);

            //func3 내부 함수
            func3 =  () => {
                this.value += 1;
                console.log('func3() called. this : ' + this);
                console.log('func3() called. this.value : ' + this.value);
            };
            func3(); // func3() 내부 함수 호출
        };
        func2(); // func2() 내부 함수 호출
    }
};
myObject.func1(); // func1() 메서드 호출
// output:
// func1() called. this.value : 2
// func2() called. this : [object Object]
// func2() called. this.value : 3
// func3() called. this : [object Object]
// func3() called. this.value : 4
```

## 언제 Arrow function을 써야 할까?

- 가능한 function 키워드의 **일반 함수**보다 `Arrow function` 을 쓰도록 하자.
- [Google’s JavaScript Style Guide](https://medium.freecodecamp.org/google-publishes-a-javascript-style-guide-here-are-some-key-lessons-1810b8ad050b) 에도 `Arrow function` 을 사용할 것을 권하고 있다.
    
    - 그 이유는 다음과 같이 설명한다.
    
      1. 문법이 간단하다
      2. 가독성이 높다
      3. this 바인딩으로 인한 문제를 상당 부분 해결해준다. 
    
- 따라서 아래의 경우를 제외하고는 `Arrow function` 을 쓰도록 하자.
  
    - **Arrow function 을 사용하면 안 되는 경우**
      1. 객체의 메서드
      2. prototype에 할당하는 메서드
      3. 생성자 함수
      4. addEventListener 함수의 콜백 함수

___
### Reference

- [Arrow function | PoiemaWeb](https://poiemaweb.com/es6-arrow-function)
- [ECMAScript 6: New Features: Overview and Comparison](http://es6-features.org/#Lexicalthis)
- [인사이드 자바스크립트](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788968480652)
- [Google’s JavaScript Style Guide](https://medium.freecodecamp.org/google-publishes-a-javascript-style-guide-here-are-some-key-lessons-1810b8ad050b)