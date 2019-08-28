2019년 8월 27일

# Quick Sort (퀵 정렬)

> pivot을 기준으로 좌우 정렬을 반복한다.

- 평균 시간복잡도는 `NlogN` 이다.

- 하지만 최악의 경우 시간복잡도가 `N^2`이다.

    - **이미 정렬된 배열**에서 **처음 또는 마지막 수를 pivot**으로 하고 정렬할 때 `N^2`이 된다.

## pivot 기준으로 좌우 분할(partition)

![](https://www.geeksforgeeks.org/wp-content/uploads/gq/2014/01/QuickSort2.png)

이미지 출처: https://www.geeksforgeeks.org/quick-sort/

##### 1. partition이 한 번 끝날 때마다 pivot의 위치가 정해진다.

##### 2. pivot 기준으로 왼쪽은 pivot 보다 작은 값들이 오른쪽은 pivot보다 큰 값이 배치된다.

##### 3. 정해진 pivot 위치를 기준으로 좌우를 똑같이 quick_sort 해준다.


### partition 동작 원리

> L: 배열의 첫 번째 원소 위치
> R: 배열의 마지막 원소 위치 -- 이 예제에서는 pivot을 R 로한다.
> i: pivot 보다 작은 원소(element)의 갯수

![](https://user-images.githubusercontent.com/34808501/63828278-e080d280-c9a0-11e9-93ef-9c632b8919ef.png)

- L을 한 칸씩 옆으로 이동하며 `pivot` 보다 크면 넘어가고 `pivot` 보다 작으면 `(i+1)`번째 원소와 `swap` 한다.

![](https://user-images.githubusercontent.com/34808501/63827740-3ce2f280-c99f-11e9-9d77-7d62afad98ba.png)

- `70`은 `pivot` 보다 크므로 넘어가고
- `20`은 `pivot` 보다 작으므로 `(i+1)`번째 원소인 `70`과 `swap` 한다.

![](https://user-images.githubusercontent.com/34808501/63827741-3ce2f280-c99f-11e9-8690-bb5d2f029670.png)

- `50,80`은 `pivot` 보다 크므로 넘어간다.

![](https://user-images.githubusercontent.com/34808501/63827742-3ce2f280-c99f-11e9-9da9-36d1af6453f4.png)

- `30`은 `pivot` 보다 작으므로 `(i+1)`번째 원소인 `70`과 `swap` 한다.

![](https://user-images.githubusercontent.com/34808501/63827744-3d7b8900-c99f-11e9-81a5-4b405fe0ea65.png)

![](https://user-images.githubusercontent.com/34808501/63827745-3d7b8900-c99f-11e9-9ebe-2222d968cb89.png)

![](https://user-images.githubusercontent.com/34808501/63827746-3d7b8900-c99f-11e9-9381-ef8ecf8e7c39.png)

- `L`이 `R` 이전까지 모두 돌았으므로
- `pivot` 위치(R)과 `(i+1)`번쨰 원소를 `swap` 한다.

![](https://user-images.githubusercontent.com/34808501/63827747-3d7b8900-c99f-11e9-9996-8da1953052c7.png)

- partition 과정을 통해 `pivot` 의 위치가 정해졌다.
- `pivot`을 기준으로 왼쪽은 모두 `pivot` 보다 작고 오른쪽은 모두 `pivot` 보다 큰 수가 된다.

- 위치가 정해진 `pivot` 좌우 원소에 대해 위와 같이 `partition` 하는 과정을 반복한다. -- `pivot` **좌우 원소의 갯수가 1개가 될 때 까지 반복**

```python
def partition(arr, L, R):
    pivot = arr[R]  # 마지막 값을 pivot으로 하는 quick sort
    i = L - 1  # i는 pivot 보다 작은 element 의 갯수를 의미한다.

    for j in range(L, R):
        if arr[j] <= pivot:
            i+=1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i+1], arr[R] = arr[R], arr[i+1]
    return i+1 
    # 반환하는 i+1 인덱스가 pivot의 위치가 된다. 
    # pivot 기준으로 왼쪽은 pivot 보다 작은 값들이 오른쪽은 pivot보다 큰 값이 배치된다.

def quick_sort(arr,L,R):
    if (L < R):

        # partition이 한 번 끝날 떄마다 pivot의 위치가 정해진다.
        p = partition(arr, L,R) 
        
        # 정해진 pivot 위치를 기준으로 좌우를 똑같이 quick_sort 해준다.
        quick_sort(arr, L, p-1)
        quick_sort(arr, p+1, R)
    return arr
```

### 아래와 같이 quick_sort를 구현할 수도 있다.

출처: https://stackoverflow.com/questions/18262306/quicksort-with-python

```python
def quick_sort(arr):

    less = []
    equal = []
    greater = []

    if len(arr) >1:
        pivot = arr[0]  # 첫번째 원소를 pivot 으로 하는 quick_sort  
        ## arr[-1] 이라고 하면 마지막 원소를 pivot으로 하는 quick_sort가 된다.

        for x in arr:
            if x < pivot:
                less.append(x)
            elif x == pivot:
                equal.append(x)
            elif x > pivot:
                greater.append(x)
        return quick_sort(less) + equal + quick_sort(greater)

    else: return arr
```

### Reference

- https://www.geeksforgeeks.org/python-program-for-quicksort/

- https://www.youtube.com/watch?v=COk73cpQbFQ&t=296s

- https://stackoverflow.com/questions/18262306/quicksort-with-python
