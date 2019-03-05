---
layout: post
title: Lv1 - 자릿수 더하기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12931

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.


#### 제한사항
- N의 범위 : 100,000,000 이하의 자연수


#### 입출력 예

N | return
:---------:  | :-----------:
123 | 6
987 | 24

## 내 풀이
```python
def sum_digit(n: int):
    num = 0
    for i in str(n):
        num += int(i)
    return num
```

## 다른 사람 풀이
```python
# 람다 함수 이용
def sum_digit(number):
    return sum([int(i) for i in str(number)])
```

```python
# 몫(//)과 나머지(%) 이용
def sum_digit(number):
    if number < 10:
        return number;
    return (number % 10) + sum_digit(number // 10)
```


## 배운점
#### `//` 연산자
-`//`을 이용하면 나누었을 때 몫을 구할 수 있다.
- `10//3 => 3`
- 참고: `%` 연산자는 나누었을 때 나머지를 구할 수 있다.
- `10%3 => 1`

## 느낀점
- 람다 함수를 잘 쓰자
