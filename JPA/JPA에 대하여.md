# JPA

##### JPA ?

- Java Persistence API

- 자바 진영의 **ORM** 기술 표준

  - **ORM ?**
    - Object-relational mapping(객체 관계 매핑)
    - 객체는 객체대로 설계
    - 관계형 데이터베이스는 관계형 데이터베이스대로 설계
    - ORM 프레임워크가 중간에서 매핑
    - 대중적인 언어에는 대부분 ORM 기술이 존재

- **JPA**는 애플리케이션과 **JDBC** 사이에서 동작

  

  

  ![image-20230321214935045](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321214935045.png)

  - **JPA** 동작 - 저장

    ![image-20230321215035366](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321215035366.png)

    

    - JPA는 알아서 Member 객체를 분석하고 Insert Query생성하고 JDBC API 사용해서 DB Insert Query 까지 다 날려줍니다.
    - 가장 중요한 패러다임 불일치도 해결해줍니다.
    - 자바 컬렉션에 저장하듯이 한 줄로 해결이 됩니다.

  

  - **JPA**  동작 - 조회

    ![image-20230321215916582](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321215916582.png)

    

    - JPA에게 id를 던져주면 Select Query를 다 만들고 JDBC API 사용하고 ResultSet을 다 매핑해주고 패러다임 불일치까지 해결해줍니다.

    