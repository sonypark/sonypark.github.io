---
layout: post
title: Lv1 - 문자열 내림차순 배
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12917

## 문제
문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.


#### 제한사항
- str은 길이 1 이상인 문자열입니다.


#### 입출력 예
s | return 
--- | -------
"Zbcdefg"    | "gfedcbZ"

## 내 풀이
```python
def sort_alphabet_reverse(str):
    st = ""
    s = sorted(str,reverse=True)
    for i in s:
        st += i
    return st
```

## 다른 사람 풀이
```python
# join 함수 이용
def solution(s):
    return ''.join(sorted(s, reverse=True))
```

```python
# 리스트로 변환 후 sort
def solution(s):
    answer = ''
    lst = list(s)
    lst.sort()
    lst.reverse()

    for i in lst:
        answer += i

    #return lst
    return answer
```

## 배운점
- join() 함수 : 문자열(string)에 element를 추가할 수 있다.
- `str +=` element. `str.join`(element) 모두 같은 결과 반환