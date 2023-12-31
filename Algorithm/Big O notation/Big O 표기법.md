# Big O 표기법

태그: 알고리즘

**📌✔**

> 알고리즘의 복잡도를 판단하는 척도는 시간복잡도와 공간 복잡도가 있음
> 
> 
> 그 중 시간 복잡도는 알고리즘 내 연산의 횟수와 밀접한 관계가 있다
> 

## #공간 복잡도 ( Space complexity )

- 공간 복잡도는 프로그램이 실행되고 완료되기까지 사용하는 총 저장 공간량을 의미
- 저장 공간 → 고정 공간 / 가변 공간으로 나뉨
    - 고정 공간 : 알고리즘과 관련 없는 공간으로 코드와 단순 변수, 상수가 해당됨
    - 가변 공간 : 알고리즘이 수행되며 동적으로 할당되는 공간임, 알고리즘과 밀접한 관련이 있음
    
    $$
    S(P)=c+Sp(n)
    $$
    
    - c : 고정 공간
    - Sp(n)는 가변 공간 → 공간 복잡도 결정짓는 요소

## #시간 복잡도 (Time complexity)

- 시간 복잡도는 프로그램이 실행되고 완료되기까지 사용하는 총 소요 시간을 의미
- 소요 시간 = 컴파일 시간 + **실행 시간**
    - 명령문의 실행 빈도수에 따라 대략적으로 소요 시간을 나타내기 위해 사용
    

## #시간 복잡도 (Time complexity) 표기법

- Big-O (빅오 표기법) : 알고리즘 **`최악의 실행 시간`**을 표기함
    - 가장 많이 사용하는 표기법
    - 최소한 보장되는 성능을 표기하기때문에 가장 일반적으로 사용
        
        ![스크린샷 2023-07-28 오후 7.54.29.png](Big%20O%20%E1%84%91%E1%85%AD%E1%84%80%E1%85%B5%E1%84%87%E1%85%A5%E1%86%B8%20069dd56c43b74ac3aa1da789b69f5372/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_7.54.29.png)
        

- Big-**Ω** (빅 오메가 표기법) : 알고리즘 **`최상의 실행시간`**을 표기함
- Big-**θ** (빅 세타 표기법) : 알고리즘 **`평균 실행 시간`**을 표기함

## **📌 빅오 표기법  (Big-O notation) 특징**

- 시간 복잡도에 미미한 영향을 주는 것들은 배제하고 표기됨
1. 상수항을 무시
    - 어떤 알고리즘이 O(N+5)의 시간복잡도를 가질 경우 상수를 생략하고 O(N)으로 표기함
2.  계수도 무시
    - 어떤 알고리즘이 O(3N)의 복잡도를 가졌으면 계수를 생략하여 O(N)으로 표기함
3. 최고차항만 표기
    - 어떤 알고리즘이 O(3N^3+2N^2+N+5)의 복잡도를 가졌으면 O(N^3)으로 표기함

## **📌 빅오 표기법  (Big-O notation) 종류**

> **실행속도**
> 
> 
> `O(1) < O ( log N ) < O(N) < O(N log N) < O(N^2) < O(2^N)`
> 

![스크린샷 2023-07-28 오후 7.41.34.png](Big%20O%20%E1%84%91%E1%85%AD%E1%84%80%E1%85%B5%E1%84%87%E1%85%A5%E1%86%B8%20069dd56c43b74ac3aa1da789b69f5372/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-28_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_7.41.34.png)

1. O(1)
    - 입력값(N)이 증가해도 실행시간은 동일한 알고리즘
    - index로 바로 접근하여 처리할 수 있는 연산과정의 시간 복잡도
    
    → 기본 연산 수 라고 생각하면 편함
    
    `예시)` Stack의 push,pop
    

1. O(log N)
    - 연산이 한번 실행될때마다 데이터의 크기가 절반으로 감소하는 알고리즘
        - log의 지수는 항상 2
    
    `예시)` binary search 알고리즘, tree 형태 자료구조 탐색
    

1. O(N)
    - 입력 값이 증가함에 따라 실행 시간도 선형적으로 증가하는 알고리즘
    
    `예시)` 1중 for문
    

1. O(N log N)
    - O(N)의 알고리즘과 O(log N)의 알고리즘이 중첩된 형태
    
    `예시)` 퀵 / 병합 / 힙 정렬
    

1. O(N^2)
    - 2중 반복 돌게 되는 알고리즘
    
    `예시)` 2중 For 문, 삽입 / 버블 / 선택 정렬
    

1. O(2^N)
    - 빅오 표기법중 가장 느린 시간 복잡도로 주로 재귀적으로 수행되는 알고리즘이 해당함
    
    `예시)` fibonacci 수열
    

<aside>
✏️ **알고리즘 문제 풀 때의 Tip!**

- 입력 데이터의 범위와 실행 시간 범위를 고려하면 문제에 대한 감을 잡을 수 있음
- 보통 코드 1억번 수행시간은 1초
- 이를 기준으로 전체 수행시간을 어림잡아 문제에 사용되는 알고리즘에 대한 힌트를 얻을 경우 알고리즘 사용 여부를 판단하여 접근할 수 있음
</aside>

🔗 [https://velog.io/@nana-moon/알고리즘-빅오-표기법big-O-notation이란](https://velog.io/@nana-moon/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%B9%85%EC%98%A4-%ED%91%9C%EA%B8%B0%EB%B2%95big-O-notation%EC%9D%B4%EB%9E%80)

🔗 [https://hudi.blog/time-complexity/](https://hudi.blog/time-complexity/)