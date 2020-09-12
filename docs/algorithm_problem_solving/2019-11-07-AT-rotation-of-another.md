
2019년 11월 7일

# Udemy - Is One Array a Rotation of Another? (Array) {docsify-ignore-all}

> 출처: https://www.udemy.com/course/11-essential-coding-interview-questions/learn/quiz/378584#overview

## 문제

Write a function that returns True if one array is a rotation of another.

### Example

`[1, 2, 3, 4, 5, 6, 7]` is a rotation of `[4, 5, 6, 7, 1, 2, 3]`.

### 제한 사항

There are **no duplicates** in each of these arrays.

## 접근 방법

- 두 배열의 길이가 다르면 rotation이 안 되므로 False를 출력한다.

- 배열의 요소를 문자열로 만든다. `(s1, s2)`

- 그 중 하나의 문자열을 두 개로 이어 붙인다. `(s2s2)`

- `s1`이 `s2s2`에 포함되면 `rotation`이 되는 문자열이다.

## 내 풀이

```python
def is_rotation(list1, list2):
    if len(list1) != len(list2): return False
    s1 = ''.join(map(str, list1))
    s2 = ''.join(map(str, list2))
    s2 += s2
    if s1 in s2:
        return True
    return False
```
