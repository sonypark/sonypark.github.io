2019년 8월 9일

# Passport 모듈을 이용한 로그인

---

> passport.initialize(), passport.session() 통해 passport를 미들웨어로 등록시킨다

### `express-session`

- req.session 객체를 생성한다.
- session을 설정하는 역할을 한다.

### `passport.initialize()`

- req 객체에 passport 설정을 심는다.

### `passport.session()` 

- req.session 객체에 passport 정보를 저장한다.

- 주의) express-session에 의해 req.session가 객체 생성되어야 passport 정보를 저장할 수 있다.

- 따라서 passport 미들웨어는 반드시 express-session 뒤에 선언해야 한다.

### `serializeUser()`

- **`sessionId`를 만드는 역할**

- 로그인 성공 시 실행된다.

- req.session 객체에 어떤 데이터를 저장할지 선택한다.  — 세션에 데이터를 저장해야 페이지 이동시에도 로그인 정보가 유지 된다.

- user 객체를 모두 저장하면 데이터 용량이 커지고 일관성 문제가 발생하므로 일반적으로 사용자 id만 저장한다.
    - 메모리는 최소한으로 써야하므로 최소 정보만 저장한다. (user객체가 아닌 `user.id` 만 저장) -- 이게 `sessionId` 가 된다.

### `deserializeUser()`

- **`sessionId`를 이용해서 `user 객체`를 가져오는 역할**

- 서버로 들어오는 매 요청(request)마다 호출된다.
- 매 호출마다 db를 읽어 `sessionId`에 해당하는`user 객체`를 가져온다.
- `req.user`에 `user 객체`를 저장한다. 따라서 req.user를 통해 로그인한 사용자 정보를 가져올 수 있다.


##### Passport 로그인에서는 아래 두 가지를 이해하는 게 가장 중요하다.

> `serializeUser`: 로그인 성공 시 사용자 정보 객체를 세션에 저장한다.

> `deserializeUser`: 세션에 저장한 아이디를 통해 데이터베이스에서 사용자 정보 객체를 불러온다.

### 전체 흐름

#### 로그인 이전

1. 로그인 요청이 들어온다.
2. `passport.authenticate` 메서드 호출
3. 로그인 전략 수행
4. 로그인 성공 시 사용자 정보 객체와 함께 `req.login` 호출
5. `req.login` 메서드가 `passport.serializeUser` 호출
6. `req.session`에 사용자 정보 저장 — 보통 id만 저장
7. 로그인 완료

#### 로그인 이후

1. 모든 요청에 `passport.session()` 미들웨어가 `passport.deserializeUser` 메서드 호출
2. `req.session`에 저장된 아이디로 데이터베이스에서 사용자 조회
3. 조회된 사용자 정보를 `req.user`에 저장
4. 라우터에서 `req.user` 객체 사용 가능

### 로그인 한 유저 인증

`isAuthenticated()`

- `isAuthenticated` 메서드를 호출하여 로그인 판단 여부를 확인할 수 있다.
- 로그인 된 유저의 경우 true를 로그인 되어있지 않은 경우는 false를 리턴한다.
- 로그인한 유저는 `next()`를 호출 해 다음 작업을 진행하게 된다.
- 로그인하지 않은 유저는 로그인 페이지로 리다이렉트 시켜 로그인을 유도할 수 있다.

```javascript
exports.isLoggedIn = (req, res, next) => {
    if (req.isAuthenticated()) {
        return next();
    } else {
        req.flash('error_msg', '로그인 후 이용해주세요.');
        res.redirect('/auth/signin');
    }
};
```

- 아래와 같이 사용하여 **로그인 한 유저만 게시글을 편집**하도록 하는 로직을 만들 수 있다.

```javascript
router.get('/edit/:id', isLoggedIn, asyncMiddleware(async (req, res) => {
    const article = await Article.findOne({
        _id: req.params.id
    });
    if (article) {
        res.render('articles/edit', {
            article: article
        });
    }
}));
```

#### 로그아웃

- 로그아웃은 아래와 같이 `req.logout()` 메서드를 이용해서 간단히 할 수 있다.
- 로그아웃은 로그인 된 유저만 할 수 있는 기능이므로 `isLoggedIn`를 사용했다.

```javascript
// 로그 아웃
router.get('/logout', isLoggedIn, (req, res) => {
    req.logout();
    req.flash('success_msg', 'You are logged out');
    res.redirect('/auth/signin');
});
```

### References

- https://github.com/expressjs/session

- [Yun Blog](https://cheese10yun.github.io/Passport-part1/)

- [ZeroCho 블로그](https://www.zerocho.com/category/NodeJS/post/57b7101ecfbef617003bf457)
