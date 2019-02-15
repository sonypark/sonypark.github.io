---
layout: post
title: Lv1 - 서울에서 김서방 찾
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12919

## 문제
String형 배열 seoul의 element중 Kim의 위치 x를 찾아, 김서방은 x에 있다는 String을 반환하는 함수, solution을 완성하세요. seoul에 Kim은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.


#### 제한사항
- seoul은 길이 1 이상, 1000 이하인 배열입니다.
- seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다.
- Kim은 반드시 seoul 안에 포함되어 있습니다.

#### 입출력 예
- seoul = ['Jane', 'Kim']
- return = '김서방은 1에 있다'


## 내 풀이
```python
def findKiminSeoul(Seoul)->str:

   for i, name in enumerate(Seoul):
        if name == 'Kim':
            return '김서방은 %d에 있다' % i
```

## 다른 사람의 풀이
```python
def findKiminSeoul2(Seoul)->str:
    return '김서방은 {}에 있다'.format(Seoul.index('Kim'))
```

## 배운점
- list 내장 함수: index 함수

## 느낀점
- list에 index 함수가 있는 걸 처음 알았다..^^