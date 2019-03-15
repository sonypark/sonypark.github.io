---
layout: post
title: Lv1 - 행렬의 덧셈
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12950

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.


#### 제한사항
- 행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.


#### 입출력 예

arr1 | arr2 | return
:---------:  | :-----------: | :-----------:
[[1,2],[2,3]] |	[[3,4],[5,6]] |	[[4,6],[7,9]]
[[1],[2]] |	[[3],[4]] |	[[4],[6]]

## 내 풀이
```python
import numpy as np

def sum_matrix(arr1, arr2):

    m1 = np.matrix(arr1)
    m2 = np.matrix(arr2)
    answer = m1 + m2

    return answer.tolist()
```


## 다른 사람 풀이
```python
def sum_matrix(arr1, arr2):
    answer = [[c + d for c , d in list(zip(a , b))] for a , b in (zip(arr1, arr2)) ]
    return answer
```


## 느낀점
- `lambda()` 함수를 잘 이용하자
- 잘 이용하면 매우 유용한데 실전에서 사용하기 힘들다.
- 계속 연습하자.