2019년 4월 5일

# crypto

---

> 암호화를 도와주는 모듈

- ex) 고객의 비밀번호는 반드시 암호화 해야한다.

## 암호화 종류

1. 단방향 암호화

2. 양방향 암호화

## 1. 단방향 암호화

- 단방향 암호화는 복호화 할 수 없는 암호화를 말한다.

  - 즉, 한 번 암호화 하면 원래 문자열을 찾을 수 없다.

- 일반적으로 비밀번호를 암호화 할 때 사용한다.

- 비밀번호는 복호화 할 필요 없기 때문이다.


### 단방향 암호화 알고리즘으로는 주로 해시(hash) 기법을 사용한다.

- 해시(hash) 기법: 특정 문자열을 고정된 길이의 다른 문자열로 바꾸는 기법
- `비밀번호` 라는 문자열을 해시를 사용해 암호화 해보자.

```javascript
const crypto = require('crypto');

console.log('base64:', crypto.createHash('sha512').update('비밀번호').digest('base64'));
console.log('hex:', crypto.createHash('sha512').update('비밀번호').digest('hex'));
console.log('base64:', crypto.createHash('sha512').update('다른 비밀번호').digest('base64'));
```

- 위를 실행하면 다음과 같은 결과가 나온다.

```javascript
base64: dvfV6nyLRRt3NxKSlTHOkkEGgqW2HRtfu19Ou/psUXvwlebbXCboxIPmDYOFRIpqav2eUTBFuHaZri5x+usy1g==
  
hex: 76f7d5ea7c8b451b773712929531ce92410682a5b61d1b5fbb5f4ebbfa6c517bf095e6db5c26e8c483e60d8385448a6a6afd9e513045b87699ae2e71faeb32d6

base64: cx49cjC8ctKtMzwJGBY853itZeb6qxzXGvuUJkbWTGn5VXAFbAwXGEOxU2Qksoj+aM2GWPhc1O7mmkyohXMsQw==
```

- `createHash(알고리즘)` : 사용할 해시 알고리즘을 넣는다. `md5, dha1, sha256, sha512` 등
- `update(암호화 할 문자열)` : 암호화할 문자열을 넣는다.
- `digest(인코딩)` : 인코딩할 알고리즘을 넣는다. `base64, hex, latin1` 등
  - 이 중 결과 문자열이 짧은  `base64` 가 많이 사용된다

## 2. 양방향 암호화

- 암호화된 문자열을 복호화 할 수 있다.

```javascript
const crypto = require('crypto');

const cipher = crypto.createCipher('aes-256-cbc', '열쇠');
let result = cipher.update('암호화 할 문장', 'utf8', 'base64');
result += cipher.final('base64');
console.log('암호화:', result);

const decipher = crypto.createDecipher('aes-256-cbc', '열쇠');
let result2 = decipher.update(result, 'base64', 'utf8');
result2 += decipher.final('utf8');
console.log('복호화:', result2);
```

```javascript
/*
암호화: JwGZuUveVRTttFegg8CaU3Tyqf8A48G6aHcaH6PnVpE=
복호화: 암호화 할 문장
*/
```

----

### Reference

- ![Node.js교과서](http://www.yes24.com/Product/goods/62597864)