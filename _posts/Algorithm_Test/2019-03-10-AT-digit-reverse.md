---
layout: post
title: Lv1 - 자연수 뒤집어 배열로 만들기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12932

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 
예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.


#### 제한사항
- n은 10,000,000,000이하인 자연수입니다.


#### 입출력 예

n | return
:---------:  | :-----------:
12345 | [5,4,3,2,1]

## 내 풀이
```python
def digit_reverse(n):
    answer = []
    for i in reversed(str(n)):
        answer.append(int(i))
    return answer
```


## 다른 사람 풀
```python
def digit_reverse(n):
    return list(map(int, reversed(str(n))))
```


## 느낀점
- `map()` 함수를 잘 이용하자
- 이론적으로 알고 있는 것과 실제로 사용하는 건 전혀 다르다.
- 이론을 설명하지 못 하면 아는게 아니듯
- 코드를 사용하지 못 한다면 모르는 것이다.