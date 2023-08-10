# MVC1 패턴과 MVC2패턴의 차이점

태그: 디자인 패턴
부가 태그: 내용정리

## #Spring의 MVC패턴

> 스프링 프레임워크는 MVC 패턴을 준수! -
> 
> - Model
>     - 어플리케이션의 정보나 데이터, DB
> - View
>     - 사용자에게 보여지는 화면, UI를 말함 - 모델로부터 정보를 얻고 표시
> - Controller
>     - 데이터와 비즈니스 로직사이의 상호 동작 관리
>     - 모델과 뷰를 동작함 - View와 Model이 직접적인 상호 소통을 하지 않도록 관리

![1920px-ModelViewControllerDiagram2.svg.png](MVC1%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%80%E1%85%AA%20MVC2%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%B4%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%A5%E1%86%B7%20129fa82a69ae469b93bffd0b5525c14e/1920px-ModelViewControllerDiagram2.svg.png)

## **📌 MVC1**

![rzhzcZc.png](MVC1%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%80%E1%85%AA%20MVC2%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%B4%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%A5%E1%86%B7%20129fa82a69ae469b93bffd0b5525c14e/rzhzcZc.png)

- 뷰, 컨트롤러를 담당하는 JSP가 담당하는 형태
    - 하나로 유저의 요청과 응답을 처리함
    
    → 재사용성 떨어지며 읽기도 힘들어짐  **`유지보수의 문제 발생!`**
    
    <aside>
    ✏️ JSP : HTML 코드에 JAVA 코드를 넣어 동적웹페이지를 생성하는 웹어플리케이션 도구임
    
    </aside>
    

## **📌 MVC2**

![keastvz.png](MVC1%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%80%E1%85%AA%20MVC2%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%B4%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%A5%E1%86%B7%20129fa82a69ae469b93bffd0b5525c14e/keastvz.png)

- 요청을 하나의 컨트롤러가 받음
- 컨트롤러와 뷰가 분리되어있어, 단점을 보완할 수 있고 수정할 부분만 고치면 되기때문에 유지보수도 편함
- `해당 패턴 적용 사례 - 스프링!`

## **✔ Spring의 MVC2**

![blr7x6q.png](MVC1%20%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%80%E1%85%AA%20MVC2%E1%84%91%E1%85%A2%E1%84%90%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%B4%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%A5%E1%86%B7%20129fa82a69ae469b93bffd0b5525c14e/blr7x6q.png)

- 유저의 요청을 받는 Dispathcer Servlet = Front Controller 역할 수행

<aside>
✏️ Front Controller란,

유저(클라이언트)의 모든 요청을 받고, 그 요청을 분석하여 세부 컨트롤러에게도 필요한 작업을 나눠줌

</aside>

🔗  [https://chanhuiseok.github.io/posts/spring-3/](https://chanhuiseok.github.io/posts/spring-3/)