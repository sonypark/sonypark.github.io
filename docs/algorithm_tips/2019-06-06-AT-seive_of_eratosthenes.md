2019년 6월 6일

# 에라토스테네스의 체(Sieve of Eratosthenes) {docsify-ignore-all}

> 개인적으로 공부한 과정을 정리해 놓은 글입니다. 내용 상 오류가 있을 수 있습니다. 잘못된 부분이 있을 경우 댓글에 남겨주시면 감사하겠습니다 :)

## 정의

- **에라토스테네스의 체(Sieve of Eratosthenes)** 는 일정 범위 안에 있는 모든 **소수**를 찾아내는 알고리즘이다.

- **소수** : 1과 자기 자신으로만 나누어지는 수 (1은 제외)


## 접근 방법

1. 숫자 2부터 시작해서 자신의 배수를 지워나간다.

2. 범위 내의 모든 수에 대해 위 과정을 반복한다.

3. 범위 내의 모든 수에 대해 위 과정이 끝나면 남은 숫자를 리턴한다.

- 이렇게 남은 숫자가 소수가 된다.

![](https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif)

이미지 출처: [Wikipedia](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

## Method 1

- 입력값을 받았을 때 소수인지 아닌지 판별하는 함수

```python
def isPrimeNum(n):
    if n == 1:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    m = int(n ** 0.5) + 1
    for i in range(3, m, 2):
        if n % i == 0:
            return False
    return True

# 입력값이 소수인지 아닌지 판별한다.
isPrimeNum(1) # False
isPrimeNum(2) # True
isPrimeNum(6) # False
isPrimeNum(13) # True
```

- 더 단순화 한 함수

```python
def isPrimeNumber(number):
    if number <= 1:
        return False
    else:
        for i in range(2, number // 2 + 1):
            if number % i == 0:
                return False
        return True
```


## Method 2

- 특정 범위에 있는 모든 소수를 구하는 함수

```python
def sieve(start, end):
    if end < 2:
        return []
    sieve_list = [False, False] + [True] * (end-1)
    for i in range(2, int(end**0.5)+1):
        if sieve_list[i]:
            sieve_list[i*2::i] = [False] * ((end-i)//i)
    return [i for i, v in enumerate(sieve_list) if v and i >= start]

# M,N 사이의 모든 소수를 리스트 형태로 반환한다.
prime_num_list = sieve(M, N)
```