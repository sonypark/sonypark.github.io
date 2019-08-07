2019년 8월 2일

# Codility  - BinaryGap (Iterations) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/1-iterations/binary_gap/

## 문제

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

def solution(N)

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..2,147,483,647].

Copyright 2009–2019 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

### 접근 방법

1. 파이썬 내장함수인 `bin`을 이용해서 입력값을 이진수로 바꾼다.

2. 0의 개수를 세는 `count` 변수와 개수를 담을 `length` 리스트를 선언 한다.

3. 0을 만나면 `count`에 +1를 한다.

4. 1을 만나면 `length` 리스트에 넣고 `count`를 초기화 한다.

5. `length` 리스트의 최댓값을 출력한다.

## 내 풀이

```python

def binaryGap(n):
    b = bin(n)[2:]
    count = 0
    length = []
    for i in b:
        if i =='1':
            length.append(count)
            count = 0
        if i =='0': count +=1
    return max(length)
```

## 느낀점

- 코딩 테스트를 Codility 에서 보는 회사(네이버, 야놀자 등)가 있어서 풀어 보았다.

- 사이트가 깔끔하게 구조화가 잘 되어있다.

- 그 동안 백준, 프로그래머스에서만 알고리즘 문제를 풀었는데 CodeSignal, Codilty 같은 외국 사이트도 좋은 것 같다.
