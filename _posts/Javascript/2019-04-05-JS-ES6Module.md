---
layout: post
title: ES6 Module
category: Javascript

tags: [Javascript, ES6, module]
comments: true
---

![es6-logo](https://user-images.githubusercontent.com/34808501/55971946-6e437600-5cbd-11e9-9796-1dd7b29cfed2.png)


# ES6 Module

## Module
> 모듈이란 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각을 말한다. 모듈은 세부 사항을 캡슐화하고 공개가 필요한 API만을 외부에 노출한다.

![module-pattern](https://user-images.githubusercontent.com/34808501/55971984-82877300-5cbd-11e9-8af3-082e1981b11b.png)

- 일반적으로 모듈은 파일 단위로 분리되어 있으며 애플리케이션은 필요에 따라 명시적으로 모듈을 로드하여 재사용한다.

- 모듈은 기능별로 분리되어 작성되므로 코드의 단위를 명확히 분리하여 애플리케이션을 구성할 수 있으며 재사용성이 좋아 개발 효율성과 유지보수성을 높일 수 있다.

- Javascript는 기본적으로 모듈 기능을 제공하지 않는다.
- 하지만 자바스크립트를 클라이언트 사이드에 국한하지 않고 범용적으로 사용하고자 하는 움직임이 생기면서 모듈 기능은 반드시 해결해야 하는 핵심 과제가 되었고 이런 상황에서 제안된 것이 `CommonJS`와 `AMD(Asynchronous Module Definition)`이다.

- 서버 사이드 자바스크립트인 Node.js는 모듈 시스템의 사실상 표준(de facto standard)인 `CommonJS`를 채택하였고 현재는 독자적인 진화를 거쳐 `CommonJS` 사양과 100% 동일하지는 않지만 기본적으로 `CommonJS` 방식을 따르고 있다.

- ES6에서는 클라이언트 사이드 자바스크립트에서도 동작하는 모듈 기능을 추가하였다. 

- 단, 현재 대부분의 브라우저가 ES6의 모듈을 지원하지 않고 있으므로 현재의 브라우저에서 ES6 모듈을 사용하려면 `SystemJS`, `RequireJS` 등의 모듈 로더 또는 `Webpack` 등의 모듈 번들러를 사용하여야 한다.

## ES6 Module
- **`export`**
- **`import`**

 ## `export`

- 모듈 안에 선언한 항목을 외부에 공개하여 다른 모듈들이 사용할 수 있게 하고 싶다면 export 해야 한다. 
- 선언된 변수, 함수, 클래스 모두 export 할 수 있다. 

```javascript
// lib.js
// 변수 공개
export const pi = Math.PI;

// 함수 공개
export function square(x) {
  return x * x;
}

// 클래스 공개
export class Person {
  constructor(name) {
    this.name = name;
  }
}
``` 

- 선언문 앞에 매번 export 키워드를 붙이는 것이 싫다면 export 대상을 모아 하나의 객체로 구성하여 한번에 export할 수도 있다.

```javascript
// lib.js
const pi = Math.PI;

function square(x) {
  return x * x;
}

class Person {
  constructor(name) {
    this.name = name;
  }
}

// 변수, 함수 클래스를 하나의 객체로 구성하여 공개
export { pi, square, Person };
```

## `import`
> export한 모듈을 로드하려면 export한 이름으로 import한다.
  
```javascript
// main.js
// 같은 폴더 내의 lib.js 모듈을 로드. 확장자 js는 생략 가능.
import { pi, square, Person } from './lib';

console.log(pi);         // 3.141592653589793
console.log(square(10)); // 100
console.log(new Person('Lee')); // Person { name: 'Lee' }
```

- 각각의 이름을 지정하지 않고 하나의 이름으로 한꺼번에 import할 수도 있다. 
- 이때 import되는 항목은 as 뒤에 지정한 이름의 변수에 할당된다.

```javascript
// main.js
// lib라는 이름으로 임포트
import * as lib from './lib';

console.log(lib.pi);         // 3.141592653589793
console.log(lib.square(10)); // 100
console.log(new lib.Person('Lee')); // Person { name: 'Lee' }
```

- 이름을 변경하여 import할 수도 있다.

```javascript
// main.js
import { pi as PI, square as sq, Person as P } from './lib';

console.log(PI);    // 3.141592653589793
console.log(sq(2)); // 4
console.log(new P('Kim')); // Person { name: 'Kim' }
```

- 모듈에서 하나만을 export할 때는 default 키워드를 사용할 수 있다. 
- 단, default를 사용하는 경우, var, let, const는 사용할 수 없다.
  
```javascript
// lib.js
function (x) {
  return x * x;
}

export default;
```

- 위 코드는 아래와 같이 축약할 수 있다.

```javascript
// lib.js
export default function (x) {
  return x * x;
}
```

- default 키워드로 export한 모듈은 {} 없이 임의의 이름으로 import한다.

```javascript
// main.js
import square from './lib';

console.log(square(3)); // 9
```

> 현재 대부분의 브라우저가 ES6의 모듈을 지원하지 않고 있으므로 ES6 모듈을 현재의 브라우저에서 사용하기 위해서는 `SystemJS`, `RequireJS` 등의 모듈 로더 또는 `Webpack` 등의 모듈번들러를 사용하여야 한다.


### Reference

- [Poiemaweb.com/es6-module](https://poiemaweb.com/es6-module)








