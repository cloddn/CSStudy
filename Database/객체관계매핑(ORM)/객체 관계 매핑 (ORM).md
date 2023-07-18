# 객체 관계 매핑 (ORM)

태그: 데이터베이스

<aside>
💡 영속성(Persistence)

- 데이터를 생성한 프로그램을 종료되더라도 사라지지않는 데이터의 특성을 말함
- 영속성을 갖지 않는 데이터는 단지 메모리에서만 존재하기때문에 프로그램을 종료하면 모두 잃어버리게 됨
</aside>

- **Object Persistence (영구적인 객체)**
    - 메모리 상의 데이터를 파일 시스템, 관계형 데이터베이스 혹은 객체 데이터베이스 등을 활용하여 영구적으로 저장하여 영속성을 부여
        
        ![스크린샷 2023-07-18 오후 10.21.44.png](%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A8%20%E1%84%86%E1%85%A2%E1%84%91%E1%85%B5%E1%86%BC%20(ORM)%20a68dffea33b642039aa919498e84661d/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-18_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.21.44.png)
        
    - 데이터를 데이터베이스에 저장하는 3가지 방법
        1. JDBC ( JAVA에서 사용 )
        2. Spring JDBBC ( ex: JdbcTemplate)
        3. Persistence Framework (ex: Hibernate , Mybatis 등)
- **Persistence Layer**
    - 프로그램의 아키텍처에서 데이터에 영속성을 부여해주는 계층을 말함
    - JDBC를 이용하여 직접 구현할 수 있지만 Persistence framework을 이용한 개발이 많이 이루어짐
- **Persistence Framework**
    - JDBC 프로그래밍의 복잡함이나 번거로움없이 간단한 작업만으로 데이터베이스와 연동되는 시스템을 빠르게 개발할 수 있으며 안정적인 구동을 보장
    - Persistence Framework는 SQL Mapper와 ORM으로 나눌 수 있음
        - `ex)` JPA, Hibernate, Mybatis

# ORM (object Relational Mapping)

**📌** Object Relational Mapping, 객체-관계 매핑

- 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑(연결)해주는 것을 말함
    - 객체 지향 프로그래밍은 클래스를 사용하고 관계형 데이터베이스는 테이블을사용함
        - 따라, 객체 모델과 관계형 모델간의 불일치가 존재
    - ORM을 통해 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결함
- 데이터 베이스 데이터 ← 매핑 → Obejct 필드
    - 객체를 통해 간접적으로 데이터베이스 데이터를 다룸
- Persistent API라고도 할 수 있음
    - `ex)` JPA, Hibernate 등

## **📌 ORM의 장단점**

### **✔ 장점**

- 객체 지향적은 코드를 인해 비스니스 로직에 더 집중할 수 있게 함
    - ORM을 이용하면 SQL 쿼리가 아닌 메서드로 데이터를 조작할 수 있어 개발자가 객체 모델로 프로그래밍하는데 집중할 수 있도록 함
    - 선언문, 할당, 종료 같은 부수적인 코드가 없거나 줄어듦
    - 각종 객체에 대한 코드를 별도로 작성하기때문에 코드의 가독성을 올려줌
    - SQL의 절차적이고 순차적인 접근이 아닌, 객체지향적인 접근으로 인해 생산성이 증가
- 재사용 및 유지보수의 편리성이 증가
    - ORM은 독립적으로 작성되어있고, 해당 객체들을 재활용할 수 있다
    - 때문에 모델에서 가공된 데이터를 컨트롤러에 의해 뷰와 합쳐지는 형태로 디자인패턴을 견고하게 다지는데에 유리
    - 매핑 정보가 명확, ERD를 보는 것에 대한 의존도 낮춤
- DBMS에 대한 종속성이 줄어듦
    - 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하기때문에 RDBMS의 데이터 구조와 JAVA의 객체 지향 모델 사이의 간격을 좁힐 수 있음
    - 대부분 ORM 솔루션은 DB에 종속적이지 않음
        - 종속적이지 않다 = 구현 방법뿐만 아니라 많은 솔루션에서 자료형 타입까지 유효함
        - 프로그래머는 Object에 집중함으로 극단적으로 DBMS를 교체하는 거대한 작업에도 비교적 적은 리스크와 시간이 소요됨
        - 또한, 자바를 가공할경우 equals , hashCode의 오버라이드 같은 자바의 기능을 이용할 수 있고, 간결하고 빠른 가공이 가능함

### **✔ 단점**

- 완벽한 ORM으로만 서비스를 구현하기가 어렵다
    - 사용하기 편하지만,, 설계는 신중히!
    - 프로젝트 복잡성이 커질경우 난이도 올라감
    - 잘못 구현될 경우 속도 저하 및 심각할 경우 일관성이 무너질 수 있음
    - 자주 사용되는 대형쿼리는 속도를 위해 SP를 쓰는 등 별도의 튜닝이 필요함
    - DBMS의 고유 기능을 이용하기 어려움 ( 단점이라고 볼순 없음. 특정 DBMS의 고유 기능을 이용하면 이식성이 저하됨)
- 프로시저가 많은 시스템에서 ORM에서 객체지향적인 장점을 활용하기 어려움
    - 이미 프로시저가 많은 시스템에선 다시 객체로 바꿔야하며, 그 과정에서 생산성 저하, 리스크가 많이 발생할 수 있음

## **📌 The object-Relational Impedance Mismatch**

![스크린샷 2023-07-18 오후 10.33.39.png](%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A8%20%E1%84%86%E1%85%A2%E1%84%91%E1%85%B5%E1%86%BC%20(ORM)%20a68dffea33b642039aa919498e84661d/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-18_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.33.39.png)

**✔  세분성 Granularity**

**✔ 상속 Inheritance**

**✔ 일치 Identity**

**✔ 연관성 Associations**

**✔ 탐색/순회 Navigation**

### **✔ Association 연관성**

- Java에서 객체 참조 (Object References) : 방향성이 있다 ( Directional)
    - Java에서 양방향 관계가 필요한 경우, 연관을 두번 정의해야함
        - 즉, 서로 Reference를 가지고 있음
            
            ```java
            public class Employee { 
                  private int id; 
                  private String first_name; 
                  …
                  private Department department; // Employee -> Department
                  …
              }
            https://gmlwjd9405.github.io/2019/02/01/orm.html
            ```
            
- RDBMS와 외래키 ( Foreign Key)
    - FK와 테이블 Join은 관계형 데이터베이스 연결을 자연스럽게 만듦
        
        ![스크린샷 2023-07-18 오후 10.39.11.png](%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A8%20%E1%84%86%E1%85%A2%E1%84%91%E1%85%B5%E1%86%BC%20(ORM)%20a68dffea33b642039aa919498e84661d/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-18_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.39.11.png)
        
    - 방향성이 없음 (Direction-Less)
        
        ```sql
        INSERT INTO 
          EMPLOYEE(id, first_name, … ,department_id) // FK
          VALUES …
        ```
        

### ✏️ (1) One-to-One Relationship

- 예시, 각 학생은 고유한 주소를 갖고 있음
    1. RDBMS (방향성X)
    
    ![스크린샷 2023-07-18 오후 10.40.43.png](%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%80%E1%85%A8%20%E1%84%86%E1%85%A2%E1%84%91%E1%85%B5%E1%86%BC%20(ORM)%20a68dffea33b642039aa919498e84661d/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-18_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.40.43.png)
    
    - 각 Student의 recode는 서로 다른 Address record를 가리키고 이것은 일대일 매핑을 보여줌
    1. Java Object (방향성 O)

```java
public class Student {
 private long studentId;
 private String studentName;
 private Address studentAddress; // Student -> Address
 …
}
public class Address {
 private long addressId;
 private String street;
 private String city;
 private String state;
 private String zipcode;
 …
}
```

### ✏️ (2) One-to-Many Relationship

- 예시, 각 학생은 여러개의 핸드폰을 가질 수 있다고 하자
    1. RDBMS (방향성X)
        - 각 Student의 record는 여러개의 Phone record를 가리킬 수 있음 ( 일대다 매핑)
        - 해당 관계를 다른 테이블 ( Relational Model)로 만들 수 있음
            - One-to-Many 구성방법
                1. JOIN TABLE
                2. JOIN COLUMN
    2. Jaca Object (방향성O)
        
        ```java
        public class Student {
         private long studentId;
         private String studentName;
         private Set<Phone> studentPhoneNumbers; // Student -> Some Phones
         …
        }
        public class Phone {
         private long phoneId;
         private String phoneType;
         private String phoneNumber;
         …
        }
        ```
        

🔗 [https://gmlwjd9405.github.io/2019/02/01/orm.html](https://gmlwjd9405.github.io/2019/02/01/orm.html)

###