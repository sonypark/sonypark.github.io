---
layout: post
title: Lv1 - 핸드폰 번호 가리기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12948

## 문제
프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 `*`으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

#### 제한사항
- s는 길이 4 이상, 20이하인 문자열입니다.

#### 입출력 예

phone_number | return 
:--------: | :---------:
"01033334444"    | "*******4444"
"027778888"    | "*****8888"

## 내 풀이
```python
def hide_numbers(phone_number):
    return phone_number.replace(phone_number[:-4] , '*' * len(phone_number[:-4]))
```

## 다른 사람 풀이
```python
def hide_numbers(s):
    return "*"*(len(s)-4) + s[-4:]
```