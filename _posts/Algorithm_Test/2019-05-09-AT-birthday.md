---
layout: post
title: 백준 5635 - 생일 - sort(key=cmp)**
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---

> 출처: https://www.acmicpc.net/problem/5635

> 개인적으로 공부한 내용을 정리한 문서이므로 내용 상 오류가 있을 수 있습니다.
> 잘못된 내용이 있을 경우 댓글로 남겨주시면 감사하겠습니다.

## 문제
어떤 반에 있는 학생들의 생일이 주어졌을 때, 가장 나이가 어린 사람과 가장 많은 사람을 구하는 프로그램을 작성하시오.

#### 입력
- 첫째 줄에 반에 있는 학생의 수 n이 주어진다. (1 ≤ n ≤ 100)

- 다음 n개 줄에는 각 학생의 이름과 생일이 "이름 dd mm yyyy"와 같은 형식으로 주어진다. 이름은 그 학생의 이름이며, 최대 15글자로 이루어져 있다. dd mm yyyy는 생일 일, 월, 연도이다.

- 이름이 같거나, 생일이 같은 사람은 없다.

#### 출력

- 첫째 줄에 가장 나이가 어린 사람의 이름, 둘째 줄에 가장 나이가 많은 사람 이름을 출력한다.

#### 예제 입력

```python
5
Mickey 1 10 1991
Alice 30 12 1990
Tom 15 8 1993
Jerry 18 9 1990
Garfield 20 9 1990
```

#### 예제 출력

```python
Tom
Jerry
```

## 내 풀이 : sort(key=cmp) 이용

```python
import sys
import functools
n = int(sys.stdin.readline())

birthday = []
for i in range(n):
    name, d,m,y = sys.stdin.readline().split()
    birthday.append([name, int(d), int(m), int(y)])


def compareBirthDay(a, b):
    if a[3] == b[3]:
        if a[2] == b[2]:
            return a[1] - b[1]
        return a[2] - b[2]
    return a[3] - b[3]

birthday.sort(key=functools.cmp_to_key(compareBirthDay))
print(birthday[-1][0])
print(birthday[0][0])
```

## 다른 사람 풀이
- cmp 에서 요소를 비교할 때 우선순위를 `,`로 구분..!!

```python
def finde(x):
    return x[0],x[1],x[2]

test = int(input())
list = []
for i in range(test):
    a = input().split()
    list.append([int(a[3]), int(a[2]), int(a[1]), a[0]])
list = sorted(list, key = finde)
print(list[len(list)-1][3])
print(list[0][3])
```

## 다른 사람의 풀이를 보고 적용한 내 풀이

- `functools` 도 쓸 필요 없고 compare 함수의 코드도 한 줄로 줄었다.

```python
import sys
birthday = []
for i in range(n):
    name, d,m,y = sys.stdin.readline().split()
    birthday.append([name, int(d), int(m), int(y)])

def compareBirthDay(x):
    return x[3],x[2],x[1]

birthday.sort(key=compareBirthDay)
print(birthday[-1][0])
print(birthday[0][0])
```

## 배운점

- sort,sorted 의 `key` option 에 compare 함수를 넣어 정렬할 수 있다.

- 한 개의 요소를 기준으로 정렬

```python
birthday = [['Jerry', 18, 9, 1990], ['Garfield', 20, 9, 1990], ['Alice', 30, 12, 1990], ['Mickey', 1, 10, 1991], ['Tom', 15, 8, 1993]]

# 년도별 오름차순 정렬
sorted(birthday, key=lambda year: year[3])
birthday.sort(key = lambda year: year[3]) 
# => [['Jerry', 18, 9, 1990], ['Garfield', 20, 9, 1990], ['Alice', 30, 12, 1990], ['Mickey', 1, 10, 1991], ['Tom', 15, 8, 1993]] 
```

- 두 개 이상의 요소를 기준으로 정렬

```python
birthday = [['Jerry', 18, 9, 1990], ['Garfield', 20, 9, 1990], ['Alice', 30, 12, 1990], ['Mickey', 1, 10, 1991], ['Tom', 15, 8, 1993]]

def compareBirthDay(a, b):
    if a[3] == b[3]:
        if a[2] == b[2]:
            return a[1] - b[1]
        return a[2] - b[2]
    return a[3] - b[3]

# 년 월 일 순으로 오름차순 정렬
birthday.sort(key=functools.cmp_to_key(compareBirthDay))
# => [['Jerry', 18, 9, 1990], ['Garfield', 20, 9, 1990], ['Alice', 30, 12, 1990], ['Mickey', 1, 10, 1991], ['Tom', 15, 8, 1993]]
```

- `,`로 정렬 우선 순위 정해 줄 수 있음

```python
birthday = [['Jerry', 18, 9, 1990], ['Garfield', 20, 9, 1990], ['Alice', 30, 12, 1990], ['Mickey', 1, 10, 1991], ['Tom', 15, 8, 1993]]

def compareBirthDay(x):
    return x[3],x[2],x[1]

birthday.sort(key=compareBirthDay)
# => [['Jerry', 18, 9, 1990], ['Garfield', 20, 9, 1990], ['Alice', 30, 12, 1990], ['Mickey', 1, 10, 1991], ['Tom', 15, 8, 1993]]
```

## 느낀점
- 이 문제를 푸는 데 시간이 오래 걸렸다.
- 정답률이 높은 편이라 어려운 문제는 아닌거 같은데 개인적으로는 어려웠다.
- 그래도 이 문제를 통해 key 값을 기준으로 정렬하는 방법을 배울 수 있어서 참 좋았다.
- 다른 사람의 풀이를 보며 더 간단하고 좋은 방법을 배울 수 있었다. 이럴 때 기분이 참 좋다.
- 정렬 관련 문제가 나오면 오늘 배운 방식으로 굉자히 유용할 것 같다.





