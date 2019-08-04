2019년 8월 4일

# Codility  - OddOccurrencesInArray (Array) {docsify-ignore-all}

> 출처: https://app.codility.com/programmers/lessons/2-arrays/odd_occurrences_in_array/

## 문제

A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9

- the elements at indexes 0 and 2 have value 9,
- the elements at indexes 1 and 3 have value 3,
- the elements at indexes 4 and 6 have value 9,
- the element at index 5 has value 7 and is unpaired.

Write a function:

`def solution(A)`

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9

the function should return 7, as explained in the example above.

Write an efficient algorithm for the following assumptions:

- N is an odd integer within the range [1..1,000,000];
- each element of array A is an integer within the range [1..1,000,000,000];
- all but one of the values in A occur an even number of times.


### 접근 방법


## 내 풀이

- 이건 왜 안되는 걸까..? 반례가 뭘까? 정답률이 66%이다..

```python
from collections import Counter

def OddOccurrencesInArray(A):
    a = Counter(A).most_common()
    return a[-1][0]
```

## 다른 사람 풀이

- XOR 연산자 특징 이용

```python
def OddOccurrencesInArray(A):
    result = 0
    for e in A:
        print(result, e)
        print(result ^ e)
        result = result ^ e
    return result
```

## 느낀점


