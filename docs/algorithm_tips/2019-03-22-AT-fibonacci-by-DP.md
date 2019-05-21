2019년 3월 22일

# 피보나치 수열 알고리즘

> 출처: https://www.youtube.com/watch?v=vYquumk4nWw&list=PLBZBJbE_rGRU5PrgZ9NBHJwcaZsNpf8yD

## 1. Recursion

- 재귀
- 시간복잡도: O(2**n)

```python
def fibo_1(n):
    if n ==1 or n == 2:
        return 1
    else:
        return fibo_1(n-1) + fibo_1(n-2)
```

## 2. Memorized solution 

- memo[] 이용
- 시간복잡도: O(2N+1) = O(N)
- But 위에서부터 거꾸로 올라가서 값을 찾기 때문에 bottom_up 보다 시간이 오래 걸린다
- N이 커지면 **recursion depth error**가 발생한다. `maximum recursion depth exceeded in comparison`

```python
def fibo_2(n, memo):
    if memo[n] is not None:
        return memo[n]
    if n == 1 or n == 2:
        return 1
    else:
        memo[n] = fibo_2(n-1, memo) + fibo_2(n-2, memo)
        return memo[n]

def fibo_memo(n):
    memo = [None] * (n + 1)
    return fibo_2(n, memo)
```


## 3. Bottom-up approach

- bottom_up
- 시간복잡도: O(N)

```python
def fibo_3(n):
    if n == 1 or n == 2:
        return 1
    bottom_up = [None] * (n + 1)
    bottom_up[1] = 1
    bottom_up[2] = 1
    for i in range(3, n+1):
        bottom_up[i] = bottom_up[i-1] + bottom_up[i-2]
    return bottom_up[n]
```

```python
def fibo_3(n):
    a = 0
    b = 1
    for i in range(n):
    a, b = a+b, a
    return a
```