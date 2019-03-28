---
layout: post
title: Lv2 - 숫자의 표
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 피보나치]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12924

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.


## 문제
Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.

- 1 + 2 + 3 + 4 + 5 = 15
- 4 + 5 + 6 = 15
- 7 + 8 = 15
- 15 = 15


자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.

#### 제한사항
- n은 10,000 이하의 자연수 입니다

#### 입출력 예

n | return
:---------:  | :-----------:
15 | 4


## 내 풀이
```python
def expressions(n):
    answer = 0
    for i in range(1, n+1):
        s = 0
        while s < n:
            s += i
            i += 1
        if s == n:
            answer += 1
    return answer
```

## 느낀점
- 잘 모르겠으면 처음부터 하나씩 넣어보며 해보자.
- 일단은 무작정 하나씩 해보고 그 다음에 효율적인 방법을 찾자.