2019년 5월 3일

# 펠린드롬(Palindrome)

> 출처: [GreeksforGreeks](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)

## 정의
**팰린드롬(palindrome)**이란 **앞으로 읽을 때와 거꾸로 읽을 때 똑같은 단어**를 말한다.

### 다양한 풀이법

---

## Method #1
> list slice notation

1) python 의 `list slice notation` 을 이용해 입력받은 **문자열을 역순으로 배치한다.**

2) **역순으로 배치한 문자열**과 **원래 문자열**을 **비교**해서 같은지 확인한다.

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
> Method using inbuilt function to reverse a string
>
> ‘ ‘.join(reversed(string))

- python **내장 함수**인 `reversed` 를 이용한다.
- 그 후 과정은 `Method #1` 과 동일

```python
def isPalindrome(s):

    rev = ''.join(reversed(s))

    if(s==rev):
        return True
    return False
```

## Method #3
> Iterative Method

- 문자열의 첫 부분부터 문자열 길이의 절반 까지만 **루프를 돌며 체크**한다.
- 첫번째 문자와 마지막 문자, 두번째 문자와 마지막에서 두 번째 문자 등..
- 중간에 하나라도 같지 않으면 palindrome 이 아니다.

```python
def isPalindrome(str):

    for i in range(0, len(str)/2):
        if str[i] != str[len(str)-i-1]:
            return False
    return True
```

## Method #4
> Method using one extra variable

1) **빈 문자열**을 선언한다.

2) 원래 문자열(string)에서 앞에서 하나씩 문자(char)를 가져와 빈문자열 앞에 붙인다.

3) 펠린드롬이라면 2) 과정을 완료했을 때 두 문자열이 서로 같게 된다.

```python
s = 'malayalam' # palindrome
w = ''
for i in s:
    w = i + w
    if (s == w):
        print('Yes')
```