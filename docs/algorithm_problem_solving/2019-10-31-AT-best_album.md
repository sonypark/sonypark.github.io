
2019년 10월 31일

# 프로그래머스 - 베스트 앨범 (Hash) {docsify-ignore-all}

> 출처: https://programmers.co.kr/learn/courses/30/lessons/42579

## 문제

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

###  제한사항

- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.

## 입출력 예

| genres                                          | plays                      | return       |
|-------------------------------------------------|----------------------------|--------------|
| ['classic', 'pop', 'classic', 'classic', 'pop'] | [500, 600, 150, 800, 2500] | [4, 1, 3, 0] |

## 접근 방법

1. 딕셔너리를 만들어 장르를 key로 놓고 곡의 index와 횟수를 value로 넣는다. (idx, plays)
2. 문제 조건대로 장르별 재생횟수의 합을 구한 후 오름차순 한다.
3. 각 장르별 재생횟수 상위 2개의 idx를 answer 배열에 담아 출력한다.

## 내 풀이

```python
def cmp(x):
    return -x[1]


def solution(genres, plays):
    count = dict()
    d = dict()
    for i in range(len(genres)):
        if d.get(genres[i]) is None:
            d[genres[i]] = []
            d[genres[i]].append((i, plays[i]))
            count[genres[i]] = plays[i]
        else:
            d[genres[i]].append((i, plays[i]))
            count[genres[i]] += plays[i]
    tmp = []
    for k in sorted(count.items(), key=cmp):
        a = sorted(d.get(k[0]), key=cmp)[:2]
        tmp.append(a)
    answer = []
    for t in tmp:
        for v in t:
            answer.append(v[0])
    return answer
```

## 느낀점

- 이 문제는 구현하기가 까다로웠다. 천천히 고민한에 끝에 풀 수 있었다. 알고리즘 문제를 풀면서 매번 느끼는거지만 일단 어떻게 풀지 종이에 적고 시작하는게 가장 중요한 것 같다. 생각이 정리되지 않은채로 문제를 풀려고하다보면 시간만 버리는 경우가 많다.
