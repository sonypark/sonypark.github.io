
2019년 10월 27일

# codewars - Generic numeric template formatter {docsify-ignore-all}

> 출처: https://www.codewars.com/kata/55bf01e5a717a0d57e0000ec/solutions/python 

## 문제

Write a function, persistence, that takes in a positive parameter num and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.

For example:

```
persistence(39) => 3  # Because 3*9 = 27, 2*7 = 14, 1*4=4
                       # and 4 has only one digit.

persistence(999) => 4 # Because 9*9*9 = 729, 7*2*9 = 126,
                       # 1*2*6 = 12, and finally 1*2 = 2.

persistence(4) => 0   # Because 4 is already a one-digit number
```

```
persistence(39) # returns 3, because 3*9=27, 2*7=14, 1*4=4
                 # and 4 has only one digit

persistence(999) # returns 4, because 9*9*9=729, 7*2*9=126,
                  # 1*2*6=12, and finally 1*2=2

persistence(4) # returns 0, because 4 is already a one-digit number
```

## 접근 방법

- 각 자리수의 곱을 구한다.
    - 각 자리수를 곱할 때마다 count +1을 한다.

- 자리수가 한 자리가 될 때까지 반복한다.


## 내 풀이

```python
# 각 자리수의 곱을 구하는 함수
def mul(n):
    num = 1
    for i in range(len(n)):
        num *= int(n[i])
    return str(num)


def persistence(n):
    n = str(n)
    count = 0
    while len(n) > 1:
        n = mul(n)
        count += 1
    return count
```

## 다른 사람 풀이

> operator.mul, functools.reduce 모듈 이용

```python
import operator
from functools import reduce
def persistence(n):
    i = 0
    while n>=10:
        n= reduce(operator.mul,[int(x) for x in str(n)],1)
        i+=1
    return i
```

## 배운점

- `operator` 모듈에는 웬만한 연산자 함수가 다 구현되어 있다.
- `reduce`: 자바스크립트의 reduce와 같다. reduce를 사용하면 코드의 양을 많이 줄일 수 있다.
