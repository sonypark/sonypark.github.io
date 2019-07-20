2019년 7월 20일

# 백준 10825 - 국영수 (정렬) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/10825

## 문제

도현이네 반 학생 N명의 이름과 국어, 영어, 수학 점수가 주어진다. 이때, 다음과 같은 조건으로 학생의 성적을 정렬하는 프로그램을 작성하시오.

1. 국어 점수가 감소하는 순서로
2. 국어 점수가 같으면 영어 점수가 증가하는 순서로
3. 국어 점수와 영어 점수가 같으면 수학 점수가 감소하는 순서로
4. 모든 점수가 같으면 이름이 사전 순으로 증가하는 순서로 (단, 아스키 코드에서 대문자는 소문자보다 작으므로 사전순으로 앞에 온다.)

#### 입력

첫째 줄에 도현이네 반의 학생의 수 N (1 ≤ N ≤ 100,000)이 주어진다. 둘째 줄부터 한 줄에 하나씩 각 학생의 이름, 국어, 영어, 수학 점수가 공백으로 구분해 주어진다. 점수는 1보다 크거나 같고, 100보다 작거나 같은 자연수이다. 이름은 알파벳 대소문자로 이루어진 문자열이고, 길이는 10자리를 넘지 않는다.

#### 출력

문제에 나와있는 정렬 기준으로 정렬한 후 첫째 줄부터 N개의 줄에 걸쳐 각 학생의 이름을 출력한다.

#### 예제 입력1

```
12
Junkyu 50 60 100
Sangkeun 80 60 50
Sunyoung 80 70 100
Soong 50 60 90
Haebin 50 60 100
Kangsoo 60 80 100
Donghyuk 80 60 100
Sei 70 70 70
Wonseob 70 70 90
Sanghyun 70 70 80
nsj 80 80 80
Taewhan 50 60 90
```

#### 예제 출력1

```
Donghyuk
Sangkeun
Sunyoung
nsj
Wonseob
Sanghyun
Sei
Kangsoo
Haebin
Junkyu
Soong
Taewhan
```

## 내 풀이

```python
import sys
n = int(input())

a = [sys.stdin.readline().split() for _ in range(n)]

def cmp_score(x):return -int(x[1]), int(x[2]),-int(x[3])
def cmp_name(x): return x[0]

a.sort(key=cmp_name)
a.sort(key=cmp_score)

for i in a:
    print(i[0])
```

## 다른 사람 풀이

```python
from sys import stdin

n = int(stdin.readline().rstrip())
lst = []
for i in range(n):
    name, k, e, m = stdin.readline().split()
    lst.append((name, int(k), int(e), int(m)))

lst.sort(key=lambda item: item[0])
lst.sort(key=lambda item: item[3], reverse=True)
lst.sort(key=lambda item: item[2])
lst.sort(key=lambda item: item[1], reverse=True)

for item in lst:
    print(item[0])
```

## 배운점

#### 1. 파이썬 정렬은 **안정 정렬**이다.

- 따라서 기존의 순서가 보장된다.

> 참고: https://docs.python.org/3/howto/sorting.html

#### Sort Stability and Complex Sorts

> Sorts are guaranteed to be stable. That means that when multiple records have the same key, their original order is preserved.

```python
data = [('red', 1), ('blue', 1), ('red', 2), ('blue', 2)]
sorted(data, key=itemgetter(0))
>>> [('blue', 1), ('blue', 2), ('red', 1), ('red', 2)]
```

### 2. 정렬 우선순위가 높은 걸 마지막에 정렬한다.

- 문제에서 정렬 우선순위가 국,영,수,이름 이므로 우선순위가 높은 정렬을 마지막에 해준다.

```python
lst.sort(key=lambda item: item[0]) // 이름
lst.sort(key=lambda item: item[3], reverse=True) // 수학
lst.sort(key=lambda item: item[2]) // 영어
lst.sort(key=lambda item: item[1], reverse=True) // 국어
```

- 국어와 수학은 `내림차순` 정렬을 하라고 했으므로 `reverse` 옵션을 붙여준다.
