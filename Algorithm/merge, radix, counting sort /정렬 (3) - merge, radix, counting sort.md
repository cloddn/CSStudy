# 정렬 (3) - merge, radix, counting sort

태그: 알고리즘

## #merge sort 병합 정렬

![YlHqG.gif](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(3)%20-%20merge,%20radix,%20counting%20sort%207c60ac60d2dd46c4a16cd2e0cc8e1de2/YlHqG.gif)

> 병합 정렬 : Devide and Conquer 분할 정복 기법 & 재귀 알고리즘 → 정렬 알고리즘
> 
- ✏️ **실제 정렬 과정과 함께 알아보기~**
    - 주어진 배열을 원소가 하나 밖에 남지 않을때까지 계속 둘로 쪼갠 후에 다시 크기 순으로 재배열하면서 원래 크기의 배열로 합침
    - **예시 : 1부터 8까지 총 8개의 숫자가 들어있는 배열에 있다고 가정**
        
        `[6, 5, 3, 1, 8, 7, 2, 4]`
        
        하나의 배열을 두 개로 쪼갬
        
        `[6, 5, 3, 1] [8, 7, 2, 4]`
        
        두 개의 배열을 네개로 쪼갬
        
        `[6, 5] [3, 1] [8, 7] [2, 4]`
        
        다시 네개 의 배열을 하나씩 또 쪼갬
        
        `[6] [5] [3] [1] [8] [7] [2] [4]`
        
        두 개씩 합치면서, 작은 숫자가 앞, 큰 숫자가 뒤에 위치시킴
        
        `**[5, 6] [1, 3] [7, 8] [2, 4]**`
        
        **각 배열 내에서 가장 작은 값 2개를 비교해서 더 작은 값을 먼저 선택하면 자연스럽게 크기 순으로 선택**
        
        `**[1, 3, 5, 6] [2, 4, 7, 8]**`
        
        ⇒ 
        
        크기순으로 선택하면서 하나로 합치면 정렬된 배열을 얻을 수 있음 
        
        `[1, 2, 3, 4, 5, 6, 7, 8]`
        
    
- ✏️ **실제 정렬 구현 알아보기! “재귀이용”**
    - 재귀를 이용하여 구현가능!
    - 최대한 분할한 후에 다시 병합하면서 큰 배열을 만들어 나가면 됨
    - 따라 재귀 알고리즘의 기저 조건은 입력 배열 크기가 2보다 작을때이며, 이 조건에 해당할때에는 배열을 그대로 반환하면 됨
    - python의 slice notation ( arr[start:end])을 사용하면 간결한 코드를 작성할 수 있음
        - 리스트 slice를 할때 배열의 복제가 일어나므로 메모리 사용 효율은 좋지 않음
    
    ```python
    def merge_sort(arr):
        if len(arr) < 2:
            return arr
    
        mid = len(arr) // 2
        low_arr = merge_sort(arr[:mid])
        high_arr = merge_sort(arr[mid:])
    
        merged_arr = []
        l = h = 0
        while l < len(low_arr) and h < len(high_arr):
            if low_arr[l] < high_arr[h]:
                merged_arr.append(low_arr[l])
                l += 1
            else:
                merged_arr.append(high_arr[h])
                h += 1
        merged_arr += low_arr[l:]
        merged_arr += high_arr[h:]
        return merged_arr
    
    #최적화 할경우, 병합 결과를 담을 새로운 배열을 매번 생성해서 리턴하지 않고 인덱스 접근을 이용하여 입력 배열을 계속해서 업데이트할 경우 메모리 사용량을 대폭 줄일 수 있음 ( In-place sort )
    
    def merge_sort(arr):
        def sort(low, high):
            if high - low < 2:
                return
            mid = (low + high) // 2
            sort(low, mid)
            sort(mid, high)
            merge(low, mid, high)
    
        def merge(low, mid, high):
            temp = []
            l, h = low, mid
    
            while l < mid and h < high:
                if arr[l] < arr[h]:
                    temp.append(arr[l])
                    l += 1
                else:
                    temp.append(arr[h])
                    h += 1
    
            while l < mid:
                temp.append(arr[l])
                l += 1
            while h < high:
                temp.append(arr[h])
                h += 1
    
            for i in range(low, high):
                arr[i] = temp[i - low]
    
        return sort(0, len(arr))
    ```
    

### **📌 merge sort 특징**

- 분할 (split) 단계, 병합 (merge) 단계로 나눌 수 있으며,
    - 중간 인덱스를 찾아야하는 분할 비용보다 모든 값을 비교해야하는 병합 비용이 더 큼
    - 예제에서 보이는 것과 같이 8→4→2→1로 전반적인 반복의 수는 점점 절반으로 줄어들기때문에 `O(logN)` 시간이 필요하며, 각 패스에서 병합할때 모든 값을 비교해야하므로 `O(N)`시간이 소모됨
        - 시간 복잡도 : **`O(N logN)`**
    - 두 개의 배열을 병합할때 병합 결과를 담아 놓을 배열이 추가로 필요함.
        - 공간 복잡도 : **`O(N)`**
    - 다른 정렬 알고리즘과 달리 인접한 값들 간에 상호 자리 교대(swap)이 일어나지 않음

## #couting sort 계수 정렬

> 각 요소의 배열 등장 횟수를 count하여 누적합으로 나타내는 배열을 만든 뒤에, 그 누적합으로 요소들의 index를 알아내어, 작은 숫자 순서대로 정렬하는 기법임
> 

![images-wjdqls9362-post-aa2a3782-0bcd-41e8-b9a8-474df19d1fd6-countingSort.jpg](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(3)%20-%20merge,%20radix,%20counting%20sort%207c60ac60d2dd46c4a16cd2e0cc8e1de2/images-wjdqls9362-post-aa2a3782-0bcd-41e8-b9a8-474df19d1fd6-countingSort.jpg)

### **📌 counting sort 특징**

- 비교 정렬이 아니므로 시간 복잡도 :  **`O ( n + k )`**
    - k는 Input 요소의 최댓값
        - k가 작은 수라면 O(n)이겠지만, k가 무한으로 커질때에는 O(무한)이 될 수 있다.
    - O(n+k)는 n or k 라는 뜻으로, n이 클지, k가 클지 아직 모르는 상태
- input arr의 요소중 최솟값~ ( 최댓값-1 ) 길이 만큼의 누적합 배열(혹은 객체)를 필요로하는 정렬 기법이므로 요소간 차이가 크거나, 최댓값 요소가 매우 클 경우 메모리 낭비가 심한 경우가 생길 수 있음

- ✏️ **실제 정렬 구현 알아보기!**
    
    ```python
    # 모든 원소의 값이 0보다 크거나 같다고 가정
    array = [7, 5, 9, 0, 3, 1, 6, 2, 9, 1, 4, 8, 0, 5, 2]
    # 모든 범위를 포함하는 리스트 선언 (모든 값은 0으로 초기화)
    count = [0] * (max(array) + 1)
    
    for i in range(len(array)):
        count[array[i]] += 1 # 각 데이터에 해당하는 인덱스의 값 증가
    
    for i in range(len(count)): # 리스트에 기록된 정렬 정보 확인
        for j in range(count[i]):
            print(i, end=' ') # 띄어쓰기를 구분으로 등장한 횟수만큼 인덱스 출력
    
    #실행 결과 :0 0 1 1 2 2 3 4 5 5 6 7 8 9 9
    ```
    

## #****Radix**** sort 기수 정렬

> **(낮은 자리에서)** 0의 자리, 10의 자리 , 100의 자리 1* (0의 n개) 자리수 **(높은 자리 순으로)** 를 기준으로 정렬하는 비교 연산을 하지 않는 정렬 기법
> 
> 
> 주어진 수 들간의 비교를 하지 않고, 0~9까지 버킷이 있고, 해당 버킷을 사용하여 정렬하는 방법
> 
> - 기수 : 주어진 데이터를 구성하는 기본요소.
>     - 2진수는 0과 1, 10진수는 0~9, 영문자는 a~z까지 각 기수의 개수만큼 만드는 것

![images-wjdqls9362-post-92c336e8-fee4-4418-849b-52e0ce70f7bf-radixSort.jpg](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(3)%20-%20merge,%20radix,%20counting%20sort%207c60ac60d2dd46c4a16cd2e0cc8e1de2/images-wjdqls9362-post-92c336e8-fee4-4418-849b-52e0ce70f7bf-radixSort.jpg)

### **📌 radix sort 특징**

- 시간 복잡도 : O(N) / O(r*N) : r은 숫자 자리수, n은 정렬될 수의 갯수
    - O(NlogN) 정렬법을 깨는 유일한 정렬법
    - 하지만, 데이터 타입이 일정해야하고 양의 정수는 양의 정수끼리 음의 정수는 음의 정수끼리 비교해야하는 등 구현에 많은 조건이 붙어 사용하기 까다로움
- 제자리 정렬이 아니므로, 추가적인 메모리가 많이 필요함 ㅠㅠ
- 내부적으로 중간 정렬을 사용하는데 k (요소중 최댓값)에 따라 사용되는 중간 정렬이 다름
    - k가 작을때는 계수 정렬 (couting sort), k가 클 때는 퀵정렬 (quick sort)를 사용하는 것이 좋음
    
- ✏️ **실제 정렬 과정 알아보기!**
    
     `[153, 262, 37, 598, 433, 855]` 를 기수 정렬을 이용하여 정렬해보자
    
    1. 가장 낮은 1번째 자리부터 (1의 자리) , 가장 높은 3번째 자리 (100의 자리) 순으로 정렬한다
        
        ![R1280x0.jpeg](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(3)%20-%20merge,%20radix,%20counting%20sort%207c60ac60d2dd46c4a16cd2e0cc8e1de2/R1280x0.jpeg)
        
    2. 다음과 같이 0~9까지의 버킷들이 자릿수별로 있고, 해당하는 자릿수에 맞게 버킷에 담게 된다
        
        ![R1280x0-2.jpeg](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(3)%20-%20merge,%20radix,%20counting%20sort%207c60ac60d2dd46c4a16cd2e0cc8e1de2/R1280x0-2.jpeg)
        
    
    `결과 : [37, 153, 262, 433, 598, 855]`
    
    - **`과정`** :
        - 1의 자리 버킷에 수들을 담고 -> 버킷에 담긴 순서대로 꺼내온다. (1의 자리로 정렬)
        - 꺼내온 것을 이번엔 10의 자리 버킷에 수들을 담고 -> 버킷에 담긴 순서대로 꺼내온다. (10의 자리로 정렬)
        - 꺼내온 것을 마지막으로 100의 자리 버킷에 수들을 담고 -> 버킷에 담긴 순서대로 꺼내온다. (100의 자리로 정렬)

- ✏️ **실제 정렬 구현 알아보기!**
    
    ```python
    from collections import deque
    
    def radixSort():
        nums = list(map(int, input().split(' ')))
        buckets = [deque() for _ in range(10)]
        
        max_val = max(nums)
        queue = deque(nums)
        digit = 1 # 자릿수
        
        while (max_val >= digit): # 가장 큰 수의 자릿수일 때 까지만 실행
            while queue:
                num = queue.popleft()
                buckets[(num // digit) % 10].append(num) # 각 자리의 수(0~9)에 따라 버킷에 num을 넣는다.
            
            # 해당 자릿수에서 버킷에 다 넣었으면, 버킷에 담겨있는 순서대로 꺼내와 정렬한다.
            for bucket in buckets:
                while bucket:
                    queue.append(bucket.popleft())
            print(digit,"의 자릿 수 정렬: ", list(queue))
            digit *= 10 # 자릿수 증가시키기
        
        print(list(queue))
    ```
    

🔗 [https://www.daleseo.com/sort-merge/](https://www.daleseo.com/sort-merge/)

🔗 [https://velog.io/@wjdqls9362/Algorithm-정렬-Radix-sort-Counting-sort](https://velog.io/@wjdqls9362/Algorithm-%EC%A0%95%EB%A0%AC-Radix-sort-Counting-sort)

🔗 [https://freedeveloper.tistory.com/378](https://freedeveloper.tistory.com/378)

🔗 [https://10000cow.tistory.com/entry/정렬-7-기수-정렬radix-sort](https://10000cow.tistory.com/entry/%EC%A0%95%EB%A0%AC-7-%EA%B8%B0%EC%88%98-%EC%A0%95%EB%A0%ACradix-sort)