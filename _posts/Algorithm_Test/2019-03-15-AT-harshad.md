---
layout: post
title: Lv1 - 하샤드 수
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12947

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제

양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

#### 제한사항
- x는 1 이상, 10000 이하인 정수입니다.

#### 입출력 예

n | return
:---------:  | :-----------:
10 | true
12 | true
11 | false
13 | false

## 내 풀이
```python
def harshad(n):
    sum_digit = 0

    for i in str(n):
        sum_digit += int(i)

    if n % sum_digit == 0:
        return True
    else:
        return False
```


## 다른 사람 풀이
```python
def Harshad(n):
    # n은 하샤드 수 인가요?
    return n % sum([int(c) for c in str(n)]) == 0
```


## 느낀점
- `lambda()` 함수를 잘 이용하자
- 이론적으로 알고 있는 것과 실제로 사용하는 건 전혀 다르다.
- 이론을 설명하지 못 하면 아는게 아니듯
- 코드를 사용하지 못 한다면 모르는 것이다.