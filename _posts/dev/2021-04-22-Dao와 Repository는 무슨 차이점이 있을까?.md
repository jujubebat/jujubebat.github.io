---
Atitle: "Dao와 Repository는 무슨 차이점이 있을까?"
categories:
  - dev
tags:
  - Java
  - Spring
---

[DAO와 REPOSITORY 논쟁](http://aeternum.egloos.com/1160846)을 읽고 요약정리한 글입니다. 

# DAO
- DAO는 도메인 레이어와 퍼시스턴스 레이어를 명확하게 분리하기 위해 제시 되었다.
- DAO는 비지니스 로직과 퍼시스턴스 로직의 명확한 분리를 위해 퍼시스턴스 로직을 캡슐화하고 도메인 레이어에 객체-지향적인 인터페이스를 제공한다.
- DAO가 비록 객체 지향적인 인터페이스를 제공하려는 의도를 가지고 있더라도, 실제 개발 시에는 하부의 퍼시스턴스 메커니즘에 데이터베이스라는 사실을 숨기려고 하지 않는다.
- DAO의 인터페이스는 데이터베이스의 CRUD 쿼리와 1대1 매칭되는 세밀한 단위의 오퍼레이션을 제공한다. (Repository가 제공하는 오퍼레이션보다 세밀하다.)
- DAO는 퍼시스턴스 레이어에 속한다. 반면 REPOSITORY의 인터페이스는 도메인 레이어에 속한다. 
- DAO는 데이터베이스 테이블 별로 생성되는 것이 일반적이다. 
- 따라서 DAO 식별 과정은 도메인 규칙 보다는 데이터베이스 테이블의 단위에 영향을 받는 경향이 강하다. (DAO는 인터페이스 차원에서는 데이터베이스에 대한 의존도를 캡슐화할 수 있지만, 테이블 변경에 대해서는 그렇지 않음.)

# Repository
- Repository는 도메인 레이어에 객체 지향적인 컬렉션 관리 인터페이스를 제공하기 위해 사용된다.
- 하나의 단위로 생각할 수 있는 객체들의 군집인 Aggregate별로 하나의 Repository를 사용한다.
- 예를들어 `Order` 객체와 `OrderLineItem` 객체가 하나의 Aggregate이고, `OrderLineItem`이 `Order`에 종속된다면, `OrderRepositry` 사용해서 모든 `Order`와 `OrderLineItem` 객체에 대한 컬렉션을 관리한다.
- Repository는 특정 객체 집합의 가상적인 메모리 컬렉션을 관리한다. 
- 시스템에 1억건의 주문 정보가 존재한다면 `OrderRepository`는 1억건의 `Order` 객체와 그와 관련된 `OrderLineItem` 객체가 메모리 내에 로드되어 있다고 가정한다. 
- 클라이언트는 `OrderRepository`를 사용해서 `Order` 객체 컬렉션에 `Order` 객체를 추가하거나, 제거하거나, 카운트를 셀 수 있어야한다. 
- Repository는 퍼시스턴스 메커니즘에 대한 어떤 가정도 하지 않는다. 
- Repository를 사용할 때는 이미 모든 `Order` 객체와 `OrderLineItem`이 메모리에 로드되어 있다고 가정하고 메모리에 로드된 특정 객체, 객체 집합, 전체 객체에 접근하기 위해 Repository를 사용한다.
- Repository 자체는 도메인 모델에 속한다. 하지만 Repository 내부에서는 Aggregate 생명 주기를 관리하기 위해 하부의 퍼시스턴스 메커니즘을 사용할 필요가 있다. (예를들어 SQL문과 SQL문을 실행하는 로직)
- 하지만 Repository에 퍼시스턴스 로직이 포함될 경우 Repository를 직접 사용하는 도메인 객체 역시 퍼시스턴스 매커니즘에 의존하게 되는 부작용이 발생한다.
- 이를 해결하기 위한 최선의 방법은 Repository를 인터페이스와 구현부로 분리한 후 인터페이스는 도메인 레이어에 속하도록 하고, 구현부는 퍼시스턴스 레이어에 속하도록 하는 것이다. 
- Repository에서 제공하는 하나의 오퍼레이션이 DAO의 여러 오퍼레이션에 매핑되는 것이 일반적이다.
- Repository의 인터페이스는 연관 객체의 묶음인 Aggregate에 포함된 특정 Entity인 Aggregate Root와 관련된 오퍼레이션만을 포함하며, 테이블 변경에 대해서 투명하다.
- Repository는 도메인 모델링 단계에서 Aggregate를 도출하는 과정에서 자동으로 식별된다. (Repository 식별 과정은 도메인 규칙에 영향을 받는다.)
