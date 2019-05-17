2019년 1월 30일

# 유클리드 호제법

> 출처: [위키피디아](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95#%EC%A0%95%EC%88%98%EC%9D%98_%EA%B2%BD%EC%9A%B0)

## 정의
- 2개의 자연수 a, b에 대해서 a를 b로 나눈 나머지를 r 이라 하자 (단, a>b) 
- 이 때 a와 b의 최대공약수는 b와 r의 최대공약수와 같다. 

#### 정리
- a를 b로 나눈 나머지 = r (a >= b, 0 <= r < b)
- a,b의 최대공약수를 (a,b)라고 하면 다음이 성립한다.
- (a,b) = (b,r)

```
1071과 1029의 최대공약수를 구하면,

1071은 1029로 나누어 떨어지지 않기 때문에, 1071을 1029로 나눈 나머지를 구한다. ≫ 42
1029는 42로 나누어 떨어지지 않기 때문에, 1029를 42로 나눈 나머지를 구한다. ≫ 21
42는 21로 나누어 떨어진다.

따라서, 최대공약수는 21이다.
```

상기한 1071과 1029에 대한 예시를 위와 같은 표현으로 적어보면
```
(1071,1029) = (1029,42) = (42,21) = (21,0) = 21

1071 = 1029 * 1 + 42
1029 = 42 *24 + 21
42 = 21 * 2
```
처럼 쓸 수 있다.

