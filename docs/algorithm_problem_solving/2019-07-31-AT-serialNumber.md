2019년 7월 31일

# 백준 1431 - 시리얼 번호 (정렬) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/1431

## 문제

다솜이는 기타를 많이 가지고 있다. 그리고 각각의 기타는 모두 다른 시리얼 번호를 가지고 있다. 다솜이는 기타를 빨리 찾아서 빨리 사람들에게 연주해주기 위해서 기타를 시리얼 번호 순서대로 정렬하고자 한다.

모든 시리얼 번호는 알파벳 대문자 (A-Z)와 숫자 (0-9)로 이루어져 있다.

시리얼번호 A가 시리얼번호 B의 앞에 오는 경우는 다음과 같다.

1. A와 B의 길이가 다르면, 짧은 것이 먼저 온다.
2. 만약 서로 길이가 같다면, A의 모든 자리수의 합과 B의 모든 자리수의 합을 비교해서 작은 합을 가지는 것이 먼저온다. (숫자인 것만 더한다)
3. 만약 1,2번 둘 조건으로도 비교할 수 없으면, 사전순으로 비교한다. 숫자가 알파벳보다 사전순으로 작다.

시리얼이 주어졌을 때, 정렬해서 출력하는 프로그램을 작성하시오.

#### 입력

첫째 줄에 기타의 개수 N이 주어진다. N은 1,000보다 작거나 같다. 둘째 줄부터 N개의 줄에 시리얼 번호가 하나씩 주어진다. 시리얼 번호의 길이는 최대 50이고, 알파벳 대문자 또는 숫자로만 이루어져 있다. 시리얼 번호는 중복되지 않는다.

#### 출력

첫째 줄부터 차례대로 N개의 줄에 한줄에 하나씩 시리얼 번호를 정렬한 결과를 출력한다.

#### 예제 입력

```
5
ABCD
145C
A
A910
Z321
```

#### 예제 출력

```
A
ABCD
Z321
145C
A910
```

### 접근 방법

cmp 함수를 만들어 문제 조건에 따라 정렬 우선 순위를 부여한다.

## 내 풀이

```python
import sys
n = int(input())
number = '0123456789'

def parse(s):
    num = []
    for i in s:
        if i in number:
            num.append(i)
    return sum(map(int, num))

def cmp(x):
    return len(x), parse(x), x

ll = [sys.stdin.readline().rstrip() for i in range(n)]
ll = sorted(ll, key= cmp)
for i in ll:
    print(i)
```

## 다른 사람 풀이

```python
n=int(input())
L=[]
for i in range(n):
    a=input()
    v=0
    for j in a:
        try:
            v+=int(j)
        except:
            pass
    L.append((len(a),v,a))
    print(L)
L.sort()
print(L)
for i in L:
    print(i[2])
```

## 배운점

- `isdigit()` 라는 내장 함수를 이용하면 해당 문자가 숫자인지 아닌지 알 수 있다.
    - 숫자면 `True`, 숫자가 아니면 `False`를 리턴한다.
    - [참고](https://www.programiz.com/python-programming/methods/string/isdigitㅍ)

- **튜플안에 담긴 순서**로 정렬된다는 사실을 몰랐다..!
    - 다른 사람의 풀이를 보며 알게되었다.
