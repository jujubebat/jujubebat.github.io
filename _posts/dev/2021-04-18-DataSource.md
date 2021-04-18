---
title: "ConnectionPool과 DataSource"
categories:
  - dev
tags:
  - Java
  - Spring 
---

# ConnectionPool(DBCP)
![9GeMX](https://user-images.githubusercontent.com/37281119/115138689-957d6c80-a068-11eb-8e67-f64b9ee4785b.jpg)
- 클라이언트의 요청으로 인해 매번 새로운 DB 연결이 발생한다면 성능 저하가 발생할 수 있다. 
- 매번 DB 커넥션 객체를 생성하는 것은 큰 비용이기 때문이다.
- 미리 DB 커넥션 객체들을 만들어서 **Connection Pool** 이란 곳에 담아두고, 연결이 필요할 때마다 가져다 쓰고 반환하는 식으로 하면 이러한 비용을 줄일 수 있다. 
- **Connection Pool** 을 사용하면 미리 DB 커넥션을 만들어두기 때문에 매 DB 접속마다 새로운 커넥션 객체를 생성하고 닫는 시간이 소모 되지 않는다는 장점이 있다.
- 만약 **Connection Pool** 에 남아 있는 DB 커넥션 객체가 없다면 해당 요청은 대기 상태로 되고, DB 커넥션 객체가 반환되면 순서대로 할당해준다. 

# DataSource

-  Java의 javax.sql.DataSource 인터페이스는 Connection Pool을 관리하고 사용할 수 있게 한다.
- DataSource 구현체는 아래와 같은 것들이 있다.
  - Tomcat JDBC Connection Pool
  - HikariCP 
  - Commons DBCP
  - Commons DBCP2
- JDBC API에서는 아래와 같이  `DriverManager`말고도 `DataSource`를 이용해서 DB 커넥션을 가져올 수 있다.

``` java
Connection conn = null;
try { 
conn = dataSource.getConnection(); 
...
```

- 스프링 JDBC의 JdbcTemplate, NamedParameterJdbcTemplate, SimpleJdbcInsert는 내부적으로 DataSource 객체를 사용하여 DB 연결을 구현한다. 

# 참고

- https://www.boostcourse.org/web316/lecture/254337/?isDesc=false
- https://brownbears.tistory.com/289
- https://jaehoney.tistory.com/33