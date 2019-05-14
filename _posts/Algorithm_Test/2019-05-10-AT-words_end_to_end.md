---
layout: post
title: 2018 서머코딩 - 영어 끝말잇기**
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: https://programmers.co.kr/learn/courses/30/lessons/12981

## 문제
- 1부터 n까지 번호가 붙어있는 n명의 사람이 영어 끝말잇기를 하고 있습니다. 영어 끝말잇기는 다음과 같은 규칙으로 진행됩니다.

1. 1번부터 번호 순서대로 한 사람씩 차례대로 단어를 말합니다.
2. 마지막 사람이 단어를 말한 다음에는 다시 1번부터 시작합니다.
3. 앞사람이 말한 단어의 마지막 문자로 시작하는 단어를 말해야 합니다.
4. 이전에 등장했던 단어는 사용할 수 없습니다.
5. 한 글자인 단어는 인정되지 않습니다.

- 다음은 3명이 끝말잇기를 하는 상황을 나타냅니다.

`tank → kick → know → wheel → land → dream → mother → robot → tank`

- 위 끝말잇기는 다음과 같이 진행됩니다.

- 1번 사람이 자신의 첫 번째 차례에 tank를 말합니다.
- 2번 사람이 자신의 첫 번째 차례에 kick을 말합니다.
- 3번 사람이 자신의 첫 번째 차례에 know를 말합니다.
- 1번 사람이 자신의 두 번째 차례에 wheel을 말합니다.
- (계속 진행)


끝말잇기를 계속 진행해 나가다 보면, 3번 사람이 자신의 세 번째 차례에 말한 tank 라는 단어는 이전에 등장했던 단어이므로 탈락하게 됩니다.


사람의 수 n과 사람들이 순서대로 말한 단어 words 가 매개변수로 주어질 때, 가장 먼저 탈락하는 사람의 번호와 그 사람이 자신의 몇 번째 차례에 탈락하는지를 구해서 return 하도록 solution 함수를 완성해주세요.



#### 제한사항
- 끝말잇기에 참여하는 사람의 수 n은 2 이상 10 이하의 자연수입니다.
- words는 끝말잇기에 사용한 단어들이 순서대로 들어있는 배열이며, 길이는 n 이상 100 이하입니다.
- 단어의 길이는 2 이상 50 이하입니다.
- 모든 단어는 알파벳 소문자로만 이루어져 있습니다.
- 끝말잇기에 사용되는 단어의 뜻(의미)은 신경 쓰지 않으셔도 됩니다.
- 정답은 [ 번호, 차례 ] 형태로 return 해주세요.
- 만약 주어진 단어들로 탈락자가 생기지 않는다면, [0, 0]을 return 해주세요.


## 풀이
```python
def word_tag(n,words):
    past_list = []
    past_list.append(words[0])
    words.remove(words[0])
    count = 0
    WRONG = False
    for w in words:
        count +=1
        if w in past_list:
            WRONG = True
            break
        else:
            past_list.append(w)
            if(past_list[-2][-1] == past_list[-1][0]):
                pass
            else:
                WRONG = True
                break
    if WRONG:
        count_turn, num_of_person = divmod(count, n)
        count_turn +=1
        num_of_person +=1
        return [num_of_person, count_turn]
    else:
        return [0,0]
```

## 다른 사람 풀이

- list slice 를 이용해 한 줄에 끝냈다.
- 대단하다..

```python
def solution(n, words):
    for p in range(1, len(words)):
        if words[p][0] != words[p-1][-1] or words[p] in words[:p]: return [(p%n)+1, (p//n)+1]
    else:
        return [0,0]
```

## 배운점
- list slice 의 위력..

- `divmod(a,b)` : a 를 b로 나눈 몫과 나머지를 튜플 형태로 리턴한다.

```python
divmod(8, 3) =  (2, 2)
divmod(3, 8) =  (0, 3)
divmod(5, 5) =  (1, 0)
``` 


## 느낀점
- 개인적으로 이 문제는 어려웠다.
- 테스트 케이스 4개를 계속 통과 못해서 고생했다.
- 결국 https://codedrive.tistory.com/81 이 분의 풀이를 보고 풀었다.
- 이 문제는 사실 풀었다기 보단 답을 보고 구현한 거라 많이 아쉽다.
- 아직 알고리즘은 많이 부족한 것 같다. 그래도 포기하지 말고 꾸준히 풀어나가자.
