
2019년 11월 9일

# Udemy - One Away String (String) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/379168#overview

## 문제

Write a function that takes two strings and returns True if they are **one away** from each other.

They are **one away** from each other if a single operation (changing a character, deleting a character or adding a character) will change one of the strings to the other.

### Example

- "abcde" and "abcd" are one away (deleting a character).

- "a" and "a" are one away (changing the only character 'a' to the equivalent character 'a').

- "abc" and "bcc" are **NOT** one away. (They are two operations away.)

## 접근 방법

- **one away**: 문자열 원소 중 하나만 빼서 만들어야 한다.

    - 문자열의 길이가 2이상 차이 나면 one away 조건에 어긋나므로 False를 리턴한다.

- 나올 수 있는 경우의 수는 다음 두 가지이다.

    - 1. 문자열의 길이가 같은 경우

    - 2. 문자열이 다른 경우 (길이가 1 차이 나는 경우)

1. 문자열의 길이가 같은 경우

- 두 문자열에서 같은 원소가 두 개 이상일 경우 False, 그 외의 경우 True를 리턴한다.

2. 문자열이 다른 경우 (길이가 1 차이 나는 경우)

- 작은 문자열 길이만큼 순회하며 다른 원소가 나왔을 때 해당 원소를 긴 문자열에서 빼준다.
- 이 떄, 작은 문자열과 긴 문자열이 같다면 True 같지 않다면 False를 리턴한다.

## 내 풀이

```python
def is_one_away(s1, s2):
    if abs(len(s1) - len(s2)) > 1: return False

    if len(s1) == len(s2):
        count = 0
        for i in range(len(s1)):
            if s1[i] != s2[i]:
                count += 1
        if count > 1: return False
        return True

    if len(s1) > len(s2):
        longer_string = s1
        shorter_string = s2
    else:
        longer_string = s2
        shorter_string = s1

    for j in range(len(shorter_string)):
        if longer_string[j] != shorter_string[j]:
            longer_string = longer_string[:j] + longer_string[j + 1:]

            if longer_string == shorter_string:
                return True
            else:
                return False
    return True
```
