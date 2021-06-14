---
title: "Java와 Spring의 데이터 접근 기술"
categories:
  - dev
tags:
  - Java
  - Spring
---

# JDBC(Java Database Connectivity)

- 자바로 데이터베이스에 접속할 수 있게 해주는 자바 API다. 

## JDBC 작업 순서

1. DB 연결을 위한 Connection을 가져온다.

2. SQL을 담은 Statement(또는 PreparedStatement)를 만든다.

3. 만들어진 Statement를 실행한다.

4. 조회의 경우 SQL 쿼리의 실행 결과를 ResultSet으로 받아서 정보를 저장할 오브젝트(여기서 는 User)에 옮겨준다.

5. 작업 중에 생성된 Connection, Statement, ResultSet 같은 리소스는 작업을 마친 후 반드시 닫아준다.

6. JDBC API가 만들어내는 예외exception를 잡아서 직접 처리하거나, 메소드에 throws를 선언 해서 예외가 발생하면 메소드 밖으로 던지게 한다.

### 샘플 코드 

- 아래 코드는 users 테이블의 레코드 수 조회 쿼리를 실행하는 jdbc 코드다.
- DB 접근을 위한 Connection, PreparedStatement, ResultSet와 같은 리소스들은 보통 풀(Pool) 방식으로 운영된다.
- 미리 정해진 풀 안에 리소스 객체들을 미리 만들어 둔 다음 필요할때 리소스들을 할당해주고, 사용을 마치면 다시 풀로 반환 받는다.
- 요청이 매우 많은 서버환경에서는 매번 새로운 리소스를 생성하는 대신 풀에 미리 만들어둔 리소스를 돌려가며 사용하는 편이 훨씬 유리하다. 
- 사용한 리소스는 pool로 다시 반환해야 한다. 그렇지 않으면 풀에 있는 리소스가 고갈되고 서버에서는 리소스가 꽉 찼다는 에러가 나면서 서비스가 중단될 것이다. 
- 아래 코드를 보면 할당 받은 리소스를 반드시 닫아주기 위해 **복잡한 예외 처리 로직**이 등장하는 것을 볼 수 있다. 

```java
public int getCount() throws SQLException {
        Connection c = null;
        PreparedStatement ps = null;
        ResultSet rs = null;

        try {
            c = dataSource.getConnection();
            ps = c.prepareStatement("select count(*) from users");

            // ResultSet 도 다양한 SQLException 이 발생할 수 있는 코드이므로 try 블록 안에 둬야 한다.
            rs = ps.executeQuery();
            rs.next();
            return rs.getInt(1);
        } catch (SQLException e) {
            throw e;
        } finally {
            // 만들어진 ResultSet을 닫아주는 기능. close()는 만들어진 순서의 반대로 하는 것이 원칙이다.
            if (rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                }
            }
            if (ps != null) {
                try {
                    ps.close();
                } catch (SQLException e) {
                }
            }
            if (c != null) {
                try {
                    c.close();
                } catch (SQLException e) {
                }
            }
        }
    }
```

# Spring JDBC

- 앞서 살펴본 코드와 같이 JDBC API를 사용하면 복잡한 예외 처리 로직이 반복된다. 변화되는 부분은 SQL문을 실행하는 try문 뿐이다.
- JDBC API를 사용하면 위와 같은 복잡한 예외 처리 로직을 반복 구현하지 않아도 된다. 
- JdbcTemplate 클래스에는 위와같은 반복되는 예외 처리 로직을 미리 갖고 있다. 이를 **템플릿**이라고 한다. 
- 그리고 try 문안에서 실행되는 로직로 미리 갖고 있다. 이를 **콜백**이라고 한다. 
- 우리가 JdbcTemplate 메서드에 SQL 문을 전달하면 JdbcTemplate는 내부적으로 SQL문 실행에 대한 적절한 콜백을 템플릿으로 전달해서 실행한다. 이러한 동작 방식을 **템플릿/콜백 패턴**이라고 한다. 전략 패턴의 컨텍스트와 전략이 같은 곳에 위치 하는 구조라고 생각하면 된다. 

- 또한 Spring JDBC는 JDBC가 던지는 `SQLException` 을 런타임 예외인  `DataAccessException`로 포장해서 던진다. 

# Spring Data JDBC 

# Hibernate

# JPA

# 참고
- https://velog.io/@seculoper235/JDBC-5편-jdbcTemplate
- https://www.boostcourse.org/web316/lecture/20660?isDesc=false
- https://www.inflearn.com/course/스프링-입문-스프링부트/lecture/49596?tab=curriculum