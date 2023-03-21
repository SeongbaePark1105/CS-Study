# JPA와 모던 자바 데이터 저장 기술



#### 객체와 관계형 데이터베이스의차이

1. 상속
2. 연관관계
3. 데이터 타입
4. 데이터 식별 방법

- ##### 상속

  ![image-20230321211918671](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321211918671.png)

  - 관계형 데이터베이스는 기본적으로 상속은 없다. 있긴 한데 완전히 똑같지는 않다.
  - 슈퍼타입, 서브타입 관계로 해결



- ##### 연관관계

  - 계층형 아키텍처 진정한 의미의 `계층 분할`이 어렵다.
    - 물리적으로는 분할이 되어 있으나 논리적으론 엮여있다.
  - 객체답게 모델링 할수록 매핑 작업만 늘어난다.

  ![image-20230321212438659](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321212438659.png)

  - 객체를 테이블에 맞추어 보통 모델링 한다.

    ![image-20230321212554361](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321212554361.png)

  - 객체다운 모델링

    ![image-20230321212725982](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321212725982.png)

    - 문제가 있음

      - 이렇게 할 때 Data에 Insert하기 많이 힘들어짐

        ![image-20230321212812687](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321212812687.png)

        ![image-20230321213022788](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213022788.png)

    - DB에 보관하는 것이 아니라 자바 컬렉션에 관리 한다면 ?

      ![image-20230321213102547](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213102547.png)

  - 객체 그래프 탐색

    - 객체는 자유롭게 객체 그래프를 탐색할 수 있어야 한다.

      ![image-20230321213228543](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213228543.png)

    - SQL은 처음 실행하는 SQL에 따라 탐색 범위 결정

      ![image-20230321213307119](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213307119.png)

      - 이럴 경우 엔티티 신뢰 문제가 생긴다.

        ![image-20230321213434843](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213434843.png)

  - 비교하기

    ![image-20230321213826001](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213826001.png)

    - 데이터는 같지만 각자 다른 인스턴스이기 때문에 다르다.

    

  - 비교하기 - 자바 컬렉션에서 조회

    ![image-20230321213943396](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230321213943396.png)

  - 객체를 자바 컬렉션에 저장 하듯이 DB에 저장할 수는 없을까 ?

    - 이 문제를 해결하는 것이 **JPA**