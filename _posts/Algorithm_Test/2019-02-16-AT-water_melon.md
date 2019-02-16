---
layout: post
title: Lv1 - 수박수박수..
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12919

## 문제
길이가 n이고, `수박수박수박수....`와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 예를들어 n이 4이면 `수박수박`을 리턴하고 3이라면 `수박수`를 리턴하면 됩니다.


#### 제한사항
- n은 길이 10,000이하인 자연수입니다.

#### 입출력 예
- n=3 => '수박수'
- n=4 => '수박수박'


## 내 풀이
```python
def water_melon(n)->str:

    string = ''

    for i in range(1, n+1):
        if i%2 != 0:
            string += '수'
        else:
            string += '박'
    return string
```

## 다른 사람의 풀이
```python
def water_melon(n)->str:
    string = '수박' * n
    return string[:n]
```

## 배운점
- 같은 문자를 반복하는 문제는 `곱하고 슬라이스` 하기 

## 느낀점
- 문자열, 리스트에서 slice 기능을 잘 활용하자