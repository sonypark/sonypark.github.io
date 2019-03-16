---
layout: post
title: Lv1 - 약수의 합
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12928?language=python3#

## 문제
자연수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.

#### 제한사항
- n은 0 이상 3000이하인 자연수입니다.

## 풀이
```python
def sum_divisor(n):
    sum = 0
    for i in range(1,n+1):
        if n%i == 0:
           sum += i
    return sum
```

## 더 효율적인 방법
```python
import math
def sum_divisor2(n):
    sum = 0
    mid = int(math.sqrt(n))

    for i in range(1, mid+1):
        if n % i == 0:
            if i*i == n: # i제곱이 n일 경우는 한 번만 더해줘야 한다. (ex. 25의 약수: 1, 5 ,25)
                sum += i
            else:
                sum += i + n/i
    return int(sum)

```

## 배운점
- 약수의 특성: n=a*b (단, a <= b) 
- 약수 a,b는 쌍으로 존재한다. 
- a,b는 반비례 관계이다.
- a의 최대값은 a == b 일 때 이다.
- 따라서 약수를 구할 때 a == b 일때 까지만 구하면 된다.(즉, n = a*a 가 되는 시점)

## 느낀점
- 쉬운 풀이와 효율적인 풀이가 있다. 보통 쉬운 풀이가 먼저 떠올라 그렇게 풀게 된다.
- 풀었다고 그냥 넘어가지 말고 좀 더 효율적인 풀이가 있는지 고민하자.