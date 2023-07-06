# JPA 사용시 주의사항

**엔티티 매니저 팩토리**는 하나만 생성해서 애플리케이션 전체에서 공유

**엔티티 매니저**는 쓰레드간에 공유 X (사용하고 버려야 한다).

**JPA의 모든 데이터 변경은 트랜잭션 안에서 실행**

**EntityManagerFactory** 안에 있는 **EntityManager**를 통해서 작업을 해야한다

모든 데이터의 변경 작업은 **EntityTransaction **안에서 일어나야 한다.

- ```commit```을 꼭 해주어야 하고 자원을 다쓰면 ```EntityManager```를 닫아야한다.

```java
// 여기서 name은 persistence.xml에 작성한 유닛 네임
EntityManagerFactory emf = Persistence.createEntityManagerFactory("name");
EntityManager em = emf.createEntityManager();
EntityTransaction tx = em.getTransaction();
// 트랜젝션을 시작하면 시작한다고 써야함
tx.begin();
try{
    // 완료하면 commit을 해주어햐함
    tx.commit();
} catch (Exception e){
    // 에러발생시 롤백
    tx.rollback();
} finally {
    // 마무리 단계에선 엔티티매니저를 닫아줘야한다.
    em.close();
}
// 내부적으로 릴리즈가 되기위해선 닫아줘야한다.
emf.close();
```



---



#### JPQL

---

- **JPA**를 사용하면 **엔티티 객체**를 중심으로 개발
- 문제는 **검색 쿼리**
- 검색을 할 때도 **테이블이 아닌 엔티티 객체**를 대상으로 검색
- 모든 DB 데이터를 **객체**로 변환해서 검색하는 것은 불가능
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 **검색 조건이 포함된 SQL**이 필요

- **JPA**는 **SQL을 추상화**한 **JPQL**이라는 **객체 지향 쿼리** 언어 제공
- SQL과 문법 유사, ```SELECT```, ```FROM```, ```WHERE```, ```GROUP BY```, ```HAVING```, ```JOIN``` 지원
- **JPQL**은 **엔티티 객체**를 대상으로 쿼리
- **SQL은 데이터베이스 테이블**을 대상으로 쿼리

