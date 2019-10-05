
2019년 10월 5일

# 백준 1003 - 피보나치 (DP) {docsify-ignore-all}

> 출처: https://www.acmicpc.net/problem/1003

## 문제

다음 소스는 N번째 피보나치 수를 구하는 C++ 함수이다.

```c++
int fibonacci(int n) {
    if (n == 0) {
        printf("0");
        return 0;
    } else if (n == 1) {
        printf("1");
        return 1;
    } else {
        return fibonacci(n‐1) + fibonacci(n‐2);
    }
}
```
fibonacci(3)을 호출하면 다음과 같은 일이 일어난다.

- fibonacci(3)은 fibonacci(2)와 fibonacci(1) (첫 번째 호출)을 호출한다.

- fibonacci(2)는 fibonacci(1) (두 번째 호출)과 fibonacci(0)을 호출한다.

- 두 번째 호출한 fibonacci(1)은 1을 출력하고 1을 리턴한다.

- fibonacci(0)은 0을 출력하고, 0을 리턴한다.

- fibonacci(2)는 fibonacci(1)과 fibonacci(0)의 결과를 얻고, 1을 리턴한다.

- 첫 번째 호출한 fibonacci(1)은 1을 출력하고, 1을 리턴한다.

- fibonacci(3)은 fibonacci(2)와 fibonacci(1)의 결과를 얻고, 2를 리턴한다.

1은 2번 출력되고, 0은 1번 출력된다. N이 주어졌을 때, fibonacci(N)을 호출했을 때, 0과 1이 각각 몇 번 출력되는지 구하는 프로그램을 작성하시오.

#### 입력

첫째 줄에 테스트 케이스의 개수 T가 주어진다.

각 테스트 케이스는 한 줄로 이루어져 있고, N이 주어진다. N은 40보다 작거나 같은 자연수 또는 0이다.

#### 출력

각 테스트 케이스마다 0이 출력되는 횟수와 1이 출력되는 횟수를 공백으로 구분해서 출력한다.

#### 예제 입력1

```
3
0
1
3
```

#### 예제 출력1

```
1 0
0 1
1 2
```

## 접근 방법

- 각 단계마다 0과 1이 출력되는 횟수를 배열에 담는다.
- 피보나치 수열의 성질에 의해 n번째 0과 1이 출력되는 횟수는 n-1, n-2 번째 0과 1이 출력되는 횟수의 합과 같다.

![](https://user-images.githubusercontent.com/34808501/66250241-04db8600-e77b-11e9-995a-ed926627da6a.png)


![](https://user-images.githubusercontent.com/34808501/66250242-06a54980-e77b-11e9-98a5-7d6823c2628f.png)

위와 같은 방법으로 dp에 단꼐별 0과 1이 출력되는 횟수를 담으면 다음과 같이 된다.

```
dp = [[1,0], [0,1], [1,2], [2,3], [3,5] ...]
```

## 내 풀이

```python
import sys
t = int(input())

dp = [[0,0] for _ in range(41)]
dp[0] = [1,0]
dp[1] = [0,1]

for i in range(2, len(dp)):
    dp[i][0] = dp[i-1][0] + dp[i-2][0]
    dp[i][1] = dp[i-1][1] + dp[i-2][1]


for _ in range(t):
    n = int(sys.stdin.readline())
    print(*dp[n])
```

## 느낀점
- 피보나치 수열은 익숙한 주제라 다른 DP 문제에 비해 쉽게 풀었다.
