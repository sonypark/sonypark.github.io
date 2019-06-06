2019년 6월 6일

# 백준 1929 - 소수 구하기 (seive) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/1929

## 문제

M이상 N이하의 소수를 모두 출력하는 프로그램을 작성하시오.

#### 입력

첫째 줄에 자연수 M과 N이 빈 칸을 사이에 두고 주어진다. (1 ≤ M ≤ N ≤ 1,000,000)

#### 출력

한 줄에 하나씩, 증가하는 순서대로 소수를 출력한다.

#### 예제 입력

```
3 16
```

#### 예제 출력

```
3
5
7
11
13
```

## 접근 방법

- 올바른 괄호(VPS)가 되기 위해서는 아래 두 조건이 성립해야 한다.

1. 소수 판별 함수를 만든다.

2. M,N 사이에 for 문을 돌면서 소수인 수만 출력한다.

## 내 풀이

> 소요 시간: 2112 ms

```python
import sys

m, n = map(int, sys.stdin.readline().split())


def primNum(n):
    if n == 1:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    N = int(n ** 0.5) + 1
    for i in range(3, N, 2):
        if n % i == 0:
            return False
    return True


for j in range(m, n + 1):
    if (primNum(j)):
        print(j)
```

## 다른 사람 풀이 : 에라토스테네스의 체

> 소요 시간: 168 ms

```python
import sys

def sieve(start, end):
    if end < 2:
        return []
    sieve_list = [False, False] + [True] * (end-1)
    for i in range(2, int(end**0.5)+1):
        if sieve_list[i]:
            sieve_list[i*2::i] = [False] * ((end-i)//i)
    return [i for i, v in enumerate(sieve_list) if v and i >= start]


M, N = map(int, sys.stdin.readline().split())

prime_num_list = sieve(M, N)

for p in prime_num_list:
    print(p)
```

## 배운점

- 에라토스테네스의 체(sieve of eratosthenes)를 이해했다.

## 느낀점

- 내 풀이도 에라토스테네스의 체를 이용한 것이긴 하지만 다른 사람 풀이와 비교했을 때 10배이상 비효율적이었다.

- 내 풀이는 입력값이 소수 인지 아닌지 판별하는 문제에는 적절하다.

- 하지만 일정 범위에 있는 소수의 리스트를 출력하는 데에는 비효율적이다. 숫자마다 매번 함수를 호출해야되기 때문이다.

- 따라서 소수의 리스트를 출력하는 문제에서는 다른 사람의 풀이 처럼 풀도록 하자.