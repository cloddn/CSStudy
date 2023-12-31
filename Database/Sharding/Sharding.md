# Sharding

태그: 데이터베이스

# DB Sharding

> 데이터베이스의 샤딩 : 한 테이블의 row들을 여러 개의 서로 다른 테이블, 즉 파티션으로 물리적으로 분리하는 것
> 
> 
> row들을 여러개의 서로 다른 테이블로 분해하는 것 = 한 테이블을 Horizontal Partitioning했다고 볼 수 있음
> 

![스크린샷 2023-07-17 오전 11.54.08.png](Sharding%20392a6fdafd19423693adf8f3279e2b8a/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_11.54.08.png)

- 기존에 하나의 구성될 스키마를 다수의 복제본으로 구성하고 각각의 샤드에 어떤 데이터가 저장될지를 샤드키를 기준으로 분리함
- 주로 application level에서 실행되며, 어떤 샤드로 읽기와 쓰기를 전송할지 정의하는 코드를 가지게 됨
    - 어떤 데이터 베이스에서는 내장된 샤딩 기능이 있어, database level에서 실행될때도 있음

## **📌 샤딩의 장단점**

- 장점
    - Scale-out 이 가능
    - 스캔 범위를 줄여서 쿼리 반응 속도를 빠르게 함
    - 장애가 샤드 단위로 발생
- 단점
    - 프로그래밍 복잡도 증가
    - 데이터가 한 쪽 샤드로 몰릴 경우 (Hotspot), 샤딩이 무의미해짐
    - 잘 못 사용할 경우 risk가 큼
    - 한번 샤딩 사용시 샤딩 이전의 구조로 돌아가기 힘듦

- 프로그래밍, 운영적 복잡도가 높아지는 단점
    - 샤딩은 피하는 것이 좋음, 다른 방법 사용!
    - 예시 ) 데이터베이스 서버의 Scale-UP,
    - Read의 부하가 클 경우 Cache 사용 및 Database Replication,
    - 테이블의 일부 컬럼만 주로 사용할경우 Vertical Partitioning 등 사용

## **📌 여러가지 샤딩 방식**

> 샤드 키에 따라 달라짐
> 
> 
> 최대한 샤드들에게 균일하게 분산하는 것이 좋음
> 

### (1) Hash Sharding

![스크린샷 2023-07-17 오후 12.00.03.png](Sharding%20392a6fdafd19423693adf8f3279e2b8a/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.00.03.png)

- 데이터베이스의 id를 샤딩하는 방식
- 샤드키를 id%num하여 정하는 방식
- 한번 나눌 갯수를 정해놓으면 수정하지 못한다는 단점이 있고, 단순히 hashing 방식이기에 데이터가 저장되는 공간적 효율에 대한 고려는 따로 할 수 없음

### (2) Dynamic Sharding

![스크린샷 2023-07-17 오후 12.01.24.png](Sharding%20392a6fdafd19423693adf8f3279e2b8a/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.01.24.png)

- 일종의 Locator Service를 통하여 샤드 키를 정하는 방식
- Locator Service를 한번 거쳐서 샤드키를 얻기때문에 확장에 유연함
    - 데이터 재배치등에 있어 Locator Service로 변환해야하기때문에 Locator에 의존적이라는 단점 존재

### (3) Entity Group

![스크린샷 2023-07-17 오후 12.02.49.png](Sharding%20392a6fdafd19423693adf8f3279e2b8a/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-17_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_12.02.49.png)

- key-vale 방식인 Hash Sharding, Dynamic Sharding과는 다르게,
- 동일한 파티션에 관련된 엔티티를 저장하여 단일 파티션 안에 추가 기능을 제공하는 방식
- 즉, 관련된 데이터에 하나의 샤드를 이용하는 방식
- 하나의 물리적인 샤드를 이용하기에 쿼리진행시 효과적이며, 응집도가 높아진다는 장점이 있음
- 다른 샤드와 관련된 쿼리를 사용하게 된다면 샤드를 사용안했을때보다 성능이 더 떨어질 수 있다는 단점이 존재함

🔗 [https://minkwon4.tistory.com/317](https://minkwon4.tistory.com/317)