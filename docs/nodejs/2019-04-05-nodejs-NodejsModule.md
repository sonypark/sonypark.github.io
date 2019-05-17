2019년 4월 5일

![node-logo](https://user-images.githubusercontent.com/34808501/55972050-afd42100-5cbd-11e9-87a0-cdb791119fc6.png)

# Node.js Module
___
### Javascript의 약점

- Module 기능이 없다.
- `script tag`를 이용하여 외부의 스크립트 파일을 가져올 수는 있지만 파일마다 독립적인 파일 스코프를 갖지 않고 하나의 전역 객체(Global Object)에 바인딩되기 때문에 전역 변수가 중복되는 등의 문제가 발생할 수 있다.
- 따라서 모듈화가 불가능하다.(단, ES6에서는 모듈 기능을 추가했다. - `export, require`)

### Node.js는 module 단위로 각 기능을 분할할 수 있다. 
- module은 파일과 1대1의 대응 관계를 가지며 하나의 모듈은 자신만의 독립적인 실행 영역(Scope)를 가지게 된다. 
- 따라서 JavaScript와는 달리 전역변수의 중복 문제가 발생하지 않는다.

- Node.js 모듈은 module.exports 또는 exports 객체를 통해 정의하고 외부로 공개한다. 
- 공개된 모듈은 require 함수를 사용하여 임포트한다.

## `exports`
 
 - 모듈은 독립적인 파일 스코프를 갖기 때문에 모듈 안에 선언한 모든 것들은 기본적으로 해당 모듈 내부에서만 참조 가능하다.
 - 모듈 안에 선언한 항목을 외부에 공개하여 다른 모듈들이 사용할 수 있게 하고 싶다면 exports 객체를 사용해야 한다.
 - 외부에 공개할 대상을 exports 객체의 프로퍼티 또는 메서드로 정의한다.

```javascript
// circle.js
const { PI } = Math;

exports.area = (r) => PI * r * r;

exports.circumference = (r) => 2 * PI * r;
``` 

- circle.js는 독립적인 파일 스코프를 갖는 모듈이다. 
- circle 모듈에서 area와 circumference를 exports 객체의 메서드로 정의하였다. 
- 변수 PI는 circle 모듈에서만 유효한 private 변수가 되고, area와 circumference는 외부에 공개된다.

```javascript
// app.js
const circle = require('./circle.js'); // == require('./circle')

console.log(`지름이 4인 원의 면적: ${circle.area(4)}`);
console.log(`지름이 4인 원의 둘레: ${circle.circumference(4)}`);
```

- require 함수를 사용하여 circle 모듈을 import 한다.
- 이때 circle 모듈은 객체로 반환된다. 
- 따라서 circle.area, circle.circumference 와 같은 형식으로 사용가능하다.

```
$ node app
지름이 4인 원의 면적: 50.26548245743669
지름이 4인 원의 둘레: 25.132741228718345
```

## `module.exports`

- exports 객체는 프로퍼티 또는 메서드를 여러 개 정의할 수 있다. 
- 하지만 module.exports 에는 하나의 값(원시 타입, 함수, 객체)만 할당할 수 있다.

```javascript
// circle.js
const { PI } = Math;

module.exports = function (r) {
  return {
    area() { return PI * r * r; },
    circumference() { return 2 * PI * r}
  };
}
```

- circle 모듈의 module.exports 에 하나의 함수를 할당한다.

```javascript
// app.js
const circle = require('./circle');
const myCircle = circle(4);

console.log(`지름이 4인 원의 면적: ${myCircle.area()}`);
console.log(`지름이 4인 원의 둘레: ${myCircle.circumference()}`);
```
- require 함수를 통해 circle 모듈을 임포트하여 circle 변수에 할당한다. 
- 이때 circle 변수는 circle 모듈에서 module.exports에 할당한 값 자체 즉 객체를 반화하는 함수이다.

```javascript
// primitive.js
const pv = 'primitive value';
module.exports = pv;
```

```javascript
// app.js
const value = require('./primitive');
console.log(value); // => 'primitive value'
```

구분 | 모듈 정의 방식 | require 함수의 호출 결과
:---------:  | :---------------: | :-------------------:
export	| exports 객체에는 값을 할당할 수 없고 공개할 대상을 exports 객체에 프로퍼티 또는 메서드로 추가한다. | exports 객체에 추가한 프로퍼티와 메서드가 담긴 객체가 전달된다.
module.exports	| module.exports 객체에 하나의 값(원시 타입, 함수, 객체)만을 할당한다. | module.exports 객체에 할당한 값이 전달된다.

## `module.exports` 에 `함수` 할당하기

```javascript
// foo.js
module.exports = function(a, b) {
  return a + b;
};
```

```javascript
// app.js
const add = require('./foo');

const result = add(1, 2);
console.log(result); // => 3
```

- module.exports는 1개의 값만을 할당할 수 있다. 
- `객체`를 사용하면 복수의 기능을 하나로 묶어 export 할 수 있다.

## `exports`에 `객체` 할당하기

- 객체를 외부에 공개(`export`)하는 경우 다음과 같이 정의한다.

```javascript
// foo.js
module.exports = {
  add (v1, v2) { return v1 + v2 },
  minus (v1, v2) { return v1 - v2 }
};
```

```javascript
// app.js
const calc = require('./foo');

const result1 = calc.add(1, 2);
console.log(result1); // => 3

const result2 = calc.minus(1, 2);
console.log(result2); // => -1
```

## `require`

- require 함수의 인수에는 파일뿐만 아니라 디렉터리를 지정할 수도 있다.

```
project/
├── app.js
└── module/
    ├── index.js
    ├── calc.js
    └── print.js
```

- 아래과 같이 모듈을 명시하지 않고 require 함수를 호출하면 해당 디렉터리의 index.js을 로드한다.

```javascript
const myModule = require('./module');
```

- 이때 로드되는 index.js 내에서 calc.js과 print.js를 require하면 한번의 require로 alc.js과 print.js의 모든 기능을 사용할 수 있다.

```javascript
// module/index.js
module.exports = {
  calc: require('./calc'),
  print: require('./print')
};
```

```javascript
// module/calc.js
module.exports = {
  add (v1, v2) { return v1 + v2 },
  minus (v1, v2) { return v1 - v2 }
};
```

```javascript
// module/print.js
module.exports = {
  sayHello() { console.log('Hi!') }
};
```

```javascript
// app.js
const myModule = require('./module');

// module/calc.js의 기능
const result = myModule.calc.add(1, 2);

console.log(result);

// module/print.js의 기능
myModule.print.sayHello();
```

## 코어 모듈과 파일 모듈

> 코어 모듈: Node.js가 기본으로 포함하고 있는 모듈이다. 

>  코어 모듈을 로딩할 때에는 패스를 명시하지 않아도 된다.

```javascript
const http = require('http');
```

> npm을 통해 설치한 외부 패키지 또한 패스를 명시하지 않아도 된다.

```javascript
const mongoose = require('mongoose');
```

> 코어 모듈과 외부 패키지 이외는 모두 파일 모듈이다. 
> 파일 모듈을 로딩할 때에는 패스를 명시하여야 한다.

```javascript
const foo = require('./lib/foo');
```
___
### Reference

- [Modules - Node.js v11.13.0 Documentation](https://nodejs.org/api/modules.html)
- [Node.js의 module loading system](https://poiemaweb.com/nodejs-module)









