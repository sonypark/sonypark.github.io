---
layout: post
title: Lv1 - 특정 날짜의 요일 구하기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12901

## 문제
2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 요일의 이름은 일요일부터 토요일까지 각각 `SUN,MON,TUE,WED,THU,FRI,SAT`
입니다. 예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 `TUE`를 반환하세요.

#### 제한사항
- n은 길이 10,000이하인 자연수입니다.

#### 입출력 예
- 2016년은 윤년입니다.
- 2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)

## 내 풀이
```python
import datetime

def getDayName(a,b):
    x = datetime.datetime(2016, a, b)
    return x.strftime("%a").upper()
```

## 다른 사람의 풀이
```python
def getDayName(a,b):
    months = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
    days = ['FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED', 'THU']
    return days[(sum(months[:a-1])+b-1)%7]
```

## 배운점
- datetime 모듈의 strftime 함수를 이용하면 특정 날짜를 원하는 `str`형태로 반환할 수 있다.
- ex) `%a` : `Weekday, short version`, `Wed` 
- ex) `%A` : `Weekday, full version`, `Wednesday` 
- ex) `%b` : `Month name, short version`, `Dec` 
- ex) `%B` : `Month name, full version`, `December` 
- ex) `%y` : `Year, short version, without century`, `18` 
- ex) `%Y` : `Year, full version`, `2018` 

## 느낀점
- 모듈을 이용하면 훨씬 빠르고 간단하게 풀 수 있다.
- 하지만 알고리즘 문제의 본래 취지와는 맞지 않을 수 있다. 이미 만들어진 모듈을 이용하는 것 보단 스스로 그 모듈을 만들어보길 원할 것이다.
- 따라서 두 가지 방법 모두 알고 있는 게 좋다.