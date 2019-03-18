---
layout: post
title: Lv1 - 이상한 문자 만들기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12930

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.


#### 제한사항
- 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.


#### 입출력 예

s | return
:---------:  | :-----------:
"try hello world" |	"TrY HeLlO WoRlD"

## 내 풀이
```python
def lower_upper_case(s):
    # 전체 문자열을 소문자로 초기화
    s = s.lower().split(" ")
    new_s_list = []

    for w in s:
        for c in range(len(w)):
            # 단어의 특정 문자에 접근하기 위해 리스트로 변환
            w = list(w)
            # 짝수번째 문자를 대문자로 변환
            if c % 2 == 0:
                w[c] = w[c].upper()

        # 리스트로 분리한 문자를 하나로 다시 합쳐준다
        w = "".join(w)
        new_s_list.append(w)

    # 원래 문자열 형태로 합쳐준다.
    answer = " ".join(new_s_list)

    return answer
```

## 배운점
- `lower()`, `upper()` 함수
- 문자열을 `소문자`, `대문자`로 바꿔준다.

- `join()` 함수
- 반복가능한 객체(iterable object) 안에 있는 요소를 가져와 구분자를 기준으로 합쳐준다.
- Syntax: `separator.join(iterable)`

```python
myTuple = ("John", "Peter", "Vicky")
x = "#".join(myTuple)

print(x)
=> John#Peter#Vicky
```