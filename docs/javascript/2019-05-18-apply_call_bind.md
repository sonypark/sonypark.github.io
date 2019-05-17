2019년 5월 18일

# apply, call, bind 를 이용한 this 바인딩
___

#### **apply()**
> Syntax: `function.apply(thisArg, [argsArray])`

- `thisArg` : function 내부의 **this 를 바인딩 할 객체**

- `[argsArray]` : function 이 필요로 하는 **파라미터를 담을 배열**

#### **call()**
> Syntax: `function.call(thisArg, arg1, arg2, ...)`

- `thisArg` : function 내부의 **this 를 바인딩 할 객체**

- `arg1, arg2 ...` : function 이 필요로 하는 **각각의 파라미터**

#### **bind()**
> Syntax: `function.bind(thisArg[, arg1[, arg2[, ...]]])`

- `thisArg` : function 내부의 **this 를 바인딩 할 객체**



### apply 를 이용한 명시적 this 바인딩
> 출처: 인사이드 자바스크립트 (p116)

```javascript
function Person(name, age, gender){
    this.name = name;
    this.age = age;
    this.gender = gender;
}

// 빈 객체 생성
const sony = {}

// apply() 메서드 호출
Person.apply(sony, ['sony', 20, 'man']);
console.log(sony) // {name: "sony", age: 20, gender: "man"}
```

- 위 예제 코드의 의미는 다음과 같다.
- `Person('sony', 20, man)`함수를 호출 하라
- 이 때 Person 함수 내부의 `this`를 `sony 객체`에 `바인딩`하라



### call 을 이용한 명시적 this 바인딩

- 위 예제를 call 을 이용해 바인딩 하면 다음과 같다.

```javascript
Person.call(sony, 'sony', 20, 'man')
```

- `apply`와 `call`의 차이는 **두 번째 인자**로 넘겨주는 **인자값의 형식**이다.

    - `apply`: **배열 형태**로 넘긴다.
    - `call` : **각각 하나의 인자**로 넘긴다.
> `apply`, `call`을 호출하는 함수가 필요로 하는 파라미터를 두 번째 인자값으로 넘겨준다.
>
> 위의 예제에서 Person 함수가 `apply`, `call` 함수를 호출한다.
>
> Person 함수는 `name`, `age`, `gender`를 파라미터로 받으므로 해당 파라미터를 두 번째 인자값으로 넣어준다. 


## apply, call 과 bind 는 다르다


- **bind** 는 **`this` 를 바인딩한 새로운 함수를 리턴한다.** 

  - `this` 를 바인딩한 함수를 **나중에 사용할 때 쓴다.**
- **apply, cal**l 은 **`this`를 바인딩한 함수를 바로 실행한다**

  - `this` 를 바인딩 한 함수를 **바로 사용할 때 쓴다.**



```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( function() {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }, 1000);
    }
}

myflower = new Garden('Lily');
myflower.grow(); // TypeError: this.grow is not a function
```

- 위 예제를 실행하면 에러가 발생한다.
- 그 이유는 `setTimeout`의 콜백함수의` this`가 `window`를 가리키기 때문이다.
- 기대하는 결과는 `setTimeout`의 콜백함수의 `this`가 `myflower`를 가리키도록 하는 것이다.



## bind를 이용한 this 바인딩

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( function() {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }.bind(this), 1000);
    }
}

myflower = new Garden('Lily');
myflower.grow();

// 식물이 쑥쑥 자라는 중입니다.
// 식물이 쑥쑥 자라는 중입니다.
// 식물이 쑥쑥 자라는 중입니다.
```

- `bind`를 사용하면 `this`를 원하는 객체에 바인딩 할 수 있다.
- 위와 같이 `setTimeout` 함수를 실행할 때 생성자 함수의 `this`를 바인딩 해주면 된다.
- 생성자 함수의 `this`는 생성자 함수가 생성한 객체를 가리키므로 위 예제에서 this는 `myflower`를 가리킨다.
  - 생성자 함수: `Garden의 constructor`, 생성자 함수가 생성한 객체: `myflower`


- 좀 더 보기 좋게 아래와 같이 바꿀 수도 있다.

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
        this.bindGrowCallback = this.growCallback.bind(this);
    }

    growCallback(){
        console.log('식물이 쑥쑥 자라는 중입니다.');
        this.grow();
    };

    grow() {
        // 둘 중 하나 사용
        setTimeout(this.growCallback.bind(this), 1000);
        setTimeout(this.bindGrowCallback, 1000);
    }
}
```



### 참고) Arrow Function을 이용하면 lexical scope에 의해 this를 바인딩 할 수 있다.

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( () => {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }, 1000);
    }
}

myflower = new Garden('Lily');
myflower.grow();

// 식물이 쑥쑥 자라는 중입니다.
// 식물이 쑥쑥 자라는 중입니다.
// 식물이 쑥쑥 자라는 중입니다.
```

- 위 예제에서 `setTimeout`을 **arrow function**으로 바꾸었다.
- `setTimeout`이 선언된 지점에서 `this`는 **lexical scope**에 의해 상위 스코프인 `grow` 함수의 `this`를 가리킨다.
- `grow` 함수는 `Garden` 클래스의 메서드이므로 `grow` 함수 내의 `this`는 `Garden` 클래스의 생성자 함수가 만든 **객체**를 가리킨다.
- 따라서 결과는 `bind`를 이용했을 때와 동일하다.



## call 을 이용한 this 바인딩

- Garden 클래스의 grow 메서드가 아닌 윈도우 객체의 grow 메서드를 호출하도록 해보자

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( function() {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }, 1000);
    }
}

function grow() {
    setTimeout(function () {
        console.log('식물이 지맘대로 자라요');
        this.grow()
    }, Math.random()*2000)
}

myflower = new Garden('Lily');
myflower.grow.call(window);

// 식물이 쑥쑥 자라는 중입니다.
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
```

- `myflower.grow.call(window)`: `myflower`의 `grow` 함수를 호출 할 때 `this`를 `window` 객체로 바인딩한다.
- 즉, `myflower`의 `grow` 메서드 안의 `this`는 `window`를 가리킨다.
- 따라서 `myflower`의 `grow` 메서드 안의` this.grow`는 윈도우 객체의 `grow` 함수를 호출한다.
- 사실 `setTimeout`의 콜백함수의 `this`가 `window`를 가리키기 때문에 `myflower.grow()` 라고만 써도 똑같이 동작한다.



## this 바인딩을 이용하여 다른 객체의 메서드 실행 하기

### bind를 이용한 this 바인딩

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( function() {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }.bind(otherObject), 1000);
    }
}

const otherObject = {
    grow() {
        setTimeout(() => {
            console.log('식물이 지맘대로 자라요');
            this.grow()
        }, Math.random()*2000)
    }
};


myflower = new Garden('Lily');
myflower.grow();

// 식물이 쑥쑥 자라는 중입니다.
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
```

- `bind`를 이용해 `this`를 `otherObject`에 바인딩했다.

### bind + call 을 이용한 this 바인딩

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( function() {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }.bind(this), 1000);
    }
}

const otherObject = {
    grow() {
        setTimeout(() => {
            console.log('식물이 지맘대로 자라요');
            this.grow()
        }, Math.random()*2000)
    }
};


myflower = new Garden('Lily');
myflower.grow.call(otherObject);

// 식물이 쑥쑥 자라는 중입니다.
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
```

- `setTimeout`의 **콜백 함수**가 **일반 함수(funciton)**이므로 콜백 함수의 `this`는 `전역객체(window)`를 가리킨다.
- 따라서 `bind`를 이용해 `grow`함수가 가리키는 `this(otherObject)`로 바인딩 해줘야 한다.
    
    - 위 예제의 this 바인딩 과정
    
        1. **`call`**을 이용해 `myflower.grow` 메서드의 `this` 를 `otherObject`로 바인딩한다.
        2. **`bind`**를 이용해 `setTimeout` 함수의 콜백함수에 `grow` 함수의 `this(otherObject)`를 바인딩한다.



### call 을 사용한 this 바인딩

- `call` 만 사용해 다른 객체의 메서드를 바인딩 하려면 **arrow function**을 활용하면 된다.

```javascript
class Garden {
    constructor(flower){
        this.flower = flower;
    }

    grow() {
        setTimeout( () => {
            console.log('식물이 쑥쑥 자라는 중입니다.');
            this.grow();
        }, 1000);
    }
}

const otherObject = {
    grow() {
        setTimeout(() => {
            console.log('식물이 지맘대로 자라요');
            this.grow()
        }, Math.random()*2000)
    }
};


myflower = new Garden('Lily');
myflower.grow.call(otherObject);

// 식물이 쑥쑥 자라는 중입니다.
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
// 식물이 지맘대로 자라요
```

- `setTimeout`의 콜백 함수를 **arrow function**으로 바꾸었다.
- 따라서 콜백 함수의 `this`는 상위 스코프(`grow` 함수)의 `this` 를 가리킨다.
- 그리고 `myflower.grow.call(otherObject)` 을 이용해 `grow` 함수의 `this`를 `otherObject`로 바인딩 했다.
- 그러므로 콜백 함수의 `this`는 `otherObject` 를 가리킨다.

___
### Reference

- [코드스쿼드 - 크롱 강의](https://codesquad.kr/)
- [인사이드 자바스크립트](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788968480652)