# 정렬 (2) - quick

태그: 알고리즘

## #퀵정렬 quick sort

> 일반적으로 사용되고 있는 아주 빠른 정렬 알고리즘이며, 분할 정보 알고리즘 중ㅎ 나아미
> 
- Pivot 피봇을 지정해서 기준점으로 잡음
- 불안정 정렬에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속함
- 분할 정복 알고리즘의 한 종류로, 평균적으로 매우 빠른 속도를 가짐
- n개의 데이터를 정렬할 때, 최악의 경우 O(n^2) 비교를 수행하고 평균적으로 O(n logn)의 비교를 수행함

![img.gif](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(2)%20-%20quick%20521eaf2442a8460089850a04b3c1718c/img.gif)

- 위 gif 이미지에서 보면 노란색이 pivot, 초록색이 pivot보다 작은 데이터, 보라색이 pivot보다 큰 데이터, 주황색이 정렬이 완료된 데이터이다.

### **📌 quick 정렬 순서**

```
1. 리스트 중에서 하나의 원소를 고름
	해당 원소를 pivot 피봇으로 지정함
2. 피봇 앞으로는 피봇보다 값이 작은 원소들이 오고, 뒤로는 피봇보다 값이 큰 원소들이 오도록 피봇을 기준으로 리스트를 둘로 나눈다
	2-1. 리스트가 둘로 나뉘는 것을 분할
	2-2. 분할을 마친 뒤 , 피봇은 더이상 움직이지 않음
3. 분할된 두 리스트에 대해 재귀적으로 위 과정을 반복한다. 
	리스트의 크기가 1이하가 되도록
```

- ✏️ **quick 정렬 실제 정렬 과정 알아보기~**
    1. 피봇 : p 
        
        리스트 왼쪽 끝과 오른쪽 끝에서 시작한 인덱스들을 l,r
        
        ```
        5 - 3 - 7 - 6 - 2 - 1 - 4
                                p
        ```
        
    
     2. 리스트 왼쪽에 있는 l 위치의 값이 피봇보다 크고 오른쪽 r위치의 값은 피봇 값보다 작으므로 둘이 swap 
    
    ```
    5 - 3 - 7 - 6 - 2 - 1 - 4
    l                   r   p
    
    1 - 3 - 7 - 6 - 2 - 5 - 4
    l                   r   p
    ```
    
    1. r 위치의 값이 피봇보다 작지만 , l 위치의 값도 피봇보다 작으므로 교환하지 않음
        
        ```
        1 - 3 - 7 - 6 - 2 - 5 - 4
            l           r       p
        ```
        
    2. l 위치를 피봇 값보다 큰 값이 나올 때까지 진행하고 , l이 피봇값보다 크고, r이 피봇값보다 작으므로 둘이 swap 
    
    ```
    1 - 3 - 7 - 6 - 2 - 5 - 4
            l       r       p
    1 - 3 - 2 - 6 - 7 - 5 - 4
            l       r       p
    ```
    
    1. l 위치가 r위치보다 커지면, (index)
        
        **l 위치의 값과 피봇 값을 swap**함
        
        ```
        1 - 3 - 2 - 6 - 7 - 5 - 4
                                p
        1 - 3 - 2 - 4 - 7 - 5 - 6
                    p
        ```
        
    2. 피봇 값 좌우의 리스트에 대해 각각 퀵 정렬을 재귀적으로 수행함
        
        ```
        1 - 3 - 2       7 - 5 - 6
        1 - 2 - 3       5 - 6 - 7
        ```
        
    3. 완성된 리스트는 다음과 같음
        
        `1 - 2 - 3 - 4 - 5 - 6 - 7`
        
- ✏️ **quick 정렬 구현하기**
    
    ```python
    # 가장 일반적인 퀵 정렬
    def quick_sort(array, start, end):
        if start >= end: return # 원소가 1개인 경우
        pivot = start # 피벗은 첫 요소
        left, right = start + 1, end
        
        while left <= right:
            # 피벗보다 작은 데이터를 찾을 때까지 반복
            while left <= end and array[left] <= array[pivot]:
                left += 1
            # 피벗보다 큰 데이터를 찾을 때까지 반복
            while right > start and array[right] >= array[pivot]:
                right -= 1
            if left > right: # 엇갈린 경우
                array[right], array[pivot] = array[pivot], array[right]
            else: # 엇갈리지 않은 경우
                array[right], array[left] = array[left], array[right]
        # 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
        quick_sort(array, start, right - 1)
        quick_sort(array, right + 1, end)
    
    # 파이썬의 장점을 살린 퀵 정렬
    def quick_sort(array):
        # 리스트가 하나 이하의 원소를 가지면 종료
        if len(array) <= 1: return array
        
        pivot, tail = array[0], array[1:]
        
        leftSide = [x for x in tail if x <= pivot]
        rightSide = [x for x in tail if x > pivot]
        
        return quick_sort(leftSide) + [pivot] + quick_sort(rightSide)
    ```
    

### **✔ 퀵 정렬 특징**

- **`장점`**
    - 속도가 빠르다 퀵!!!!
        - 시간 복잡도 O (n logn)을 가진 다른 정렬 알고리즘과 비교했을때도 가장 빠른 속도를 가짐
    - 추가 메모리 공간이 필요하지 않음
        - **O(logn)만큼의 메모리를 필요로함  ?**
- **`단점`**
    - 정렬된 리스트에 대해서는 퀵 정렬 분할로 인해 수행시간이 더 소요됨
    - 퀵 정렬 불균형 분할을 방지하기 위해 피봇을 선택할때 신중해야함!
        - 단점을 해결하기 위해 임의의 요소를 선택 후 중 간값을 선택하는 식으로 피봇을 선택함
- **`시간 복잡도`**
    - 최선의 경우 n만큼 파티션을 나누는데 그때마다 데이터가 절반씩 줄어들어 **O(nlogn)**
    - 최악의 경우 **O(n^2)**
        - 순환 호출의 깊이가 n
        - 특히 이미 정렬된 리스트에 대하여 퀵정렬을 시도하는 경우, 순환 호출 깊이 * 각 순환 호출 단계 비교 연산 = n^2
    - 평균적으로 **O(nlogn)**임
        - 불필요한 데이터 이동을 줄이고, 한번 결정된 피봇은 추후 연산에 사용하지 않기때문에

🔗 [https://velog.io/@roro/자료구조알고리즘-퀵정렬-힙정렬-위상-정렬#02-힙정렬-heap-sort](https://velog.io/@roro/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%80%B5%EC%A0%95%EB%A0%AC-%ED%9E%99%EC%A0%95%EB%A0%AC-%EC%9C%84%EC%83%81-%EC%A0%95%EB%A0%AC#02-%ED%9E%99%EC%A0%95%EB%A0%AC-heap-sort)

🔗 [https://latte-is-horse.tistory.com/197](https://latte-is-horse.tistory.com/197)