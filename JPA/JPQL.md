# JPQL

- **JPA**를 사용하면 **엔티티 객체**를 중심으로 개발
- 문제는 **검색 쿼리**
- 검색을 할 때도 **테이블이 아닌 엔티티 객체**를 대상으로 검색
- 모든 DB 데이터를 **객체**로 변환해서 검색하는 것은 불가능
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 **검색 조건이 포함된 SQL**이 필요

- **JPA**는 **SQL을 추상화**한 **JPQL**이라는 **객체 지향 쿼리** 언어 제공
- SQL과 문법 유사, ```SELECT```, ```FROM```, ```WHERE```, ```GROUP BY```, ```HAVING```, ```JOIN``` 지원
- **JPQL**은 **엔티티 객체**를 대상으로 쿼리
- **SQL은 데이터베이스 테이블**을 대상으로 쿼리

```java
// 간단한 사용법
List<Member> result = em.createQuery("select m from Member as m", Member.class)
							// 페이징 함수 setFirstResult : 몇번부터 시작할껀지, SetMaxResults : 몇개 가지고 올건지
							.setFirstResult(0)
							.setMaxResults(1)
							.getResultList();
```

