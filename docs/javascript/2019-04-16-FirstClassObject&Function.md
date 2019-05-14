2019년 4월 16일

# Javascript 1급객체, 1급함수

## 1급 시민(First class citizen)이란?

- 1급시민 이라는 말은 권한을 많이 누리는 대상이라고 볼 수 있다.
- 이를테면 다음과 같은 권한들이다.

    - 1급 시민은 투표권이 있다.
    - 1급 시민은 군인이 될 수 있다.
    - 1급 시민은 정치에 참여 할 수 있다.


## 프로그래밍에서 1급(First class)이란?

- 아래 조건을 충족시켜야 한다.

    - **함수의 인자**가 될 수 있다.
    - **함수의 리턴**이 될 수 있다.
    - **변수에 할당** 될 수 있다. 
    
- 예를들어, 자바스크립트에서 primitive types는 1급 시민이다.
> primitive types: String, Number, Boolean, undefined, null    
    
```javascript
const n = 1; // 숫자는 변수에 담긴다.
function test_int(a){
	return a;
}

const int = test_int(3);  // 숫자는 함수의 인자가 된다.
console.log(int);   // 숫자는 함수의 리턴이 된다.
```

## 1급 객체(First class object)
> 자바스크립트의 객체는 1급객체이다.

- 자바스크립트의 **객체**는 **함수의 인자**가 될 수 있다.
- 자바스크립트의 **객체**는 **함수의 리턴**이 될 수 있다.
- 자바스크립트의 **객체**는 **변수에 할당** 될 수 있다.

```javascript
const tmp_obj = { name :'first class object1'};   // 객체는 변수에 담긴다.

function test_obj(obj){
	return obj;
}

const obj = test_obj(tmp_obj);   // 객체는 함수의 인자가 된다.
console.dir(obj);  // 객체는 함수의 리턴이 된다.
```

## 1급 함수(First class function)
> 자바스크립트의 함수는 1급함수이다.

- 자바스크립트의 **함수**는 **함수의 인자**가 될 수 있다.
- 자바스크립트의 **함수**는 **함수의 리턴**이 될 수 있다.
- 자바스크립트의 **함수**는 **변수에 할당** 될 수 있다.

```javascript
const fn_outer = function(){
  	console.log('fn_outer 함수 동작...');
  return function(){  // 함수는 함수의 리턴이 될수있다.
  	console.log('리턴되는 함수가 동작...');
  };
};

const ret_fn = fn_outer(); // 함수는 변수에 담긴다.
ret_fn();    
```

```javascript
function cal(func, num){ // 함수는 함수의 인자가 될 수 있다.
    return func(num) // 함수는 함수의 리턴이 될 수 있다.
}
function increase(num){
    return num+1
}
function decrease(num){
    return num-1
}

const inc_fn = cal(increase, 1); // 함수는 변수에 할당될 수 있다.
const dec_fn = cal(decrease, 1);
```

### Reference

- [HANUMOKA 블로그](https://blog.hanumoka.net/2017/08/31/javascript-20170831-javascript-first-object/)
- [생활코딩: javascript 값으로서의 함수와 콜백](https://opentutorials.org/course/743/6508)