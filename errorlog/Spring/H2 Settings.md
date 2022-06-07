## Database "mem:springcoredb" not found, and IFEXISTS=true, so we cant auto-create it

### 원인

User가 H2상에서 Reserved Word란다.

User 테이블명을 바꾸면 되긴 할 텐데, 나는 그러지 않았다 :sweat:

[[참고사이트](https://github.com/h2database/h2database/issues/3363)]

### 해결방법

```properties
spring.datasource.url=jdbc:h2:mem:springcoredb;MODE=MySQL;NON_KEYWORDS=USER
```