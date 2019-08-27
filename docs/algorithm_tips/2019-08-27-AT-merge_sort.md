2019년 8월 27일

# Merge Sort (병할 정렬)

> 일단 반으로 최대한 나누고 나중에 합치며 정렬한다.

- Divide and Conquer(분할 정복)
    - 큰 문제를 잘게 쪼개서 해결한다.

- 시간복잡도가 항상 `NlogN` 이다.

## 분할(split)

![](https://static.javatpoint.com/tutorial/daa/images/daa-merge-sort.png)

- 먼저 위 그림처럼 더 이상 반으로 나눌 수 없을 때까지 분할한다.

## 병합 (merge)

![](https://static.javatpoint.com/tutorial/daa/images/daa-merge-sort2.png)

이미지 출처: https://www.javatpoint.com/daa-merge-sort

- 분할을 완료 했으면 병합(merge) 하면서 정렬한다.

- 정렬 할 때에는 왼쪽 배열과 오른쪽 배열의 값을 비교하면서 값이 작은 순서대로 상위 배열에 넣는다.

    - 예를 들어, 위의 그림에서 왼쪽 부분을 보자.

    - 왼쪽 배열 `[7]`과 오른쪽 배열 `[5]` 에서 왼쪽 원소(element)부터 차례로 크기를 비교한다.

        - 5가 7보다 더 작으므로 상위 배열에 5를 넣는다.
            - `[5]`
        - 왼쪽 배열의 남은 원소 7을 상위 배열에 넣는다.
            - `[5, 7]`
    - 마찬 가지로 왼쪽 배열 `[7]`과 오른쪽 배열 `[5]` 에서 왼쪽 원소(element)부터 차례로 크기를 비교해서 정렬하면 `[2, 4]`가 된다.

    - 그 다음 단계에서

    - 왼쪽 배열 `[5, 7]`과 오른쪽 배열 `[2, 4]` 에서 왼쪽 원소(element)부터 차례로 크기를 비교한다.
    
    1) 5와 2 중 2가 더 작으므로 상위 배열에 2를 넣는다.
        - 상위 배열: `[2]`
    2) 5와 4 중 4가 더 작으므로 상위 배열에 4를 넣는다.
        - 상위 배열: `[2, 4]`
    3) 오른쪽 배열의 원소는 모두 상위 배열에 들어가고 왼쪽 배열의 원소만 남았다.
    4) 왼쪽 배열은 이미 정렬 된 상태이므로 왼쪽 원소 부터 차례로 상위 배열에 넣는다.
        - 상위 배열: `[2, 4, 5, 7]`

    - 위와 같은 과정을 반복하면 최상위 배열은 모든 원소가 정렬된 상태가 된다.

```python
def merge(arr,L,R):
    i = j = k = 0

    while i < len(L) and j < len(R):
        if L[i] < R[j]:
            arr[k] = L[i]
            i += 1
        else:
            arr[k] = R[j]
            j += 1
        k += 1

    while i < len(L):
        arr[k] = L[i]
        i += 1
        k += 1

    while j < len(R):
        arr[k] = R[j]
        j += 1
        k += 1


def merge_sort(arr):

    if (len(arr) > 1):
        mid = len(arr) // 2
        L = arr[:mid]
        R = arr[mid:]

        # 분할 -- 쪼갤 수 없을 때까지 분할한다.
        merge_sort(L)
        merge_sort(R)

        # 정복 -- 합치면서 정렬
        merge(arr,L,R)

    return arr
```

### Reference

- https://www.geeksforgeeks.org/merge-sort/

- https://www.youtube.com/watch?v=TzeBrDU-JaY

- https://www.youtube.com/watch?v=ctkuGoJPmAE