2019년 5월 8일

# 팩토리얼

## 정의
> 출처: https://ko.wikipedia.org/wiki/%EA%B3%84%EC%8A%B9

- **1 부터 n 까지 모든 자연수의 곱**을 말한다.

### 다양한 풀이법

___

## Method #1

```python
def factorial(n):
    if n == 0:
        return 1
    fact = 1
    for i in range(1,n+1):
        fact = fact * i
    return fact
```

## Method #2

```python
def factorial_bottom_up(n):
    if n == 0:
        return 1
    bottom_up = [None]*(n+1)
    bottom_up[0] = 1
    bottom_up[1] = 1
    bottom_up[2] = 2
    for i in range(2,n+1):
        bottom_up[i] = i* bottom_up[i-1]
    return bottom_up[n]
```