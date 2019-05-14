2019년 4월 15일

# 함수형 프로그래밍(Functional Programming)

## 함수형 프로그래밍은 원칙 

- 입출력이 순수해야한다. (**순수함수**)
    - 하나 이상의 인자(arguments)를 받고, 받은 인자만으로 결과물을 반환해야한다.

- 부작용(side effects)이 없어야한다.
    - 의도치 않게 부모 스코프의 변수를 변경하지 않아야한다.

- 함수와 데이터를 중점으로 생각한다.


## 대표적인 함수형 프로그래밍 함수 `map(), filter(), reduce()`

```javascript
const arr = [1, 2, 3, 4, 5];
const map = arr.map(function(x) {
  return x * 2;
}); // [2, 4, 6, 8, 10]
```

- 배열 `arr`을 변경하지 않고 새로운 결과(`map`)를 얻었다.
- 즉, 배열의 메소드인 `map()`은 순수함수이다. 


```javascript
const arr = [1, 2, 3, 4, 5];
const condition = function(x) { return x % 2 === 0; }
const ex = function(array) {
  return array.filter(condition);
};
ex(arr); // [2, 4]
```

- 위 `ex 함수`는 순수함수가 아니다.
- 인자로 받지 않은 변수 `condition`을 사용했기 때문이다.
- 순수함수로 바꿔주려면 아래와 같이 변경해야한다.

```javascript
const ex = function(array, cond) {
  return array.filter(cond);
};
ex(arr, condition);
```  

- `condition` 변수를 인자로 받아 처리함으로써 순수함수가 되었다.

- **순수함수**로 만들면 **쉽게 에러를 추적**할 수 있다.
    - **에러**가 발생 할 경우 다음 **둘 중 하나**이다.
    - **인자**에 문제가 있거나
    - **함수 내부**에 문제가 있거나


```javascript
function add(count){
  let sum = 0;
     for (let i = 1; i <= count; i++) {
        sum += i;
    }
}
```

- 위 함수는 1~10까지 더하는 함수이다.
- 이를 함수형으로 표현하면 다음과 같다.

```javascript
function add(sum, count) {
  sum += count;
  if (count > 0) {
    return add(sum, count - 1);
  } else {
    return sum;
  }
}
add(0, 10); // 55
```




## Reference

- [ZeroCho Blog: (JavaScript) 함수형 프로그래밍(Functional Programming)](https://www.zerocho.com/category/JavaScript/post/572c6f759a5f1c4db2481ee3)
