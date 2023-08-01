# 정렬 (1) - bubble , selection , insertion

태그: 알고리즘

**📌**

## #거품 정렬 (Bubble Sort)

> 거품 정렬은 앞에서부터 두 개의 아이템을 비교해가면서 둘 중 큰 값을 오른쪽, 작은 값을 왼쪽으로 정렬하는 알고리즘임
> 

![images-flexing1010-post-a674a167-234e-4763-90b0-f4bbef17bdcf-bubble-sort-001.gif](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(1)%20-%20bubble%20,%20selection%20,%20insertion%20db6cba3601ac48f98f1798541d3f472d/images-flexing1010-post-a674a167-234e-4763-90b0-f4bbef17bdcf-bubble-sort-001.gif)

### **📌 구현 _ 파이썬**

> 아이디어
> 

```
1. 배열의 i번째 인덱스와 i+1번째 인덱스의 키를 비교한다.
2. i번째 인덱스의 키가 더 크다면 자리를 상호 교환(swap)한다.
3. 위 과정을 반복수행한다.
```

```python
arr = [4, 6, 1, 7, 2, 9, 3]

n = len(arr)

for i in range(n-1, 0, -1):
	for j in range(i):
		if arr[j] > arr[j+1]:
			arr[j], arr[j+1] = arr[j+1], arr[j]
```

### **✔ 특징**

- **`복잡도`**
    - 시간복잡도 : O(n^2)
        - 최선, 평균, 최악의 모든 경우가 같은 복잡도를 가짐
    - 공간복잡도 : O(n)
- **`장점`**
    - 구현이 간단하고 코드가 직관적임
    - 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않음
        - 제자리 정렬 ( in-place sorting)
    - 안정 정렬 ( Stable Sort)
- **`단점`**
    - 어떤 상황에도 시간복잡도가 O(n^2)이므로 비효율적임
    - 정렬되어있지 않은 원소가 제자리를 찾아가기 위해, 교환 연산(Swap)이 많이 일어나게 됨

## #선택 정렬 (Selection Sort)

> 먼저 배열의 **첫 원소를 저장**하고, 나머지 원소들과 비교하여 해당 원소보다 **작은 값**이 있으면 그 값을 대신 저장해가면서 **가장 작은 값을 찾음**
> 
> 
> 이렇게 찾은 가장 작은 값을 **배열의 시작점에 있는 값과 위치**를 바꿔주고, 다음 위치로 넘어가서 이 과정을 반복함 
> 

![images-flexing1010-post-de423e70-b103-42f4-ac28-cc12b30a16af-selection-sort-001.gif](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(1)%20-%20bubble%20,%20selection%20,%20insertion%20db6cba3601ac48f98f1798541d3f472d/images-flexing1010-post-de423e70-b103-42f4-ac28-cc12b30a16af-selection-sort-001.gif)

### **📌 구현 _ 파이썬**

> **`아이디어`**
> 

```
1. 배열의 가장 마지막 인덱스를 선택한다.
2. 현재 인덱스 이전의 값들을 비교하여 가장 큰 수를 선택한다.
3. 선택된 두 값을 교체한다.
4. 인덱스를 줄여가며 위의 과정을 반복한다.
```

```python
arr = [4, 6, 1, 7, 2, 9, 3]

n = len(arr)

for i in range(n-1, 0, -1):
	max_idx = i

	for j in range(i):
		if arr[j] > arr[max_idx]:
			max_idx = j
	
	arr[i], arr[max_idx] = arr[max_idx], arr[i]
```

### **✔ 특징**

- **`복잡도`**
    - 시간복잡도 : O(n^2)
    - 공간복잡도 : O(n)
- **`장점`**
    - 단순한 알고리즘
    - 정렬을 위한 비교 횟수는 많지만, 버블 정렬에 비해 실제로 교환하는 횟수는 적으므로 많은 교환이 일어나야하는 자료상태에서는 비효율적임
    - 정렬하고자하는 배열안에서 교환하는 방식이라 다른 메모리 공간을 필요로하지 않음
        - 제자리 정렬 ( in-place sorting)
- **`단점`**
    - 시간이 오래 걸림
    - 많은 교환이 일어나야하는 자료상태에서는 비효율적임
        - 정렬된 상태에서 추가되었을때 정렬 효율이 좋지 않음.
    - 불안정 정렬 ( Unstable Sort)
    

## #삽입 정렬 (Insertion Sort)

> 실제 인간이 정렬하는 논리와 유사함
> 
> 
> 두 번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교해가며 , 타겟 원소의 값이 비교 원소 값보다 크다면 비교 원소 뒤로 자리를 옮겨주는 알고리즘 
> 

![images-flexing1010-post-100bfd8c-c818-4208-aeda-5004f18ca3f1-insertion-sort-001.gif](%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%A7%E1%86%AF%20(1)%20-%20bubble%20,%20selection%20,%20insertion%20db6cba3601ac48f98f1798541d3f472d/images-flexing1010-post-100bfd8c-c818-4208-aeda-5004f18ca3f1-insertion-sort-001.gif)

### **📌 구현 _ 파이썬**

> **`아이디어`**
> 

```
1. i번째 원소와 0부터 i-1번째 원소를 비교한다.
2. 이 때, i번째 값보다 작은 값을 발견하면 그 위치에 i번째 원소를 삽입한다.
3. 위 과정을 반복한다.
```

```python
for i in range(1, n):
	key = arr[i]
	idx = i

	while idx > 0 and arr[idx-1] > key:
		arr[idx] = arr[idx-1]
		idx -= 1

	arr[idx] = key
```

### **✔ 특징**

- **`복잡도`**
    - 시간복잡도 : O(n^2)
        - 최선의 경우 (=이미 정렬이 되어있는 경우) O(n)
    - 공간복잡도 : O(n)
- **`장점`**
    - 단순한 알고리즘
    - 대부분의 원소가 이미 정렬되어있는 경우 효율적일 수 있음
    - 안정 정렬 ( Stable Sort)
    - 정렬하고자하는 배열안에서 교환하는 방식이라 다른 메모리 공간을 필요로하지 않음
        - 제자리 정렬 ( in-place sorting)
    - 같은 O(n^2)알고리즘 : Selection Sort, Bubble Sort와 비교하여 상대적으로 빠름
    
- **`단점`**
    - 다른 선택정렬, 버블 정렬에 비해선 빠를 뿐.. 여전히 비효율적임

🔗 [https://velog.io/@seongmini/Algorithm-버블-정렬](https://velog.io/@seongmini/Algorithm-%EB%B2%84%EB%B8%94-%EC%A0%95%EB%A0%AC)

🔗 [https://velog.io/@flexing1010/알고리즘-정렬-Bubble-Sort-Selection-Sort-Insertion-Sort](https://velog.io/@flexing1010/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%A0%95%EB%A0%AC-Bubble-Sort-Selection-Sort-Insertion-Sort)

🔗 [https://velog.io/@seongmini/Algorithm-선택-정렬](https://velog.io/@seongmini/Algorithm-%EC%84%A0%ED%83%9D-%EC%A0%95%EB%A0%AC)