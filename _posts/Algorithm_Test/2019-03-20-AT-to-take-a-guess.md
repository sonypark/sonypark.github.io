---
layout: post
title: Lv1 - 모의고사
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12940

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.

## 문제
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.


1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...


1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.


#### 제한사항
- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

#### 입출력 예

answers | return
:---------:  | :-----------:
[1,2,3,4,5] | [1]
[1,3,2,4,2] | [1,2,3]

## 내 풀이
```python
def take_a_guess(answers):
    s1 = [1,2,3,4,5]
    s2 = [2,1,2,3,2,4,2,5]
    s3 = [3,3,1,1,2,2,4,4,5,5]

    s1_score = 0
    s2_score = 0
    s3_score = 0

    top_score_s = []

    for i in range(len(answers)):
        if s1[i % len(s1)] == answers[i]:
            s1_score += 1
        if s2[i % len(s2)] == answers[i]:
            s2_score += 1
        if s3[i % len(s3)] == answers[i]:
            s3_score += 1

    s_score_list = [s1_score, s2_score, s3_score]
    m = max(s_score_list)
    for i in range(len(s_score_list)):
        if (s_score_list[i] == m):
            if i == 0:
                top_score_s.append(1)
            if i == 1:
                top_score_s.append(2)
            if i == 2:
                top_score_s.append(3)
    return sorted(top_score_s)
```

## 다른 사람 풀이
```python
## enumerate 함수 사용
def solution(answers):
    pattern1 = [1,2,3,4,5]
    pattern2 = [2,1,2,3,2,4,2,5]
    pattern3 = [3,3,1,1,2,2,4,4,5,5]
    score = [0, 0, 0]
    result = []

    for idx, answer in enumerate(answers):
        if answer == pattern1[idx % len(pattern1)]:
            score[0] += 1
        if answer == pattern2[idx % len(pattern2)]:
            score[1] += 1
        if answer == pattern3[idx % len(pattern3)]:
            score[2] += 1

    for idx, s in enumerate(score):
        if s == max(score):
            result.append(idx + 1)

    return result
```
## 배운점
- `enumerate()` 함수 [출처](https://wikidocs.net/32)
- 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받아 인덱스 값을 포함하는 enumerate 객체를 리턴한다.

```python
for i, name in enumerate(['body', 'foo', 'bar']):
    print(i, name)
=>
0 body
1 foo
2 bar
```

## 느낀점
- enumerate 함수를 이용하면 훨씬 더 간단하게 만들 수 있다.
- 로직은 같지만 로직을 구현하는 법은 다른 사람의 풀이가 훨씬 더 간단명료하다.
- 변수 이름도 배울점이다.
- s1,s2,s3 보다 pattern1,pattern2,pattern3 가 더 직관적이다.
- 나는 student의 앞글자를 따서 s라고 했다. 하지만 문제에서 중요한것은 학생이 아니라 그 학생이 답을 찍는 패턴이다. 따라서 변수 이름도 패턴으로 해주는 게 더 바람직하다.