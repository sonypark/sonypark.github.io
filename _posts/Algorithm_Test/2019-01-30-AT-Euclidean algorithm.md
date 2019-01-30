---
layout: post
title: 유클리드 호제법(Euclidean algorithm)
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: [위키피디아](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95#%EC%A0%95%EC%88%98%EC%9D%98_%EA%B2%BD%EC%9A%B0)

## 정의
2개의 자연수(또는 정식) a, b에 대해서 a를 b로 나눈 나머지를 r이라 하면(단, a>b), a와 b의 최대공약수는 b와 r의 최대공약수와 같다. 

#### 정리
- a를 b로 나눈 나머지 = r (a>=b, 0<=r<b)
- a,b의 최대공약를 (a,b)라고 하면 다음이 성립한다.
- (a,b) = (b,r)

```
(1071,1029) = (1029,42) = (42,21) = (21,0) = 21

1071 = 1029 * 1 + 42
1029 = 42 *24 + 21
42 = 21 * 2
```

