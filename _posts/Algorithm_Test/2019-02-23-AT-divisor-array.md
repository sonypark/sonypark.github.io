---
layout: post
title: Lv1 - 나누어 떨어지는 숫자 배열
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12910

## 문제
array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.
divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.

#### 제한사항
- arr은 자연수를 담은 배열입니다.
- 정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.
- divisor는 자연수입니다.
- array는 길이 1 이상인 배열입니다.

#### 입출력 예
arr | divisor | return
--- | ------- | ------
[5,9,7,10] | 5 | [5,10]
[2,36,1,3] | 1 | [1,2,3,36]
[3,2,6]    | 10 | [-1]

## 내 풀이
```python
def divisor_array(arr, divisor):
    new_arr = []
    for element in arr:
        if(element % divisor ==0):
            new_arr.append(element)

    if len(new_arr) ==0:
        new_arr.append(-1)

    #오름차순 정렬
    new_arr.sort()

    return new_arr
```

## 배운점
- sort() 함수 : 배열을 오름차순 정렬해준다. (내림차순은 reverse())
- 마크다운에서 Table 만드는 법을 배웠다.