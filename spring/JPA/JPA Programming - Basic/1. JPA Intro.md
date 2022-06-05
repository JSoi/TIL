## JPA (Java Persistence API)

JPA는 인터페이스의 모음이다

**자바 진영의 ORM (Object-Relational Mapping) 기술 표준**

객체는 객체대로 설계, 관계형 데이터베이스는 관계형 데이터베이스대로 설계하면 ORM Framework가 중간에서 매핑해 준다

애플리케이션과 JDBC 사이에서 동작하는 것😃



#### JPA의 역할

- JPA가 멤버 객체를 분석해서 Query를 만들어 결과를 주고 받는다

- ResultSet 매핑

- 패러다임의 불일치를 해결한다.



#### JPA를 사용하는 이유?

1. 생산적이다. 마치 java collection을 쓰는 것과 같다

2. 유지보수가 좋다
   - 필드 변경시 모든 SQL를 수정해야하는데
   - JPA는 필드만 추가하며 SQL은 JPA가 처리한다.



#### JPA와 연관 관계, 객체 그래프 탐색

```
member.setTeam(team);
jpa.persist(member)
```

동일한 트랙잭션에서 조회한 앤티티는 같음을 보장한다.



#### JPA를 쓰면 성능이 떨어진다?

JPA 같은 중간 계층이 있다면 캐싱, 버퍼링을 지원하게 된다. 👉 최적화를 통해 성능을 끌어올릴 수도 있다.

같은 트랜잭션 안에서는 같은 앤티티를 반환 👉 조회 성능 향상

DB Isolation Level이 Read Commit이어도 애플리케이션에서 Repeatable Read 보장



#### 트랜잭션을 지원하는 쓰기 지연(버퍼링 기능) - Insert

트랜잭션을 커밋할 때까지 INSERT SQL을 모은다.

비슷한 쿼리를 메모리에 쌓아서 모아서 commit하게 된다. 

```
em.persist(memberA);
em.persist(memberB);
em.persist(memberC);
```





#### 지연 로딩과 즉시 로딩✔

```
Member member = memberDAO.find(memberId);
Team team = member.getTeam();
String teamName = team.getName();
```



**지연 로딩** 

객체가 실제 사용될 때 로딩 (SELECT * FROM MEMBER / SELECT * FROM TEAM) - 한 가지만 집중해서 쓸 때



**즉시 로딩** 

JOIN으로 한 번에 *연관된 객체까지* 미리 조회 (SELECT M.*, T.* FROM MEMBER JOIN TEAM ...) 두 엔티티를 같이 자주 쓸 때