2019년 8월 27일

# Counting Sort (계수 정렬)

> 크기를 기준으로 갯수를 센다

- 시간복잡도는 `O(N)` 으로 굉장히 빠르다. -- Merge sort, Quick sort 보다 빠르다.

- 단, Counting sort를 사용하기 위해서는 다음과 같은 조건이 필요하다.

### 범위 조건이 있어야 한다. 

- **배열에 있는 원소**가 **특정 범위** 안에 있어야 한다.

    - ex) 0 이상의 자연수
    - ex) 알파벳

- **단점**

    - 배열의 원소 중 가장 큰 원소를 기준으로 count 배열을 만들기 때문에 가장 큰 원소가 너무 크면 그만큼 메모리 공간을 많이 낭비하게 된다. 그래서 counting sort는 이와 같은 조건이 맞는 경우에 한정적으로 쓰인다.

    - ex) [1,3,2,4,5,6,1,2,3,4,100000]
    - 위와 같은 배열이 있을 경우 최대 원소가 100000 이기 때문에 count 배열의 크기를 100000으로 해줘야 해서 불필요한 메모리 공간 낭비가 생기는 문제가 생긴다.

### Counting sort

- 정렬된 배열을 담을 새로운 배열(result)를 만들어 리턴하는 방법

- 단점: 메모리 공간이 더 필요하다.

```python
def counting_sort(array, maxval):

    m = maxval + 1
    count = [0] * m

    for a in array:
        count[a] += 1

    result = []
    for j in range(len(count)):
        if count[j] >0:
            for _ in range(count[j]):
                result.append(j)

    return result
```

### Counting sort

출처: https://www.geeksforgeeks.org/python-program-for-counting-sort/

- 기존 배열(array)에 정렬된 원소를 덮어쓴다.

- 장점: 메모리 공간을 새로 만들지 않아도 된다.

```python
def counting_sort(array, maxval):

    m = maxval + 1
    count = [0] * m               # init with zeros
    for a in array:
        count[a] += 1             # count occurences
    
    i = 0
    for a in range(m):            # emit
        for c in range(count[a]): # - emit 'count[a]' copies of 'a'
            array[i] = a
            i += 1

    return array
```

### Reference

- https://www.geeksforgeeks.org/python-program-for-counting-sort/

- https://www.youtube.com/watch?v=n4kbFRn2z9M