---
layout: post
title: Lv1 - 시저 암호
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12926

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 AB는 1만큼 밀면 BC가 되고, 3만큼 밀면 DE가 됩니다. z는 1만큼 밀면 a가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.


#### 제한사항
- 공백은 아무리 밀어도 공백입니다.
- s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
- s의 길이는 8000이하입니다.
- n은 1 이상, 25이하인 자연수입니다.


#### 입출력 예

s | n | return
:---------:  | :---------:  | :-----------:
"AB" | 1 | "BC"
"z" | 1 | "a"
"a B z" | 4 | "e F d"

## 내 풀이
```python
def caesarCode(s, n):
    alpabet_lowerCase = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']
    alpabet_upperCase = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']

    answer = ""

    for w in s:
        if w == ' ':
            answer += ' '
        elif w in alpabet_lowerCase:
            next_w = alpabet_lowerCase[(alpabet_lowerCase.index(w)+n) % 26]
            answer += next_w
        else:
            next_w = alpabet_upperCase[(alpabet_upperCase.index(w)+n) % 26]
            answer += next_w

    return answer
```

## 다른 사람 풀이
```python
def caesar(s, n):
    lower_list = "abcdefghijklmnopqrstuvwxyz"
    upper_list = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

    result = []

    for i in s:
        if i is " ":
            result.append(" ")
        elif i.islower() is True:
            new_ = lower_list.find(i) + n
            result.append(lower_list[new_ % 26])
        else:
            new_ = upper_list.find(i) + n
            result.append(upper_list[new_ % 26])
    return "".join(result)
```

## 배운점
- `index()` 함수
- 리스트에서 특정 요소의 인덱스를 리턴한다.
- Syntax: `list.index(elmnt)`

```python
["foo", "bar", "baz"].index("bar")
=> 1
```