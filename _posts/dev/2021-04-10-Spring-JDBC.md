---
title: "Spring JDBC"
categories:
  - dev
tags:
  - Java
  - Spring
---

# Spring JDBC
- JDBC를 사용하면 반복되는 지루한 개발요소가 있다. 

> JDBC 프로그래밍 순서
  1. JDBC 드라이버를 로딩한다.
  2. Connection 객체를 생성한다.
  3. PreparedStatement(Statement) 객체를 생성하고 SQL를 수행한다.
  4. SQL 문에 대한 결과물이 있다면 ResultSet 객체를 생성한다.
  5. Connection, PreparedStatement(Statement), ResultSet 객체를 close 한다.

- Spring JDBC는 이러한 반복적인 JDBC 저수준 구현 세부사항을 대신 처리해준다.
- Spring JDBC를 사용하여, 세부사항은 프레임워크에게 맡기고, 애플리케이션 개발자는 필요한 부분만 구현할 수 있게된다.

![2021-04-18 12 44 42](https://user-images.githubusercontent.com/37281119/115133528-ddd66380-a043-11eb-8454-dc92db9f4b5e.jpg)

# JdbcTemplate 클래스

- Spring JDBC 패키지중 하나인 **org.springframework.jdbc.core** 에 포함된 클래스다.

- `JdbcTemplate`를 사용해서 편하게 Jdbc 프로그래밍을 할 수 있다.
- 리소스 생성, 해지를 처리해서 연결을 닫는 것을 잊어 발생하는 문제 등을 피할 수 있도록 한다.
- 스테이먼트(Statement)의 생성과 실행을 처리한다.
- SQL 조회, 업데이트, 저장 프로시저 호출, ResultSet 반복호출 등을 실행한다.
- JDBC에서 `SQLException`이 발생하는 경우 런타임 예외인  `DataAccessException`로 포장해서 예외를 던진다. 

- JDBC를 직접 사용할때 나타나는 반복적인 코드를 **템플릿 메서드 패턴**이라는 디자인패턴으로 줄였기 떄문에 **JDBC Template**라는 이름이 붙었다.
- `JdbcTemplate`의 몇가지 메서드를 알아보자

## Select

#### public <T> T queryForObject(String sql, Class<T> requiredType)

```java
public int count() {
    String sql = "select count(*) from customers";
    return jdbcTemplate.queryForObject(sql, Integer.class);
}
```

#### public <T> T queryForObject(String sql, Class<T> requiredType, @Nullable Object... args)

```java
public String getLastName(Long id) {
    String sql = "select last_name from customers where id = ?";
    return jdbcTemplate.queryForObject(sql, String.class, id);
}
```

#### public <T> T queryForObject(String sql, RowMapper<T> rowMapper, @Nullable Object... args)

```java
public Customer findCustomerById(Long id) {
        String sql = "select id, first_name, last_name from customers where id = ?";
        return jdbcTemplate.queryForObject(sql, actorRowMapper,id);
    }
```

람다를 사용하면 아래와 같이 쓸 수 있다.

```java
    public Customer findCustomerById(Long id) {
        String sql = "select id, first_name, last_name from customers where id = ?";

        return jdbcTemplate.queryForObject(sql,
           (resultSet, rowNum) -> new Customer(resultSet.getString("first_name"),
                 resultSet.getString("last_name")), id);
    }
```

#### public <T> List<T> query(String sql, RowMapper<T> rowMapper)

```java
public List<Customer> findAllCustomers() {
    String sql = "select id, first_name, last_name from customers";

    return this.jdbcTemplate.query(sql,
        (resultSet, rowNum) -> new Customer(resultSet.getString("first_name"),
            resultSet.getString("last_name")));
}
```

#### public <T> List<T> query(String sql, RowMapper<T> rowMapper, @Nullable Object... args)

```java
 public List<Customer> findCustomerByFirstName(String firstName) {
        String sql = "select id, first_name, last_name from customers where first_name = ?";
        return this.jdbcTemplate.query(sql,
            (resultSet, rowNum) -> new Customer(resultSet.getString("first_name"),
                resultSet.getString("last_name")), firstName);
 }
```

## insert

#### public int update(String sql, @Nullable Object... args)

```java
public void insert(Customer customer) {
    String sql = "insert into customers (first_name, last_name) values (?, ?)";
    jdbcTemplate.update(sql, customer.getFirstName(), customer.getLastName());
}
```

## delete

#### public int update(String sql, @Nullable Object... args)

```java
public int delete(Long id) {
    String sql = "delete from customers where id = ?";
    return jdbcTemplate.update(sql, id);
}
```

# NamedParameterJdbcTemplate 클래스

- JdbcTemplate에서는 SQL문에 인자를 전달하기 위해 `?` 를 사용한다.
- NamedParameterJdbcTemplate에서는 `?` 대신 `파라미터명` 을 사용할 수 있다.

#### public <T> T queryForObject(String sql, SqlParameterSource paramSource, Class<T> requiredType)

```java
public int useMapSqlParameterSource(String firstName) {
    String sql = "select count(*) from customers where first_name = :first_name";
    SqlParameterSource namedParameters = new MapSqlParameterSource("first_name", firstName);
    return namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

#### public <T> T queryForObject(String sql, SqlParameterSource paramSource, Class<T> requiredType)

```java
public int useBeanPropertySqlParameterSource(Customer customer) {
    String sql = "select count(*) from customers where first_name = :firstName";
    SqlParameterSource namedParameters = new BeanPropertySqlParameterSource(customer);
    return namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

# SimpleJdbcInsert 클래스

- `SimpleJdbcInsert` 를 사용해서 SQL문 작성 없이 쉽게 insert 할 수 있다.
- 그냥 insert만 하고 싶다면 `execute` 메서드를, insert후 key값을 받아오고 싶으면 `executeAndReturnKey`를 사용하면 된다.

```java
public SimpleInsertDao(DataSource dataSource) {
    this.simpleJdbcInsert = new SimpleJdbcInsert(dataSource)
            .withTableName("customers") // 테이블 지정
            .usingGeneratedKeyColumns("id"); // insert시 id가 자동생성 되도록 설정
}
```

#### executeAndReturnKey (Map사용)

```java
public Customer insertWithMap(Customer customer) {
    Map<String, Object> parameters = new HashMap<>(2);
    parameters.put("first_name",customer.getFirstName());
    parameters.put("last_name",customer.getLastName());
    Long id = simpleJdbcInsert.executeAndReturnKey(parameters).longValue();
    return new Customer(id, customer.getFirstName(), customer.getLastName());
}
```

#### executeAndReturnKey (SqlParameterSource 사용)

```java
public Customer insertWithBeanPropertySqlParameterSource(Customer customer) {
    SqlParameterSource parameters = new BeanPropertySqlParameterSource(customer);
    Long id = simpleJdbcInsert.executeAndReturnKey(parameters).longValue();
    return new Customer(id, customer.getFirstName(), customer.getLastName());
}
```

# 참고

- https://velog.io/@seculoper235/JDBC-5편-jdbcTemplate
- https://www.boostcourse.org/web316/lecture/20660?isDesc=false
- https://www.inflearn.com/course/스프링-입문-스프링부트/lecture/49596?tab=curriculum