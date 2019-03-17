---
layout: post
title: Lv1 - 예산 할당
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12982

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
S사에서는 각 부서에 필요한 물품을 지원해 주기 위해 부서별로 물품을 구매하는데 필요한 금액을 조사했습니다. 그러나, 전체 예산이 정해져 있기 때문에 모든 부서의 물품을 구매해 줄 수는 없습니다. 그래서 최대한 많은 부서의 물품을 구매해 줄 수 있도록 하려고 합니다.


물품을 구매해 줄 때는 각 부서가 신청한 금액만큼을 모두 지원해 줘야 합니다. 예를 들어 1,000원을 신청한 부서에는 정확히 1,000원을 지원해야 하며, 1,000원보다 적은 금액을 지원해 줄 수는 없습니다.


부서별로 신청한 금액이 들어있는 배열 d와 예산 budget이 매개변수로 주어질 때, 최대 몇 개의 부서에 물품을 지원해 줄 수 있는지 return 하도록 solution 함수를 완성해주세요.


#### 제한사항
- d는 부서별로 신청한 금액이 들어있는 배열이며, 길이(전체 부서의 개수)는 1 이상 100 이하입니다.
- d의 각 원소는 부서별로 신청한 금액을 나타내며, 부서별 신청 금액은 1 이상 100,000 이하의 자연수입니다.
- budget은 예산을 나타내며, 1 이상 10,000,000 이하의 자연수입니다.
- 물품을 구매해 줄 수 있는 부서 개수의 최댓값을 return 하세요.

#### 입출력 예

d | budget | return
:---------:  | :-----------: | :-----------:
[1,3,2,5,4] | 9 |	3
[2,2,3,3] |	10 | 4

## 내 풀이
```python
def allocate_budget(d, budget):
    sum_d = 0
    count_i = 0

    for i in sorted(d):
        sum_d += i
        count_i += 1
        if sum_d > budget:
            return count_i - 1
        elif sum_d == budget:
            return count_i
        elif count_i == len(d):
            return count_i
```


## 다른 사람 풀이
```python
def allocate_budget2(d, budget):
    sum_d = 0
    count_i = 0

    for i in sorted(d):
        if (sum_d+i) <= budget:
            sum_d += i
            count_i += 1
    return count_i
```

## 다른 사람 풀이2
```python
def allocate_budget3(d, budget):
    d.sort()
    while budget < sum(d):
        d.pop()
    return len(d)
```

## 느낀점
- 다른 사람의 풀이를 보며 내 풀이가 쓸데없이 길고 비효율적이라는 걸 느낀다.
- 어떻게 하면 더 효율적으로 코드를 짤 수 있을지 고민하자.
- 문제를 풀고 나서도 한 번 더 고민하자.
