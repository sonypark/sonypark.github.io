---
layout: post
title: Lv1 - 정수 내림차순으로 배치하기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12933

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 

예를들어 n이 118372면 873211을 리턴하면 됩니다.

#### 제한사항
- n은 1이상 8000000000 이하인 자연수입니다.

#### 입출력 예

n | return
:---------:  | :-----------:
118372 | 873211


## 내 풀이
```python
def sort_desc(n):
    return int(''.join(sorted(str(n), reverse=True)))
```

## 배운점
- `''.join()`을 이용해 리스트 내 문자를 합칠 수 있다.
- 유용하므로 잘 기억해두자