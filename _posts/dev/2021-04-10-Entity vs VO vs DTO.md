---
title: "Entity vs VO vs DTO"
categories:
  - dev
tags:
  - Java
---

# Entity
- Entity는 RDB 테이블내에 존재하는 컬럼만을 필드로 갖는 클래스다.
- Entity 클래스는 상속을 받거나 구현체여서는 안된다.

# VO(Value Object)
- VO는 이름 그대로 값 객체라는 의미를 가진다.
- 비지니스 로직을 포함할 수 있다.
- 어떤 두 VO의 내부 필드값이 모두 같다면 두 VO는 같은 객체로 판별된다. (equals()와 hashcode()를 오버라이딩 해야한다.)
- 불변 객체다. (Read-Only)

# DTO(Data Transfer Object)
- DTO는 계층(레이어)간 데이터 교환을 위한 객체이다.
- 보통은 로직을 가지지 않으며 getter, setter 메소드만 갖는다. 
- 가변 객체다.
- ex) 어떤 객체의 특정 필드들만 추려서 JSON 형식으로 전송해야하는 경우 데이터 가공 처리를 위해 DTO를 사용한다.

## 참고
- https://webdevtechblog.com/entity-vo-dto-666bc72614bb