
# Promise

---

## Promise 란

- Promise는 **비동기 이벤트 작업의 결과**를 리턴하는 객체이다.

- Promise 객체는 비동기 작업이 완료되었을 때 **결과값**(`value`) 또는 **에러**(`error`)를 리턴한다.

## Promise의 상태(state) 정보

#### 프로미스 객체는 다음 세 가지 상태 중 하나를 갖는다.

1. `Pending` : promise 객체를 생성했을 때의 상태

2. `Resolved` / `Fulfilled`  : 비동기 처리가 정상적으로 이루어졌을 때의 상태, `value`를 리턴한다.

3. `Rejected` : 비동기 처리가 실패했을 때의 상태, `error`를 리턴한다.

![promise](https://user-images.githubusercontent.com/34808501/58876618-9e315780-8709-11e9-98c3-a4c75782ee24.png)

그림 출처 : https://www.udemy.com/nodejs-master-class/

## Promise object

- Promise를 사용하기 위해 `Promise` **객체**를 생성한다.

- Promise 객체는 `new Promise((res,rej)={})` 명령어로 생성한다.

- Promise 객체는 두 개의 파라미터(`resolve`, `reject`)를 갖는 함수를 인자값으로 받는다.

- `resolve`, `reject` 는 모두 함수이다.

```javascript
const p = new Promise((resolve, reject) => {
    // Kick off some async work  
    // ...  
    resolve(1);  // pending => resolved, fulfilled
    reject(new Error('ERROR!!!');  // pending => rejected
});

p.then(result => console.log('Result: ', result));
```

- `resolve` 는 비동기 처리가 성공했을 때의 결과(`value`)를 리턴한다.

- 리턴값으로 비동기 처리에서 얻은 결과값을 넣는다.

- `reject` 는 비동기 처리 과정에서 문제가 발생했을 때 에러(`error`)를 리턴한다.

- Promise 객체는 `then` 과 `catch` 라는 두 메서드를 갖는다.

    - `then` : 비동기 처리로 얻은 결과값을 받는다.
    - `catch` : 비동기 처리 도중 발생한 에러 메시지를 받는다.

```javascript
p.then(result => console.log('Result: ', result));
```

- `then` 메서드는 인자로 함수를 받는다. 함수의 인자값에는 `resolve` 에서 보낸 `value` 가 들어온다.

- 위 코드를 실행한 결과는 다음과 같다.

```bash
Result:  1
```

- 위 예제 코드에는 비동기 작업이 없다.
- `setTimeout` 함수를 이용해 비동기 작업을 처리해보자

```javascript
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(1);
    }, 2000);
});

p.then(result => console.log('Result: ', result));
```

- 위 코드를 실행하면 2초 뒤에 동일한 결과값을 얻는다.

```bash
Result:  1
```

- 이번에는 비동기 작업 도중에 **에러**를 발생시켜보자.

```javascript
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        // resolve(1);  
        reject(new Error('ERROR!!!'));
    }, 2000);

});

p
    .then(result => console.log('Result: ', result))
    .catch(err => console.log('Error: ', err.message));
```

- `catch` 메서드 또한  인자로 함수를 받는다. 함수의 인자값에는 `reject` 에서 보낸 `error` 객체 가 들어온다. 
- `reject`에서 보낸 에러 메시지는 `error` 객체 안의 `message` 속성에 들어있다.
- 따라서 에러 메시지를 출력하려면 `err.message` 형태로 접근하면 된다.
- 위 코드를 실행한 결과는 다음과 같다.
```bash
Error: ERROR!!!
```

### 정리

1. Promise 객체는 다음 세 가지 상태를 갖는다.

    1. `Pending` : promise 객체를 생성했을 때의 상태

    2. `Resolved` / `Fulfilled`  : 비동기 처리가 정상적으로 이루어졌을 때의 상태, `value`를 리턴한다.

    3. `Rejected` : 비동기 처리가 실패했을 때의 상태, `error`를 리턴한다.

2. 비동기 작업의 결과를 확인하기 위해 다음 두 메서드를 사용한다.

    - `then` : **(성공)** 비동기 처리로 얻은 **결과값**을 얻는다.

    - `catch` : **(실패)** 비동기 처리 도중 발생한 **에러 메시지**를 얻는다.

### 비동기 작업은 callback이 아닌 Promise를 사용하자

> 콜백 함수를 인자값으로 받는 비동기 함수는 Promise를 리턴하는 함수로 수정해보자.

- 아래 함수를 Promise를 리턴하는 함수로 바꿔보자.

```javascript
function getUser(id, callback) {
    setTimeout(() => {
        console.log('Reading a user from a database...');
        callback({ id: id, gitHubUsername: 'sony' });
    }, 2000);
}
```
  
- `callback` 함수 부분을 `Promise` 객체의 `resolve`로 대체한다
  
```javascript
function getUser(id) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('Reading a user from a database...');
            resolve({ id: id, gitHubUsername: 'sony' });
        }, 2000);
    });
}
```

- `resolve`는 비동기 처리 결과값(`value`)을 리턴한다.
- 위 예제에서의 결과값(`value`)은 `{ id: id, gitHubUsername: 'sony' }` 이다.

### Exercise

- 위에서 배운 내용을 바탕으로 아래 코드를 수정해보자.

>요구 사항: 콜백 함수를 인자값으로 받는 비동기 함수를 Promise를 리턴하는 함수로 수정한다.

```javascript
console.log('Before');
getUser(1, (user) => {
    getRepositories(user.gitHubUsername, (repos) => {
        getCommits(repos[0], (commits) => {
            console.log(commits);
        })
    })
});
console.log('After');


function getUser(id, callback) {
    setTimeout(() => {
        console.log('Reading a user from a database...');
        callback({ id: id, gitHubUsername: 'mosh' });
    }, 2000);
}

function getRepositories(username, callback) {
    setTimeout(() => {
        console.log('Calling GitHub API...');
        callback(['repo1', 'repo2', 'repo3']);
    }, 2000);
}

function getCommits(repo, callback) {
    setTimeout(() => {
        console.log('Calling GitHub API...');
        callback(['commit']);
    }, 2000);
}
```

- 수정한 코드는 다음과 같다.

```javascript
console.log('Before');
getUser(1)
    .then(user => getRepositories(user.gitHubUsername))
    .then(repos => getCommits(repos[0]))
    .then(commits => console.log(commits))
    .catch(err => console.log("Error", err.message));
console.log('After');


function getUser(id) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('Reading a user from a database...');
            resolve({ id: id, gitHubUsername: 'mosh' });
        }, 2000);
    });
}

function getRepositories(username) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('Calling GitHub API...');
            resolve(['repo1', 'repo2', 'repo3']);
        }, 2000);
    })
}

function getCommits(repo) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('Calling GitHub API...');
            resolve(['commit']);
        }, 2000);
    })
}
```

### Unit Test에서 Promise Class 사용하기

- 이미 `resolved` 된 Promise를 생성해야할 때가 있다.

- 특히 **unit test**를 할 때 유용하다.

- 예를 들어, 웹 서비스를 호출하는 비동기 작업을 시뮬레이션 하는 경우 Promise를 이용해 `resolve` 된 상황과 `reject` 된 상황을 테스트 해볼 수 있다.

- 이 경우에는 `Promise` **객체**가 아닌  `Promise` **클래스**를 선언하고 `Promise` **클래스 메서드**인 `resolve`, `reject`를 사용한다.

- 먼저 비동기 작업이 `resolve` 된 경우를 테스트 해보자.

```javascript
const p = Promise.resolve({id: sony});
p.then(result => console.log(result));
```

- 위 코드를 실행한 결과는 다음과 같다.

```bash
{id:1}
```

- 비동기 작업이 `reject`된 경우도 테스트 해보자.

```javascript
const p = Promise.reject(new Error('Reason for rejection...'));
p.catch(error => console.log(error));
```

- 위 코드를 실행한 결과는 다음과 같다.

```bash
Error: Reason for rejection...
    at Object.<anonymous> (/Users/sony/async-demo/index.js:79:26)
    at Module._compile (internal/modules/cjs/loader.js:701:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:712:10)
    at Module.load (internal/modules/cjs/loader.js:600:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:539:12)
    at Function.Module._load (internal/modules/cjs/loader.js:531:3)
    at Function.Module.runMain (internal/modules/cjs/loader.js:754:12)
    at startup (internal/bootstrap/node.js:283:19)
    at bootstrapNodeJSCore (internal/bootstrap/node.js:622:3)
```

- 이처럼 `Promise` 클래스의 메서드인 `resolve`, `reject`를 이용하여 비동기 작업을 시뮬레이션 해볼 수 있다.

### Running Parallel Promises

- 여러 개의 Promise를 실행하고 모든 Promise가 `resolve` 되었을 때 다음 작업을 실행하고 싶은 경우에는 어떻게 할까?

- 예를 들어, Facebook API와 Instagram API를 실행하고 이 두 API가 모두 비동기 처리를 완료했을 때 클라이언트에게 응답을 전달해야 할 경우를 생각해보자.

- 이 때 사용하는 것이 `Promise.all()` 이다.

- 아래 코드를 보자

```javascript
const p1 = new Promise((resolve => {
  setTimeout(()=>{
    console.log('Async operation 1..');
    resolve(1);
  },2000)
}));

const p2 = new Promise((resolve => {
  setTimeout(()=>{
    console.log('Async operation 2..');
    resolve(2);
  },2000)
}));

Promise.all([p1,p2])
    .then(result => console.log(result));
```

- 두 개의 **Promise 객체** `p1`,`p2`가 있다.

- `p1`,`p2`를 `Promise.all()`의 인자값으로 넣는다. 이 때 배열 형태 `[]`로 넣는다.

- 위 코드를 실행한 결과는 다음과 같다.

```bash
Async operation 1..
Async operation 2..
[ 1, 2 ]
```

### `Promise.all()`의 특징

- 여러개의 Promise 객체가 모두 `resolve` 된 후에 작업을 진행하기 위해 사용한다.

1. Promise 객체를 배열(`[]`) 형태로 받는다.

2. Promise.all()도 새로운 Promise 객체를 리턴한다.

3. **Promise.all()이 리턴한 Promise 객체** 또한 `pending`, `resolve`, `recject` 세 가지 상태를 갖는다.

    - `Pending` : 인자로 받은 여러 개의 Promise 객체가 결과값을 리턴하기 전까지의 상태

    - `Resolve` : 인자로 받은 Promise 객체가 **모두** `resolve` 된 경우

    - `Reject` : 인자로 받은 Promise 객체 중 **하나라도** `reject` 된 경우

#### 아래 코드와의 차이점

> `Promise.then` chaining

```javascript
// Promise.then chaining code
getUser(1)
    .then(user => getRepositories(user.gitHubUsername))
    .then(repos => getCommits(repos[0]))
    .then(commits => console.log(commits))
    .catch(err => console.log("Error", err.message));
```

- 위 코드에서 Promise 객체의 **실행 순서**는 `getUser()` => `getRepositories()` => `getCommits()` 이다.

- 각 Promise 객체의 **실행 시점**은 이전 Promise 객체가 `resolve` 된 이후이다.

- 즉, `getUser()`가 `resolve` 된 이후에만 `getRepositories()`가 실행될 수 있다. 또한 `getRepositories()`가 `resolve` 된 이후에만 `getCommits()` 이 실행될 수 있다.

- 하지만 `Promise.all()`을 이용하면 이 전 Promise 객체의 결과를 기다리지 않고 실행한다.

```javascript
Promise.all([p1,p2])
    .then(result => console.log(result));
```

- 위 코드에서 Promise 객체의 **실행 순서**는 `p1` -> `p2` 이다.

- 하지만 Promise 객체의 **실행 시점**에서는 큰 차이가 있다.

- `Promise.all()`을 이용하면 이 전 Promise 객체의 결과를 기다리지 않고 바로 실행한다.

- 즉, `p2`는 `p1`의 결과값을 기다리지 않고 바로 실행한다.

- 따라서 **실행 순서**는 `p1`이 `p2`보다 빠르지만 작업 **완료 시점**은 `p2`가 `p1` 보다 빠를 수 있다.

    - 비동기 처리 작업이 `p1`이 `p2`보다 오래 걸릴 수도 있기 때문이다.

    - 만약 `Promise.then` 으로 `chaining`했다면 `p2`는 항상 `p1`보다 늦게 종료 된다.

    - 하지만 `Promise.all`을 사용하면 먼저 완료된 작업이 먼저 종료된다.

#### 중간에 error 가 발생하는 경우

```javascript
const p1 = new Promise((resolve,reject) => {
  setTimeout(()=>{
    console.log('Async operation 1..');
    // resolve(1);
    reject(new Error('Something failed..'))
  },2000)
});

const p2 = new Promise((resolve => {
  setTimeout(()=>{
    console.log('Async operation 2..');
    resolve(2);
  },2000)
}));

Promise.all([p1,p2])
    .then(result => console.log(result))
    .catch(err => console.log(err.message));
```

- `Promise.all()`의 인자값으로 받은 여러 Promise 객체 중 **하나라도** `reject`가 되면 `Promise.all()`의 전체 결과값은 `reject` 된다.

- 위 코드에서는 `p1`의 결과값이 `reject` 되었다.
- 따라서 `Promise.all` 의 결과값도 `reject` 된다.

```bash
Async operation 1..
Async operation 2..
Something failed..
```

- `p1`의 결과에 상관없이 `p2`가 실행된 것을 알 수 있다.

- 또한 `p1`의 결과값이 `reject`이기 때문에 `p2`의 결과에 상관없이 `Promise.all` 의 결과값은 `reject`가 되었다.

### Promise.race()

> 여러 Promise 객체 중 가장 먼저 resolve된 Promise 객체의 결과값 (value)만 리턴한다

#### `Promise.all()` 과의 차이점은 다음과 같다.

- `Promise.all()`은 모든 Promise 객체가 `resolve` 되기를 기다렸다가 모두 `resolve`가 되면 결과(`resolve`)를 리턴한다.

- `Promise.race()`는 말 그대로 모든 Promise 객체가 레이스를 펼친다. 그 중 **가장 빠르게 `resolve`된 값만 리턴**한다.

- `Promise.all()`은 모든 Promise 객체의 결과값을 배열(`[]`)에 담아 리턴한다.

- `Promise.race()` 가장 빠른 Promise 객체의 결과값 하나(`value`)만 리턴한다.


```javascript
const p1 = new Promise((resolve) => {
  setTimeout(()=>{
    console.log('Async operation 1..');
    resolve(1);
  },2000)
});

const p2 = new Promise((resolve => {
  setTimeout(()=>{
    console.log('Async operation 2..');
    resolve(2);
  },2000)
}));

Promise.race([p1,p2])
    .then(result => console.log(result))
    .catch(err => console.log(err.message));
```

- 위 코드를 실행한 결과는 다음과 같다.

```bash
Async operation 1..
Async operation 2..
1
```

- 두 Promise 객체 `p1`, `p2` 모두 실행되었지만 가장 빠르게 `rosolve` 된 `p1`의 결과값(`1`)만 리턴한다.

----

### Reference

-  [Udemy: Nodejs - The Complete Guide to Build RESTful APIs](https://www.udemy.com/nodejs-master-class/)