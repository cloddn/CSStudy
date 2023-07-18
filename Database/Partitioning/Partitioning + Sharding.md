# Partitioning + Sharding 간략

태그: 데이터베이스

# 파티셔닝 (Partitioning)

> 파티셔닝 : 데이터베이스를(큰 테이블이나 인덱스를) 여러 부분(작은 파티션)으로 분할하는 것
> 
> 
> VLDB (Very Large DBMS)와 같은 너무 큰 테이블이 들어가면서, 용량과 성능 측면에서 많은 이슈가 발생할때 파티셔닝 기법을 이용하여 해결함
> 
> - 데이터가 너무 커져서 조회하는 시간이 길어질때 , 관리용이성, 성능, 가용성 등의 향상을 이유로 행해지게 된다

## **📌** 파티셔닝의 이점

(1) 성능 (Performance)

- 특정 Query의 성능을 향상시킬 수 있음
- 대용량 Data Write 환경에서 효율적이다
- 필요한 데이터만 빠르게 조회할 수 있으므로 쿼리가 가벼워짐
- Full Scan에서 데이터 접근의 범위를 줄여 성능을 향상 시킴

(2) 가용성 (Availability)

- 물리적인 파티셔닝으로 전체 데이터의 훼손 가능성을 줄어들고, 데이터 가용성이 향상됨
- 파티션 별로 독립적으로 백업하고 복구할 수 있음
- 테이블의 파티션 단위로 Disk I/O를 분산하여 경합을 줄이므로 UPDATE 성능을 향상할 수 있음

(3) 관리용이성 (Manageable)

- 큰 테이블을 제거하여 쉽게 관리하도록함

(**✔**) 테이블을 여러 파티션으로 쪼개기때문에 테이블간의 Join 비용이 증가함

테이블과 인덱스를 별도로 파티셔닝할 수 없기때문에 테이블과 인덱스를 같이 파티셔닝해야한다는 단점이 존재

## **📌** 파티셔닝의 이점

### (1) 수평 파티셔닝 (Horizontal Partitioning)

![수평 파티셔닝](Partitioning%20+%20Sharding%20%E1%84%80%E1%85%A1%E1%86%AB%E1%84%85%E1%85%A3%E1%86%A8%209023c6021b874e2b8ea82b81af27401f/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_10.22.01.png)

수평 파티셔닝

- **데이터의 개수**를 기준으로 나누어 파티셔닝함
- 장점
    - 데이터의 개수와 인덱스의 개수가 줄어들어 성능이 향상됨
- 단점
    - 데이터를 찾는 과정이 기존보다 복잡하으로 Latency가 증가함

<aside>
💡 Sharding 샤딩이란?

같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법

- 샤딩과 수평 파티셔닝을 구분할 것
    - 수평 파티셔닝은 **같은 데이터베이스** 내에서 하나의 큰 테이블을 쪼개 분산 저장
    - 샤딩은 하나의 큰 테이블을 쪼개 각각 **다른 데이터베이스**에 분산 저장
</aside>

![샤딩](Partitioning%20+%20Sharding%20%E1%84%80%E1%85%A1%E1%86%AB%E1%84%85%E1%85%A3%E1%86%A8%209023c6021b874e2b8ea82b81af27401f/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_10.24.23.png)

샤딩

- 수평 파티셔닝의 장점을 다 가짐
    - 데이터의 개수와 인덱스의 개수가 줄어들어 성능이 향상됨
- 단점
    - 데이터베이스 서버 간의 연결 과정이 많아져서 비용이 증가함
    - 하나의 서버가 고장나면 데이터의 무결성이 깨질 수 있음

### (2) 수직 파티셔닝 (Vertical Partitioning)

![수직 파티셔닝](Partitioning%20+%20Sharding%20%E1%84%80%E1%85%A1%E1%86%AB%E1%84%85%E1%85%A3%E1%86%A8%209023c6021b874e2b8ea82b81af27401f/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_10.26.47.png)

수직 파티셔닝

- **테이블의 일부 열을 빼내는 형태로 분할 = 테이블 칼럼 기준**으로 나누어 파티셔닝함
- 정규화도 수직 파티셔닝과 관련된 과정이라고 볼 수 있음
    - 하지만, 수직 파티셔닝은 이미 정규화된 데이터를 분리하는 과정임
- 장점
    - 자주 사용하는 칼럼을 분리하여 성능을 향상시킴
    - 같은 타입의 데이터가 저장되어 데이터 압축률을 높일 수 있음
    - 조회시 필요없는 칼럼을 조회하지 않아도 되므로 성능상 이점이 있음
- 단점
    - 데이터를 찾는 과정이 기존보다 복잡하므로 Latency가 증가함

## **📌** 파티셔닝 범위

### (1) 범위 분할 (Range partitioning)

- 연속적인 숫자나 날짜를 기준으로 파티셔닝 ( by Range )
- 분할 키 값이 범위 내에 있는지 여부로 구분
- 우편 번호, 날짜등의 데이터에 적합

### (2) 목록 분할 (List partitioning)

- 값 목록에 파티션을 할당 분할할 키 값을 그 목록에 비추어 파티션을 선택함
- 특정 파티션에 저장될 데이터에 대한 명시적 제어가 가능함
- 분포도가 비슷하며, 많은 SQL에서 해당 칼럼의 조건이 많이 들어오는 경우 유용함

### (3) 해시 분할 (Hash partitioning)

- 파티션 키 (Key)의 해시 값에 의한 파티셔닝이 이루어짐 (by Hash)
- 균등한 데이터 분할이 가능
- 특정 데이터가 어느 Hash 파티션에 있는지 판단하기 어려움
- 해시 함수의 값에 따라 파티션에 포함할지 여부를 결정
- 파티션을 위한 범위가 없는 데이터에 적합

### (4) 합성 분할 (Composite partitioning)

- 상기 기술을 결합하는  것, 파티션의 서브 파티션을 뜻함
- 큰 파티션에 의한 I/O 요청을 여러 파티션으로 분산할 수 있음
    - 예를 들면, 먼저 범위를 분할, 다음에 해시 분할하는 것과 같은것

## **📌 파티셔닝 실제로 해보기~~**

### **✔ 배경**

AWS RDS에서 Legacy DB는 db.t2.micro 크기로 사용

![스크린샷 2023-07-18 오후 10.10.13.png](Partitioning%20+%20Sharding%20%E1%84%80%E1%85%A1%E1%86%AB%E1%84%85%E1%85%A3%E1%86%A8%209023c6021b874e2b8ea82b81af27401f/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-18_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.10.13.png)

### **✔ 분할 기준**

1. 범위 분할 ( Range partitioning)
    
    ```sql
    CREATE TABLE t1 (
        id INT,
        year_col INT
    )
    PARTITION BY RANGE (year_col) (
        PARTITION p0 VALUES LESS THAN (1991), 
        PARTITION p1 VALUES LESS THAN (1995),
        PARTITION p2 VALUES LESS THAN (1999)
    );
    
    INSERT INTO t2 (id, year_col)
    VALUES (1, 1990),(2, 1991),(3,1996),(4,1999),(5,1995),(6,1989),(7,1891),(8,1892);
    ```
    
2. 목록 분할 ( List partitioning)
    
    ```sql
    CREATE TABLE employees (
        id INT NOT NULL,
        fname VARCHAR(30),
        lname VARCHAR(30),
        hired DATE NOT NULL DEFAULT '1970-01-01',
        separated DATE NOT NULL DEFAULT '9999-12-31',
        job_code INT,
        store_id INT
    )
    PARTITION BY LIST(store_id) (
        PARTITION pNorth VALUES IN (3,5,6,9,17),
        PARTITION pEast VALUES IN (1,2,10,11,19,20),
        PARTITION pWest VALUES IN (4,12,13,14,18),
        PARTITION pCentral VALUES IN (7,8,15,16)
    );
    
    ```
    
3. 해시 분할 ( Hash partitioning)
    
    ```sql
    CREATE TABLE t1 (
        id INT,
        year_col INT
    )
    PARTITION BY HASH(id) #해시 할 칼럼 값
    PARTITIONS 8; #테이블을 나눌 분할수
    ```
    

1. 합성 분할 ( Composite Partitioning)
    
    ```sql
    CREATE TABLE ts (id INT, purchased DATE)
        PARTITION BY RANGE( YEAR(purchased) )
        SUBPARTITION BY HASH( TO_DAYS(purchased) )
        SUBPARTITIONS 2 (
            PARTITION p0 VALUES LESS THAN (1990),
            PARTITION p1 VALUES LESS THAN (2000),
            PARTITION p2 VALUES LESS THAN MAXVALUE
        );
    ```
    

🔗 [https://code-lab1.tistory.com/202](https://code-lab1.tistory.com/202)

🔗 [https://soye0n.tistory.com/267](https://soye0n.tistory.com/267)