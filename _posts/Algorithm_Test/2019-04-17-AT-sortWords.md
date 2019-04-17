---
layout: post
title: [백준] 단어 정렬
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬, 피보나치]
comments: true
---
> 출처: https://www.acmicpc.net/problem/1181

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.


## 문제
알파벳 소문자로 이루어진 N개의 단어가 들어오면 아래와 같은 조건에 따라 정렬하는 프로그램을 작성하시오.

- 길이가 짧은 것부터
- 길이가 같으면 사전 순으로

#### 입력

```javascript
13
but
i
wont
hesitate
no
more
no
more
it
cannot
wait
im
yours
```

#### 출력

```javascript
i
im
it
no
but
more
wait
wont
yours
cannot
hesitate
```

## 내 풀이

```angular2
sugar 가 5로 나누어 떨어지면
    - sugar 에서 5kg을 빼주고 pack_num 를 하나 추가한다.
그렇지 않으면
    - sugar 에서 3kg을 빼주고 pack_num 를 하나 추가한다.
이 과정을 sugar 가 0이 될 때 까지 반복한다
sugar 가 0 밑으로 떨어지면 -1을 출력한다.
```

```python
n = int(input())

arr = set()
for _ in range(n):
    arr.add(input())

print(arr)

# words 요소를 x 라고 했을 때 (x = words[i] ) len(x), x 순으로 정렬한다
for word in sorted(arr, key=lambda e: (len(e), e)):
    print(word)
```


## 배운점

- `sorted()`
- `key=` 에 정렬 옵션을 설정 할 수 있다.
- `sorted(arr, key=lambda e: len(e))` : 배열 arr의 각 요소(e)의 `길이(len)` 기준으로 정렬한다.
- `sorted(arr, key=lambda e: (len(e), e))` : 배열 arr의 각 요소(e)의 `길이(len)`와 `사전 순`으로 정렬한다.

## 느낀점
- 파이썬은 알고리즘을 풀기에 참 좋은 언어인 것 같다.
- 편리한 내장함수가 많다.


