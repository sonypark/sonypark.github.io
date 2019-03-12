---
layout: post
title: Lv1 - 제일 작은 수 제거하기
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12935

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 

예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.


#### 제한사항
- arr은 길이 1 이상인 배열입니다.
- 인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.

#### 입출력 예

arr | return
:---------:  | :-----------:
[4, 3, 2, 1] | [4, 3, 2]
[10] | [-1]


## 내 풀이
```python
def remove_min(arr):

    if len(arr) <2:
        return [-1]

    arr.remove(min(arr))
    return arr
```

## 배운점
- `remove()`
- 리스트에서 `remove()`는 해당 값(value)을 갖는 element를 삭제한다.
- cf) `pop()`은 해당 index의 값(value)을 삭제한다. 
