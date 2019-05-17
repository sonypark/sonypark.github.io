# VSCODE - Node.js Debugging
____
## Break Point

- Debug mode로 코드를 실행하면 `Break Point`가 지정된 라인에서 멈춘다.
- 이 상태에서 값을 확인하고 명령어를 실행하면서 디버깅을 한다.

### breakpoints의 종류

- `expression condition`
    - 조건을 설정할 수 있다.

- `hit point`
    - 특정 hit 반복 후 break
    - 반복문에서 특정 횟수만큼 실행 후 값을 확인할 때 유용하다.

- `Log message`
    - 프로그램을 멈추지 않고 콘솔창에 로그 메시지를 남긴다.

## Step over / Step into/ Step out

### Step over

- 현재 break 걸린 라인을 **실행 후 다음 라인으로 이동한다.**
- 현재 break 걸린 라인에 함수가 존재하면 실행하고 그 **함수 안으로는 들어가지 않는다.**

- 아래 코드를 디버깅 한다고 가정하자.

```javascript
function updateHeader() {
  var day = new Date().getDay();
  var name = getName(); // A
  updateName(name); // D
}
function getName() {
  var name = app.first + ' ' + app.last; // B
  return name; // C
}
```

- Breakpoint로 `A`에 멈춰있는 상태에서 `step over` 버튼을 누르면 `B,C` (`getName()`함수)가 실행되고 `D`에서 멈춘다.

### Step into

- 현재 break 된 라인에 함수가 있다면 해당 **함수 안으로 들어가 라인별로 코드를 실행한다.**

- 현재 **break 된 라인에 있는 함수가 디버깅을 하는데 중요한 함수일 때** `step into`를 이용해 해당 함수 안으로 들어가서 살펴본다.

```javascript
function updateHeader() {
  var day = new Date().getDay();
  var name = getName(); // A
  updateName(name);
}
function getName() {
  var name = app.first + ' ' + app.last; // B
  return name;
}
```

- `A`에 멈춰 있는 상태에서 `step into`를 누르면 현재 라인을 실행하고 `getName()`함수로 들어가 `B`에서 멈춘다.

### Step out

- `step into로 들어온 함수`를 **끝까지 실행하고 빠져나온다.**
- 보통 step into로 파고 들어간 **함수에서 빠져 나올 때 사용한다.**

```javascript
function updateHeader() {
  var day = new Date().getDay();
  var name = getName();
  updateName(name); // C
}
function getName() {
  var name = app.first + ' ' + app.last; // A
  return name; // B
}
```

- `A`에 멈춰 있는 상태에서 `step out`을 누르면 `getName()` 함수의 나머지 코드(`B`)를 실행하고 `C`에서 멈춘다.


### Watch 사용법

- watch를 사용하면 break 된 상태에서 코드를 실행하며 **특정 변수 또는 함수값을 체크**할 수 있다.

- break 된 라인에서 사용 가능한 모든 값과 메서드를 사용할 수 있다.

- 단, watch에서 값을 변경하는 코드를 사용한 경우 의도치 않게 다른 로직을 수행할 수 있으니 주의하자.

다음과 같이 1부터 9까지 더하는 함수가 있다고 가정하자.

```javascript
function sum1to9() {
    let result = 0;
    for(let i = 0; i < 10; i++){
        result = result+i;
    }
}
```

- 위 코드에서 watch를 이용해 디버깅 할 때 i = i + 3을 할 경우 i의 값이 변경된다.

- 코드가 복잡해질수록 체크해야 할 사항이 늘어난다.(수 천개의 변수, 객체, 요소들이 생긴다.)
이 때 watch를 이용해 원하는 것만 추적하면 유용하다.

### Call Stack

> 코드 실행에 따라 call stack이 쌓이는 공간

- `call stack`은 기본적으로 프로그램 상에서 우리가 어디에 있는지를 기록하는 자료구조이다.

- 만약 함수를 실행하면, 해당 함수는 호출 스택의 가장 상단에 위치한다(`push`).

- **함수의 실행이 끝날 때**(리턴 값을 돌려줄 때), 해당 함수를 **호출 스택에서 제거한다**(`pop`).


```javascript
function multiply(x, y) {
    return x * y;
}
function printSquare(x) {
    var s = multiply(x, x);
    console.log(s);
}
printSquare(5);
```

- 위의 코드를 실행하기 전에는 `call stack`은 비어있다.
- 하지만 코드가 실행되면서 `call stack`은 다음과 같이 변한다.

![img](../javascript/img/call_stack_img1.png)

- `call stack`의 `각 단계(step)`를 `stack frame`이라고 한다.

> 특정 시점에 함수 호출 횟수가 `call stack`의 최대 허용치를 넘게 되면 `stackoverflow`가 발생한다.

![img](../javascript/img/call_stack_overflow_img.png)

- `call stack`에는 break 라인에 오기 전 까지 실행된 로직들이 표시된다.

- 이를 통해 이전에 어떤 값들이 넘어왔는지, 이전에 다른 연산을 했을 때 값이 어떻게 바뀔지를 확인 할 수 있다.

- `call stack`에서 찾고자 하는 코드 라인을 클릭하면 해당 라인으로 이동한다.

- 이동 후에  break 라인에서 했던 것처럼 `variables` 와 `watches`를 통해 원하는 값과 코드를 확인할 수 있다.

- 프레임워크에서 어떻게 코드가 실행되고 값이 변경되는지 확인할 때 매우 유용하다.
____
### Reference

- [Chrome DevTools에서 자바스크립트 디버깅 시작하기](https://developers.google.com/web/tools/chrome-devtools/javascript/?hl=ko)

- [Break Point로 코드 일시 중지하기](https://developers.google.com/web/tools/chrome-devtools/javascript/breakpoints?hl=ko#function)

- [JavaScript Debugging Reference  |  Tools for Web Developers  |  Google Developers](https://developers.google.com/web/tools/chrome-devtools/javascript/reference?hl=ko)

- [How JavaScript works: an overview of the engine, the runtime, and the call stack](https://blog.sessionstack.com/how-does-javascript-actually-work-part-1-b0bacc073cf)
