
2019년 11월 8일

# Udemy - Non-Repeating Character (String) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/380026#overview

## 문제

Implement a function that takes a string and returns the first character that does not appear twice or more.

### Example

- `"abacc" -> 'b'` ('a' appears twice, and so does 'c')

- `"xxyzx" -> 'y'` ('y' and 'z' are non-repeating characters, and 'y' appears first)

### 제한 사항

If there is no non-repeating character, return None.

## 접근 방법

- 딕셔너리를 만들어 key에는 문자열 원소를 value에는 해당 문자열이 나온 횟수를 담는다.

- value가 1인 원소를 출력한다.

## 내 풀이

```python
def non_repeating(given_string):
    is_exist = dict()

    for s in given_string:
        if s not in is_exist:
            is_exist[s] = 1
        else:
            is_exist[s] += 1

    for s1 in given_string:
        if is_exist[s1] == 1:
            return s1
    return None
```
