# 주요 공부내용 정리

### JPA 구동 방식

<img width="438" alt="스크린샷 2023-03-22 오전 12 30 33" src="https://user-images.githubusercontent.com/48097396/226656617-e96f7efb-c938-4021-a2c1-b3fbd7bb5110.png">

Persistence -> EntityManagerFactory -> EntityManager 생성

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.Persistence;

EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello");
EntityManager em = emf.createEntityManager();
```

### JPA 주의

- EntityManagerFactory는 하나만 생성
- EntityManager는 요청마다 생성 -> 즉, **스레드간 공유 절대 금지!**
- 모든 데이터 변경은 트랜잭션 내에서 실행해야 한다.

### JPQL 장점

SQL과는 무엇이 다른가?
- SQL은 DB 테이블을 대상으로 쿼리

**ENTITY 객체를 대상으로 쿼리**

예) pagination 시, DB 방언을 몰라도 쉽게 구현 및 변경 할 수 있음

```java
List<Member> result = em.createQuery("select m from Member as m", Member.class)
        .setFirstResult(5)
        .setMaxResults(8)
        .getResultList();
```
