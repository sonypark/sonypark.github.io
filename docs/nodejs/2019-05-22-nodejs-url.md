2019년 4월 5일

# Built-in module: url

___

> 인터넷 주소를 쉽게 조작하도록 도와주는 모듈

## url 처리를 하는 두 가지 방법
  
1. `WHATWG 형식` (node version 7에서 추가된 형식)

2. `기존 노드 url 형식`

![WHATWG_node_url](./img/WHATWG_node_url.png)

- 가운데 `https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash`을 기준으로 

- 아래가 `WHATWG 형식`, 위에가 `기존 노드 url 형식`이다.

## 1. **WHATWG 형식**

- url 모듈 안에 있는 `URL 생성자`를 사용한다.

- `URL 생성자`에 주소를 넣어 객체를 만들면 주소가 부분별로 정리된다.

- WHATWG 형식에만 있는 속성: `username, password, origin, searchParams`

```javascript
const url = require('url');

const { URL } = url;
const myURL = new URL('http://www.gilbut.co.kr/book/bookList.aspx?sercate1=001001000#anchor');
console.log('new URL():', myURL);
console.log('url.format():', url.format(myURL));
```

- 위의 결과는 다음과 같다.

```javascript
/*
new URL(): URL {
  href:
   'http://www.gilbut.co.kr/book/bookList.aspx?sercate1=001001000#anchor',
  origin: 'http://www.gilbut.co.kr',
  protocol: 'http:',
  username: '',
  passwor`d`: '',
  host: 'www.gilbut.co.kr',
  hostname: 'www.gilbut.co.kr',
  port: '',
  pathname: '/book/bookList.aspx',
  search: '?sercate1=001001000',
  searchParams: URLSearchParams { 'sercate1' => '001001000' },
  hash: '#anchor' }
url.format(): http://www.gilbut.co.kr/book/bookList.aspx?sercate1=001001000#anchor
*/
```

## 2. **기존 노드 url 형식**

- `url.parse`에 주소를 넣으면 주소가 부분별로 정리된다.

```javascript
const url = require('url');

const parsedUrl = url.parse('http://www.gilbut.co.kr/book/bookList.aspx?sercate1=001001000#anchor');
console.log('url.parse():',parsedUrl);
console.log('url.format():', url.format(parsedUrl));
```

- 위의 결과는 다음과 같다.

```javascript
/*
url.parse(): Url {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: 'www.gilbut.co.kr',
  port: null,
  hostname: 'www.gilbut.co.kr',
  hash: '#anchor',
  search: '?sercate1=001001000',
  query: 'sercate1=001001000',
  pathname: '/book/bookList.aspx',
  path: '/book/bookList.aspx?sercate1=001001000',
  href:
   'http://www.gilbut.co.kr/book/bookList.aspx?sercate1=001001000#anchor' }
url.format(): http://www.gilbut.co.kr/book/bookList.aspx?sercate1=001001000#anchor
*/
```

- **WHATWG 형식**과 **기존 노드 url 형식** 비교
  
  - **WHATWG 형식**의 `username`과 `password`은 **노드 url 형식**의 `auth` 속성과 같다.
  
  - **WHATWG 형식**의 `searchParams`는 **노드 url 형식**의  `query` 속성과 같다.

## 참고) 노드 url 형식을 꼭 사용해야 하는 경우

- 주소가 host 부분 없이 `pathname` 부분만 오는 경우 (`book/bookList.apsx`)

- 위의 경우에는 **WHATWG 형식**으로 주소를 **처리 할 수 없다.**

## WHATWG 형식의 searchParams 객체

- `http://www.gilbut.co.kr/?page=3&limit=10&category=nodejs&category=javascript`

- 위의 주소에서 `?page=3&limit=10&category=nodejs&category=javascript` 부분이 `search` 이다.

- WHATWG 형식은 `search` 부분을 `searchParams` 라는 특수한 객체를 반환하므로 유용하다.

- `search` 부분은 보통 주소를 통해 **데이터**를 **전달** 할 때 사용한다.

- `search` 는 물음표(`?`)로 시작하며 `key = value` **형식**으로 **데이터**를 **전달**한다.

- `key`가 여러개인 경우 `&`로 구분한다.

## searchParams 객체에는  다양한 메서드가 있다

- 이러한 메서드를 이용해 `search` 부분을 조작한다.

```javascript
const { URL } = require('url');

const myURL = new URL('http://www.gilbut.co.kr/?page=3&limit=10&category=nodejs&category=javascript');

console.log('searchParams:', myURL.searchParams);
```



```javascript
/*
searchParams: URLSearchParams {
  'page' => '3',
  'limit' => '10',
  'category' => 'nodejs',
  'category' => 'javascript' }
*/
```

- `getAll(key)` : `key`에 해당하는 **모든 값**들을 가져온다.
  - 위 예제에서 `category`라는 `key`값에는 두 개의 `value`(`nodejs, javascript`)가 들어있다.

- `get(key)`: `key`에 해당하는 **첫 번째 값만** 가져온다.

- `has(key)`: 해당 `key`가 **있는지 검사**한다.

```javascript
console.log(`searchParams.getAll('category'):`, myURL.searchParams.getAll('category'));
console.log(`searchParams.get('limit'):`, myURL.searchParams.get('limit'));
console.log(`searchParams.has('page'):`, myURL.searchParams.has('page'));
```

```javascript
/*
searchParams.getAll('category'): [ 'nodejs', 'javascript' ]
searchParams.get('limit'): 10
searchParams.has('page'): true
*/
```

- `keys()`: `searchParams` 의 모든 `key` 를 `iterator` **객체로 가져온다.**

- `values()`:  `searchParams` 의 모든 `value` 를 `iterator` **객체로 가져온다.**

```javascript
console.log(`searchParams.keys():`, myURL.searchParams.keys());
console.log(`searchParams.values():`, myURL.searchParams.values());
```

```javascript
/*
searchParams.keys(): URLSearchParams Iterator { 'page', 'limit', 'category', 'category' }
searchParams.values(): URLSearchParams Iterator { '3', '10', 'nodejs', 'javascript' }
*/
```

- `append(key, value)` : 해당 `key` 를 추가한다. 같은 `key`가 있으면 **유지하고 하나 더 추가**한다.

````javascript
myURL.searchParams.append('filter', 'code');
myURL.searchParams.append('filter', 'squad');
console.log(`searchParams.getAll():`, myURL.searchParams.getAll('filter'));

// ssearchParams.getAll(): [ 'code', 'squad' ]
````

- `set(key, value)` : append 와 비슷하다. 다른점은 같은 `key` 값이 있으면 **모두 지우고 새로 추가**한다.


```javascript
myURL.searchParams.set('filter', 'code squad');
console.log(`searchParams.getAll():`, myURL.searchParams.getAll('filter'));

// searchParams.getAll(): [ 'code squad' ]
```

- `delete(key)` : 해당 `key` 를 **삭제**한다.

```javascript
myURL.searchParams.delete('filter');
console.log(`searchParams.getAll():`, myURL.searchParams.getAll('filter'));

// searchParams.getAll(): []
```

- `toString()` : `searchParams` 객체를 다시 **문자열로 합친다**. 이 문자열을 `search` 에 대입하면 주소 객체에 반영된다.

```javascript
console.log(`searchParams.toString():`, myURL.searchParams.toString());

// searchParams.toString(): page=3&limit=10&category=nodejs&category=javascript

myURL.search = myURL.searchParams.toString();
```

- WHATWG 형식의 `searchParams`가 기존 노드 url 형식의 `query` 보다 유용한 이유
  - `query` 는 `querystring` 모듈을 한 번 더 사용해야 하는 번거로움이 있다.

----

### Reference

- ![Node.js교과서](http://www.yes24.com/Product/goods/62597864)
