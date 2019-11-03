
2019년 11월 1일

# 프로그래머스 - 숫자 야구 (완전탐색) {docsify-ignore-all}


> 출처: https://programmers.co.kr/learn/courses/30/lessons/42842

## 문제



###  제한사항



## 입출력 예

| baseball                                             | return |
|------------------------------------------------------|--------|
| [[123, 1, 1], [356, 1, 0], [327, 2, 0], [489, 0, 1]] | 2      |

## 접근 방법

- 우선 **1~9로 만들 수 있는 세자리 수의 순열** 을 모두 구한다.
    - 경우의 수가 `9*8*7` 밖에 되지 않아서 성능에 큰 지장을 주지 않는다.

- 그 후 모든 경우의 수와 문제에서 주어진 수와 야구 게임을 진행한다.
    - 문제에서 주어진 숫자들의 strike, ball 조건을 만족하는 경우의 수만 남기고 리턴한다.
    - 기존 경우의 수 배열을 새로 리턴한 경우의 수 배열로 대체한다.
    - 이 과정을 반복한다.(즉, 조건에 일치하는 경우의 수만 남기는 과정을 반복한다.)

## 내 풀이

```python
from itertools import permutations


def baseball_game(n, s, b, cases):
    answer = []
    for c in cases:
        strike = 0
        ball = 0
        for i in range(3):
            for j in range(3):
                if i == j and c[i] == n[j]:
                    strike += 1
                elif i != j and c[i] == n[j]:
                    ball += 1
        if strike == s and ball == b:
            answer.append(c)
    return answer


def solution(baseball):
    numbers = ['1', '2', '3', '4', '5', '6', '7', '8', '9']
    cases = list(permutations(numbers, 3))

    for n, s, b in baseball:
        cases = baseball_game(str(n), s, b, cases)
    return len(cases)
```

## 느낀점
