
2019년 11월 6일

# Udemy - Common Elements in Two Sorted Arrays (Array) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/378244#overview

## 문제

Write a function that returns the common elements (as an array) between two sorted arrays of integers (ascending order).

### Example

The common elements between `[1, 3, 4, 6, 7, 9]` and `[1, 2, 4, 5, 9, 10]` are `[1, 4, 9]`.

### 접근 방법

- 첫 번째 배열을 set에 담는다.

- 두 번째 배열을 순회하면서 첫 번째 배열에 있는 요소인지 확인한다.

- 첫 번째 배열에 있는 요소일 경우 공통 요소 이므로 answer 배열에 담아 출력한다.

## 내 풀이

```python
def common_elements(list1, list2):
    list1 = set(list1)
    answer = []
    for number in list2:
        if number in list1:
            answer.append(number)
    return answer
```
