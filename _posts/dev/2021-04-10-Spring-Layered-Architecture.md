---
title: "Spring Web Layered Architecture"
categories:
  - dev
tags:
  - Java
  - Spring
---

![spring-web-app-architecture](https://user-images.githubusercontent.com/37281119/115111148-cfdc0080-9fb9-11eb-9366-af295c852945.png)

# Web Layer
- 컨트롤러(@Controlle)와 JSP/Freemarker 등의 뷰 템플릿 영역이다.
- 필터(@Filter), 인터셉터, 컨트롤러 어드바이스(@ControllerAdvice) 등 외부 요청과 응답에 대한 전반적인 영역이다.

# Service Layer
- 서비스(@Service) 영역이다.
- 일반적으로 Controller와 Dao의 중간 영역에서 사용된다.
- @Transactional이 사용되어야 하는 영역이기도 하다.

# Repository Layer
- Database와 같은 데이터 저장소에 접근하는 영역이다.
- Dao 영역이라고 생각하면 된다.

# Dtos

- Dto(Data Transfer Object)는 계층 간에 데이터 교환을 위한 객체를 이야기한다.
- 예를들어 뷰 템플릿 엔진에서 사용될 객체나 Repository Layer에서 결과로 넘겨준 객체 등이 이들을 이야기 한다.

# Domain Model

- 도메인이라 불리는 개발 대상을 모든 사람이 동일한 관점에서 이해할 수 있고 공유할 수 있도록 단순화시킨 것을 도메인 모델이라고 한다.
- @Entity가 사용되는 영역이다. 
- 도메인 모델이 데이터베이스의 테이블과 관계가 있어야만 하는 것은 아니다.
- VO 처럼 값 객체들도 이 영역에 해당하기 때문이다. 


# 참고
- https://book.naver.com/bookdb/book_detail.nhn?bid=15871738

