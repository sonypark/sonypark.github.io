2019년 8월 13일

# Codility  - GenomicRangeQuery  (Prefix Sums) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/

## 문제

A DNA sequence can be represented as a string consisting of the letters A, C, G and T, which correspond to the types of successive nucleotides in the sequence. Each nucleotide has an impact factor, which is an integer. Nucleotides of types A, C, G and T have impact factors of 1, 2, 3 and 4, respectively. You are going to answer several queries of the form: What is the minimal impact factor of nucleotides contained in a particular part of the given DNA sequence?

The DNA sequence is given as a non-empty string S = S[0]S[1]...S[N-1] consisting of N characters. There are M queries, which are given in non-empty arrays P and Q, each consisting of M integers. The K-th query (0 ≤ K < M) requires you to find the minimal impact factor of nucleotides contained in the DNA sequence between positions P[K] and Q[K] (inclusive).

For example, consider string S = CAGCCTA and arrays P, Q such that:

    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6

The answers to these M = 3 queries are as follows:

- The part of the DNA between positions 2 and 4 contains nucleotides G and C (twice), whose impact factors are 3 and 2 respectively, so the answer is 2.
- The part between positions 5 and 5 contains a single nucleotide T, whose impact factor is 4, so the answer is 4.
- The part between positions 0 and 6 (the whole string) contains all nucleotides, in particular nucleotide A whose impact factor is 1, so the answer is 1.
Write a function:

`def solution(S, P, Q)`

that, given a non-empty string S consisting of N characters and two non-empty arrays P and Q consisting of M integers, returns an array consisting of M integers specifying the consecutive answers to all queries.

Result array should be returned as an array of integers.

For example, given the string S = CAGCCTA and arrays P, Q such that:

    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6

the function should return the values [2, 4, 1], as explained above.

Write an efficient algorithm for the following assumptions:

- N is an integer within the range [1..100,000];
- M is an integer within the range [1..50,000];
- each element of arrays P, Q is an integer within the range [0..N − 1];
- P[K] ≤ Q[K], where 0 ≤ K < M;
- string S consists only of upper-case English letters A, C, G, T.

## 내 풀이1 (시간 초과)

> 시간복잡도 O(N^2)

- 정확도는 100%지만 시간복잡도가 높아 성능 검사를 통과하지 못 한다.

```python
def genomicRangeQuery(S,P,Q):
    nucleotide = [0]*len(S)

    for i in range(len(S)):
        if S[i] =='A': nucleotide[i] = 1
        elif S[i] =='C': nucleotide[i] = 2
        elif S[i] =='G': nucleotide[i] = 3
        else: nucleotide[i] = 4

    z = zip(P,Q)
    answer =[]
    for s,e in z:
        answer.append(min(nucleotide[s:e+1]))
    return answer
```

## 접근 방법

- 문자열 `S` 의 한 문자를 읽는 과정을 한 단계라고 할 때, 각 단계마다 `A,C,G,T`의 개수를 배열에 저장한다.

- `P,Q`의 범위에 있는 단계에서 `A,C,G,T`의 개수를 비교한 뒤, 개수에 변화가 있는 `A,C,G,T` 중 **minimal impact** 값을 결과(`result`)배열에 담는다.


## 내 풀이2

```python
def genomicRangeQuery(S,P,Q):
    nucleotide = {'A': 1, 'C': 2, 'G': 3, 'T': 4}

    curr_counts = [0, 0, 0, 0]
    counts = [curr_counts[:]]

    for s in S:
        curr_counts[nucleotide[s] - 1] += 1
        counts.append(curr_counts[:])

    result = []
    for i in range(len(P)):
        count_p = counts[P[i]]
        count_q = counts[Q[i]+1]

        if P[i] == Q[i]: result.append(nucleotide[S[P[i]]])
        elif count_p[0] < count_q[0]:
            result.append(1)
        elif count_p[1] < count_q[1]:
            result.append(2)
        elif count_p[2] < count_q[2]:
            result.append(3)
        elif count_p[3] < count_q[3]:
            result.append(4)
    return result
```

## 느낀점

- 어려운 문제였다. 시간복잡도를 줄이는 과정이 어려워서 stackoverflow 등을 참고해서 풀었다.
