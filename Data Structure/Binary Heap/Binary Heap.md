# Binary Heap

태그: 자료구조

**📌✔**

## 힙(Heap) / 이진 힙 (Binary heap) 알아보기

- 힙은 이진 힙이라고도 함
- 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전 이진트리 (complete binary tree)를 기본으로 한 자료구조

### **📌 힙의 속성**

1. 완전 이진 트리 (Complete Binary Tree)
    - 개발 편의성, 가독성때문에 배열 인덱스 1부터 시작!
    - 모든 레벨의 노드가 채워져 있어야 하며, 마지막 레벨은 왼쪽부터 차 있어야 합니다.
2. 부모 노드 키값과 자식 노드 키값 사이에는 대소 관계가 성립 
    - 키값 대소 관계는 오로지 부모 자식간에 성립되며 형제사이에는 대소 관계가 정해지지않음
    - `MAX_HEAP` : 부모 > 자식
    - `MIN_HEAP` : 부모 < 자식

### **📌 힙의 종류 -최대 최소힙!**

1. 최대 힙 (Max Heap)
    - 부모 키값이 자식 노드 키값보다 큰 힙
    - Key(parent) ≥ Key(child)
    - 가장 큰 값이 루트 노드에 있음
        
        ![스크린샷 2023-07-23 오후 10.18.55.png](Binary%20Heap%208339a9ab2200490cab6183f9901b9cc8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-23_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.18.55.png)
        
2. 최소 힙 (Min Heap)
    - 부모 키값이 자식 노드 키값보다 작은 힙
    - Key(parent) ≤ Key(child)
    - 가장 작은 값이 루트노드에 있음
        
        ![스크린샷 2023-07-23 오후 10.19.38.png](Binary%20Heap%208339a9ab2200490cab6183f9901b9cc8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-23_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.19.38.png)
        

## #Heap 표현

- 완전 이진 트리 / 배열로 표현 ( 개발 편의성, 가독성 - index 1부터 시작)
- 루트 노드의 인덱스 i가 1인 경우
    - 노드 i의 부모 노드 인덱스 : [i/2]
    - 노드 i의 왼쪽 자식 노드 인덱스 : 2 * i
    - 노드 i의 오른쪽 자식 노드 인덱스 : 2*i +1
        
        ![스크린샷 2023-07-26 오후 12.20.12.png](Binary%20Heap%208339a9ab2200490cab6183f9901b9cc8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-26_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.20.12.png)
        

## #Heap 연산

- 최대 힙을 예시로~ , size 변수 - 전역 변수로 가정

### **📌 Heapify : 이진 트리에서 힙 속성을 유지하는 작업을 수행**

- 위에서 아래로 내려가면서 작업을 수행함
- max heap에서 heapify 작업 수행
    1. 요소 값과 자식 노드 값을 비교함
    2. 만약 자식 노드 값이 크다면, 왼쪽, 오른쪽 자식 중 가장 큰 값으로 교환함
    3. 힙 속성이 유지될때까지 1,2번 과정을 반복함
    - `예시 : 8인 노드의 heapify를 수행하는 과정`
        
        ![스크린샷 2023-07-26 오후 12.32.07.png](Binary%20Heap%208339a9ab2200490cab6183f9901b9cc8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-26_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.32.07.png)
        
    - Step1 . 첫 번째 노드 값 (8)이 자식보다 작으므로 자식 중 가장 큰 오른쪽 자식 값(20)과 교환함
    - Step2 . 값이 8인 노드에서 Heapify를 다시 시작함 8이 왼쪽 자식 노드 13보다 작기때문에 교환
        - 이제 8이 leaf node이므로 heapify를 추가 호출 해도 힙 구조에 영향을 미치지 않음
        - **`시간 복잡도: O(logN)`**
        - ✏️ **구현** : 완전 이진 트리 - 배열 (Array) 이용하여 구현, 그래프 처럼 노드 객체를 이용하여 구현할 수도 있음
        
        ```cpp
        void max_heapify (int arr[], int i)
        {
          int largest = i;  
          int left = 2*i              //left child
          int right = 2*i +1          //right child
          
          // 현재 요소 i와 자식 노드의 값을 비교
          if(left <= array_size && arr[left] > arr[i] )
            largest = left;  
          if(right <= array_size && arr[right] > arr[largest] )
            largest = right;
          
          // 자식 노드의 값이 더 크다면 교환하고 교환된 자식 노드부터 heapify 진행
          if(largest != i ) {
            swap (arr[i] , arr[largest]);
            max_heapify (h, largest);
          } 
        }
        ```
        

### **✔ 삽입 Insert**

- 힙에 원소를 추가하기 위해 업힙이라는 작업을 수행해야함
    1. 원소를 힙의 가장 마지막 노드에 추가
    2. 추가한 원소를 부모와 비교하고, 순서가 힙 조건에 일치한다면 중지
    3. 만약 힙 조건과 순서가 맞지 않을 경우, 부모와 위치를 교환 힙 조건을 일치할때까지 2~3번 반복
        
        ![스크린샷 2023-07-26 오후 12.53.52.png](Binary%20Heap%208339a9ab2200490cab6183f9901b9cc8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-26_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.53.52.png)
        

### **✔  삭제 Delete**

- 루트 노드는 힙의 종류에 따라 최댓값 , 최소값을 가짐
    - 따라 최대값이나 최소값을 탐색할때 걸리는 시간은 항상 O(1)
- 값을 추출하고 다음 값을 루트로 만드는 작업을 다운힙이라고 함
    1. 힙의 루트 노드를 삭제
    2. 마지막 노드를 루트로 이동. 루트를 자식 노드와 비교 이때 두 자식 노드중 최대 힙인 경우. 더큰 자식과 비교하며 최소 힙인 경우 더 작은 자식과 비교함 , 순서가 힙 조건과 일치한다면 중지함
    3. 만약 힙 조건과 순서가 맞지 않을 경우, 위치를 교환. 힙 조건을 일치할때까지 2~3번 반복
        
        ![스크린샷 2023-07-26 오후 12.54.02.png](Binary%20Heap%208339a9ab2200490cab6183f9901b9cc8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-26_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.54.02.png)
        

🔗 [https://yoongrammer.tistory.com/80](https://yoongrammer.tistory.com/80)

🔗 [https://kayuse88.github.io/binary-heap/](https://kayuse88.github.io/binary-heap/)