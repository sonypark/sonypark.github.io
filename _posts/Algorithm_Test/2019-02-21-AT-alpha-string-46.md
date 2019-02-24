---
layout: post
title: Lv1 - 숫자로만 이루어진 문자열 판별 
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12918

## 문제
문자열 s의 길이가 4혹은 6이고, 숫자로만 구성되있는지 확인해주는 함수, solution을 완성하세요.
예를 들어 s가 a234이면 False를 리턴하고 1234라면 True를 리턴하면 됩니다. 

#### 제한사항
- s는 길이 1 이상, 길이 8 이하인 문자열입니다.

#### 입출력 예
- "a234"  => False
- "1234"  => True

## 내 풀이
```python
def alpha_string_46(str)->bool:

    if len(str) ==4 or len(str) ==6:
        try:
            if int(str):
                return True

        except: return False
    else:
        return False
```

## 다른 사람의 풀이
```python
def alpha_string46(str)->bool:
    return str.isdigit() and len(str) in (4,6)
```

## 배운점
- Python String isdigit() Method
- isdigit(): 모든 문자가 숫자인지 알려준다. 맞다면 True 아니면 False 리턴
- Syntax: string.isdigit()


## 느낀점
- 리스트 슬라이싱을 잘 익혀두자