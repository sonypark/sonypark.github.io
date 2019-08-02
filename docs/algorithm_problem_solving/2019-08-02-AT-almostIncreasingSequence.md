2019년 8월 2일

# CodeSignal  - 시리얼 번호 (정렬) {docsify-ignore-all}

> 출처: https://app.codesignal.com/arcade/intro/level-2/2mxbGwLzvkTCKAJMG

## 문제

Given a sequence of integers as an array, determine whether it is possible to obtain a strictly increasing sequence by removing no more than one element from the array.

Note: sequence a0, a1, ..., an is considered to be a strictly increasing if `a0 < a1 < ... < an`. Sequence containing only one element is also considered to be strictly increasing.

#### Example

For sequence = `[1, 3, 2, 1]`, the output should be
almostIncreasingSequence(sequence) = `false`.

There is no one element in this array that can be removed in order to get a strictly increasing sequence.

#### Input / Output

- [execution time limit] 4 seconds (py3)

- [input] array.integer sequence

    - Guaranteed constraints:
    `2 ≤ sequence.length ≤ 10**5,`
    `-10**5 ≤ sequence[i] ≤ 10**5.`

- [output] boolean

    - Return true if it is possible to remove one element from the array in order to get a strictly increasing sequence, otherwise return false.

### 접근 방법

1. strict increasing이 되기 위해서는`오름차순이 깨지는 지점` - `i` -이 **하나**여야 한다.

2. `i`가 0일 때는 strict increasing 이므로 `True`를 리턴한다.

3. `i`가 0이 아닐 때, 해당 'i`를 기준으로 앞 뒤 숫자를 하나씩 지운 후에 strict increasing 이 성립하는 지 확인한다.

4. 3번이 성립하면 `True`를 리턴하고 성립하지 않으면 `False`를 리턴한다.

## 내 풀이

> stackoverflow 에 올라온 내용을 참고했다.

```python
def first_bad_pair(sequence):
    for i in range(len(sequence)-1):
        if sequence[i] >= sequence[i+1]:
            return i
    return False

def almostIncreasingSequence(sequence):
    i = first_bad_pair(sequence)
    if(i is False): return True

    if first_bad_pair(sequence[i-1:i] + sequence[i+1:]) is False:
        return True
    if first_bad_pair(sequence[i:i+1] + sequence[i+2:]) is False:
        return True
    return False
```

## 다른 사람 풀이

- 자바스크립트로도 정말 깔끔하게 풀 수 있다. 리스펙!

```javascript
function almostIncreasingSequence(seq) {
  var bad=0
  for(var i=1;i<seq.length;i++) if(seq[i]<=seq[i-1]) {
    bad++
    if(bad>1) return false
    if(seq[i]<=seq[i-2]&&seq[i+1]<=seq[i-1]) return false
  }
  return true
}
```

## 느낀점

- 오늘부터 CodeSignal에서 문제를 풀기 시작했다. 구성이 게임 형식으로 되어있어서 재미있다!

- 이번 문제는 어려웠지만 꽤 좋은 문제라고 생각한다.
