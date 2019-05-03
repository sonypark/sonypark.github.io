---
layout: post
title: 팰린드롬(palindrome) - 여러가지 풀이
category: Algorithm Test

tags: [알고리즘, algorithm, python, 파이썬]
comments: true
---
> 출처: [GreeksforGreeks](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)

## 정의
팰린드롬(palindrome)이란 앞으로 읽을 때와 거꾸로 읽을 때 똑같은 단어를 말한다.

### 다양한 풀이법

## Method #1
> list slice notation

1) Find reverse of string
2) Check if reverse and original are same or not.

```python
def reverse(s):
    return s[::-1]

def isPalindrome(s):
    rev = reverse(s)

    if(s == rev):
        return True
    else:
        return False
```

## Method #2
> Iterative Method

- 문자열의 첫 부분부터 문자열 길이의 절반 까지만 루프를 돌며 체크한다.
- 첫번째 문자와 마지막 문자, 두번째 문자와 마지막에서 두 번째 문자 ..
- 중간에 하나라도 같지 않으면 palindrome 이 아니다.

```python
def isPalindrome(str):

    for i in range(0, len(str)/2):
        if str[i] != str[len(str)-i-1]:
            return False
    return True
```

## Method #3
> ‘ ‘.join(reversed(string))
-  Method using inbuilt function to reverse a string

```python
def isPalindrome(s):

    rev = ''.join(reversed(s))

    if(s==rev):
        return True
    return False
```

## Method #4
> Method using one extra variable

```python
s = 'malayalam' # palindrome
w = ''
for i in s:
    w = i + w
    if (s == w):
        print('Yes')
```