2019년 9월 10일

# OAuth 2.0

---

![](https://user-images.githubusercontent.com/34808501/62819063-ca92a580-bb8a-11e9-8fd8-cf91419a3a01.png)

## OAuth가 나오게 된 배경

My service에서 다른 서비스(Google,Facebook 등)을 사용하고 싶을 때가 있다. 다른 서비스를 사용하기 가장 간단한 방법은 사용자로부터 해당 서비스의 id, password를 입력받아 기억하고  있다가 사용하는 것이다. 하지만 이건 너무 위험하다. 다른 서비스의 아이디, 비밀번호를 전혀 다른 서비스에 공개한다는 건 매우 위험한 선택이다.

이러한 시나리오는 모두에게 있어 불만족스럽다.

- **User**: 처음 보는 서비스가 미덥지 않다.

- **My service**: 만약 문제가 생겼을 경우 지게 될 책임이 부담스럽다.

- **Their service**: 내 서비스의 사용자 정보가 다른 서비스에 노출 되는게 싫다.

#### 이러한 문제를 해결하기 위해 나온게 OAuth 이다.

## OAuth의 특징

- 실제 비밀번호 대신에 `AccessToken` 이라는 일종의 비밀키를 이용한다.

- `AccessToken`의 장점
    - 사용자의 실제 비밀번호가 아니다.
    - 서비스의 모든 기능이 아닌 일부 기능만 이용 가능한 토큰이다.

- OAuth는 다른 서비스로부터 `AccessToken`을 얻어내는 기술이다.
    - 이렇게 얻은 `AccessToken`을 이용해 해당 서비스의 일부 기능을 이용할 수 있는 것이 OAuth 서비스의 핵심이다.

## OAuth 인증 객체

다음 세 개의 객체가 서로 인증 과정을 거친다.

1. **User (Resource Owner)**

2. **My Service (Client)**

3. **Auth server / Resource server (ex. google, github, facebook etc)**

![](https://user-images.githubusercontent.com/34808501/62819079-12b1c800-bb8b-11e9-8996-9d831f793e57.png)

> 보통 Google, Facebook 같은 대규모 서비스는 인증 서버(Auth Server)를 따로 두는 경우가 많다.

## OAuth 인증을 위해 준비해야 할 것

OAuth 인증을 하고자 하는 서비스에서 아래 세 가지 요소를 등록해야 한다.

1. `Client ID`: public key 이다. 공개해도 된다.
2. `Client Secret`: secret key이다. 절대 공개하면 안 된다. 보통 환경변수에 담아 둔다
3. `Callback URL`: Client ID와 Client Secret을 확인한 후 redirect할 url 주소이다.

**위 세가지 요소가 모두 일치 했을 때 OAuth 인증이 성공한다.**

예를 들어, 깃헙으로 OAuth 로그인을 한다고 할 때, 깃헙에 등록된 `Client ID, Client Secret, Callback URL`과 **My Service**에 등록된 `Client ID, Client Secret, Callback URL`가 서로 일치해야한다. 하나라도 불일치하면 OAuth 로그인은 실패한다.

## OAuth 원리

### 전제

- Client가 Auth Server로부터 `Client ID, Client Secret, Callback URL`를 모두 등록/발급 받은 상태여야 한다.

### 1. Resource Owner의 승인

- **Resource Owner**가 **Auth Server**에게 승인 요청을 보낸다.
- **Auth Server**가 **Resource Owner**에게 `Authorization Code`를 보낸다.
- **Resource Owner**가 **Client**에게 `Authorization Code`를 보낸다.
- **Client**는 `Client ID, Client Secret, Callback URL, Authorization Code` 네 가지를 모두 갖고 있는 상태이다.

### 2. Auth Server의 승인

- 위 네 가지 정보를 **Auth Server**에 보낸다.
- **Resource Server**는 네 가지 정보가 모두 일치하는지 확인한다.
- 하나라도 불일치 할 경우 OAuth 인증은 실패한다.
- 모두 일치하면 `Access Token`을 발급한다.
    - `Authorization Code` 값은 더 이상 필요없기 때문에 삭제한다.

### 3. Access Token 발급

- 발급받은 `Access Token`을 통해서 **Resource Server**의 기능을 이용할 수 있다.

### 4. Refresh Token

- `Access Token`은 cookie처럼 만료 기한이 있다.
- 따라서 만료가 되면 재발급 받아야한다.
- 이 때 사용하는 게 `Refresh Token` 이다.
- 서비스마다 `Refresh Token`을 발급하지 않는 경우도 있고 쓰는 방식도 다르다.
- `Refresh Token`이 동작하는 대략적인 원리는 아래 그림과 같다.

![](https://user-images.githubusercontent.com/34808501/62819119-a97e8480-bb8b-11e9-8f2a-39b8c9385a3b.png)

> img source: [https://tools.ietf.org/html/rfc6749](https://tools.ietf.org/html/rfc6749)

---

### References

- [생활코딩 OAuth 2.0](https://opentutorials.org/course/3405/22004)

- https://tools.ietf.org/html/rfc6749