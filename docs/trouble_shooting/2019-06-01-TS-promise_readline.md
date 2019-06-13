2019년 6월 1일

# Promise를 이용한 readline 지옥 탈출

---

### 나는 어떻게 readline 지옥을 탈출했나

- 콘솔 버전 Todo App을 만들면서 입력값을 여러번 받는 기능을 구현하고 싶었다.
- 이 과정에서 겪은 시행착오를 공유하고자 한다.

## 1. 원하던 기능

### realine 재귀 호출

- 콘솔 창에서 회원가입 / 로그인 시 중복된 아이디를 입력하거나 잘못된 비밀번호를 입력하면 오류 메시지를 출력하고 다시 입력을 받아야한다.

- 이 때 `readline`을 **재귀 호출**하여 입력을 받고 싶었다.

- 구상했던 로직은 다음과 같다.

```bash
> 회원인가요? (yes/no)
> yes
> 아이디를 입력하세요
> sony
> 비밀번호를 입력하세요
> 123
> 입력한 정보가 올바르지 않습니다.
> 아이디를 입력하세요
> |
```

- 이런식으로 각 질문에 대한 입력값을 `readline`으로 받는다.
- 로그인 시 입력한 정보가 올바르지 않을 경우 로그인을 처음부터 다시 한다.

## 2. 문제 발생

- `readline`이 계속 쌓임

```javascript
const rl = require('readline');

const inputReadline = rl.createInterface({
    input : process.stdin,
    output: process.stdout,
});

class testApp {
    init() {
        inputReadline.question('회원인가요?(yes)', answer => {
            if (answer == 'yes') {
                return this.login();
            }
        });
    }

    login() {
        inputReadline.question('아이디를 입력하세요', (answer) => {
            if (answer === 'no') {
                return this.login();
            } else if (answer === 'yes') {
                return answer;
            }
        })
    }
}

const test = new testApp();
const answer = test.init();
console.log(answer);
```

- 위 코드는 처음에 작성한 테스트 코드이다.

- `readline`의 `question`만 이용해서 입력값을 받았다.

- `init()` 함수에서 `inputReadline.question()`을 호출하고 `login()`함수에서 또 다시 `inputReadline.question()`을 호출한다.

- 문제는 `readline` 위에 `readline`이 계속 호출되면서 콜백(?) 지옥에 빠진다는 것이다.

```bash
> 회원인가요?(yes)
> yes
> 아이디를 입력하세요yes
> yes
> yes
> |
```

- `readline`이 두 개 생기기 때문에 `test.init()` 메서드는 리턴값을 받지 못 한다.

```bash
> 회원인가요?(yes)
> 아이디를 입력하세요no
> 아이디를 입력하세요no
> 아이디를 입력하세요no
> 아이디를 입력하세요yes
> yes
> yes
> |
```

- 재귀로 호출한 경우에도 `readline`이 여러 개 생기기 때문에 `test.init()` 메서드는 리턴값을 받지 못 한다.

## 3. 해결

> Promise resolve 이용

- `Promise`에서 `resolve`를 하면 `Promise`가 종료되면서 `readline`도 종료되고 새로운 `Promise`와 `readline`을 호출한다.

- 따라서 `readline`은 하나로 유지된다.

- (실제로는 그런지 모르겠지만 일단은 이렇게 이해했다.)

```javascript
class TodoApp {

    init() {
        return new Promise(resolve => {
            inputReadline.question('회원인가요? (yes/no)', answer => {
                if (answer === 'no') {
                    resolve(this.register());
                } else if (answer === 'yes') {
                    resolve(this.login());
                }
            });
        });
    }

    register() {
        //..register work
    }

    login() {
        return new Promise(resolve => {
            inputReadline.question('아이디를 입력하세요', (id) => {
                console.log(id);
                return inputReadline.question('비밀번호를 입력하세요', (pw) => {
                    console.log(pw);
                    if(this.checkID_PW(id, pw)){
                        resolve(true);
                    }else {
                        this.errorLog('입력한 정보가 올바르지 않습니다.');
                        resolve(this.login());
                    };
                });
            });
        })
    }
    mainExecutor() {
        //...todo work
    }



}

const todoList = new TodoApp();

async function asyncTest() {
    await todoList.init();
    console.log('TODO APP에 오신 걸 환경합니다!');
    todoList.mainExecutor();
}
asyncTest();
```

- 위 코드를 보면 처음에 `init()` 메서드가 실행된다.

- 이 때 콘솔창에 `회원인가요? (yes/no)`라는 question이 뜬다.

- yes를 입력하면 로그인 메서드로, no를 입력하면 회원가입 메서드로 넘어간다. (간단한 테스트용으로 만든 코드이기 때문에 yes,no 이외이 입력값에 대한 에러 처리는 따로 하지 않았다.)

- `login()` 메서드에서 입력한 아이디,비밀번호 값이 올바르지 않으면 오류 메시지를 출력하면서 다시 `login()` 메서드를 실행한다.

- 이 때, `resolve`를 사용해서 기존의 `Promise`를 종료시키며 새로운 `Promise`를 호출한다.

- 따라서 `readline`은 중첩되지 않고 하나로 유지된다.

- 이와 같이, Promise를 이용해 `readline`을 재귀 호출하는 기능을 구현했다.

## 왜틀맞

- 사실 아직도 `Promise`가 어떤 원리로 동작하지는 잘 모르겠다.

- 현재는 `왜 틀렸는데 맞았다고 하지?` 의 느낌이다.

- 앞으로 `Promise`와 `Async & Await`에 대해서 더 공부하면서 내용을 보충하려고 한다.
