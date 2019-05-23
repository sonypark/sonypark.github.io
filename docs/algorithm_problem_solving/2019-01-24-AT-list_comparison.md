2019년 1월 24일

# Lv1 - 완주하지 못한 선수 (Python) {docsify-ignore-all}

> 출처: https://programmers.co.kr/learn/courses/30/lessons/42576

## 문제
수 많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

#### 제한사항
- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

#### 예시

```python
participant= [mislav, stanko, mislav, ana]
completion= [stanko, ana, mislav]

=> mislav   # mislav는 동명이인, 완주자 명단에는 한 명밖에 없기 때문에 한 명은 완주하지 못함.
```

## 풀이
```python
def solution(participant, completion):
    # 이름을 오름차순으로 정렬
    participant.sort()
    completion.sort()

    # 동명이인 중에 완주 못한 사람 체크
    for p,c in zip(participant, completion):
        if p != c:
            return p

    # 동명이인이고 완주를 하지 못했으나 이름 상 제일 뒤에 있는 사람인 경우 체크
    # 예시) 정렬된 후의 변수가 
    # participant['a', 'b', 'b', 'z', 'z'], completion['a', 'b', 'b', 'z'] 인 경우
    return participant[-1]
```

## 다른 사람 풀이
```python
import collections

def solution(participant, completion):
    answer = collections.Counter(participant) - collections.Counter(completion)
    return list(answer.keys())[0]
```


## 배운점
- 다른 사람의 풀이를 보고 Counter 함수에 대해 알게 되었다.
- Counter 함수는 리스트 안의 객체를 key값으로 객체의 갯수를 value값으로 해서 컨테이너로 만들어준다.
- Counter 객체는 서로 더하기 빼기가 가능하다.

## 느낀점
- 처음으로 알고리즘 문제를 풀어봤다.
- 가장 쉬운 단계임에도 푸는데 시간이 꽤 걸렸다.
- 다른 사람의 문제풀이를 보며 많이 배웠다.
- 파이썬의 간결함에 놀랐다. (아는 만큼 보인다.)

