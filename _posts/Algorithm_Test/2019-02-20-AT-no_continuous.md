---
layout: post
title: Lv1 - 리스트 내 연속하지 않는 수
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12906

## 문제
배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 
이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 
배열 arr에서 제거 되고 남은 수들을 return 하는 solution 함수를 완성해 주세요. 
단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다.


예를들면

- arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
- arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.
배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

#### 제한사항
- 배열 arr의 크기 : 1,000,000 이하의 자연수
- 배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수


#### 입출력 예
- [1,1,3,3,0,1,1]  => [1,3,0,1]
- [4,4,4,3,3]      => [4,3]

## 내 풀이
```python

def no_continuous(arr):

    answer = []

    for i in range(len(arr)-1):
        if arr[i] != arr[i+1]:
            answer.append(arr[i])

    # last_val_inArray
    if arr[-1] != arr[-2]:
        answer.append(arr[-1])
    else:
        answer.append(arr[-1])

    return answer
```

## 다른 사람의 풀이
```python
def no_continuous(arr):

    answer = []

    for i in arr:
        if answer[-1:] == [i]: continue
        answer.append(i)

    return answer
```

## 배운점
-  리스트를 슬라이싱 하면 리스트를 리턴한다.
-  빈 리스트를 슬라이싱해도 에러가 나지 않는다.
-  a = [] 처럼 리스트가 비어있을 때
-  `a[-1]` 하면 들어있는 element가 없기에 에러가 나지만 `a[-1:]` 하면 빈 리스트[]를 반환한다.

## 느낀점
- 리스트 슬라이싱을 잘 익혀두자