---
layout: post
title: Lv2_JadenCase 문자열 만들기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 최소공배수]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12951

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.


## 문제
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

#### 제한사항
- s는 길이 1 이상인 문자열입니다.
- s는 알파벳과 공백문자(" ")로 이루어져 있습니다.
- 첫 문자가 영문이 아닐때에는 이어지는 영문은 소문자로 씁니다. ( 첫번째 입출력 예 참고 )

#### 입출력 예

arr | result
:---------:  | :-----------:
'3people unFollowed me' |	'3people Unfollowed Me'
'for the last week'	| 'For The Last Week'


## 내 풀이
```python
def jadenCase(s):
    s = s.lower().split(' ')
    answer = []
    for i in s:
        answer.append(i.capitalize())
    return ' '.join(answer)

// test code
// s = '3people unFollowed me'
// s2 = 'for the last week'
// s3 = 'i\'m a small CAT'
```

## 다른 사람 풀이

```python
# title 함수 사용
def Jaden_Case(s):
    return s.title()
```

```python
def Jaden_Case(s):
    answer = []
    for i in range(len(s.split())):
        print(s.split()[i][0])
        answer.append(s.split()[i][0].upper() + s.split()[i].lower()[1:])
    return " ".join(answer)
```


## 배운점

- `capitalize()` : 문자열의 첫 문자를 대문자로 바꿔준다.
```python
name = "geeks for geeks"
  
print(name.capitalize()) 
# Output: Geeks for geeks
```

- `title()`: 문자열 내 각 단어의 첫문자만 대문자로 바꾸고 나머지는 소문자로 바꿔준다.

```python
str1 = 'geeKs foR geEks'
str2 = str1.title() 
print(str2) 

# Output: Geeks For Geeks
```

## 느낀점

- 파이썬에는 편리한 내장함수가 많다.
  