---
title: "컨테이너와 IoC/DI"
categories:
  - dev
tags:
  - Ioc/DI 
  - Spring
---

# 컨테이너(Container)

- 프레임워크 기반의 프로그램은 프레임워크 자신이 프로그램 실행 흐름을 제어하는 주체가 되어, 필요할 때마다 애플리케이션 코드를 호출하여 사용한다.
- 프레임워크에서 이 제어권을 가지는 것을 컨테이너라고 부른다. 
- 객체에 대한 제어권이 개발자로부터 컨테이너로 넘어가면서 객체의 생명주기 관리를 컨테이너가 도맡아서 한다. 
- 이를 일반적인 제어권의 흐름이 바뀌었다고 하여 Ioc(Inversion of Control : 제어의 역전)라고 부른다. 

## WAS의 Servlet 컨테이너

- 예를들어 Servlet을 실행해주는 WAS는 Servlet 컨테이너를 가지고 있다고 말한다.
- WAS는 웹 브라우저로부터 서블릿 URL에 해당하는 요청을 받으면 해당 서블릿을 메모리에 올리고 실행한다.
- 서블릿 클래스를 구현한 것은 프로그래머이지만, 실제로 서블릿 객체를 생성하여 메모리에 올리고 실행하는 것은 WAS의 Servlet 컨테이너다.
- Servlet 컨테이너는 동일한 서블릿에 대한 요청을 받으면 메모리 상에 올라가있는 서블릿을 실행하여 그 결과를 웹 브라우저에 전달한다.

# Ioc(Inversion of Control)/DI(Dependency Injection)

- DI는 의존성 주입이란 뜻을 가지고 있으며, 클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것을 말한다.
- 예를들어 A객체가 동작하기 위해서는 A객체가 B객체를 가지고 있어야 하는 상황이다. 이때 이 B객체를 프로그래머가 작성한 애플리케이션 코드로 직접 생성하는 것이 아니라 컨테이너가 대신 생성해 주는 것이다.
- 개발자들은 제어를 담당할 필요없이 빈 설정 파일에 의존 관계 정보만 추가해주면 된다. 그리고 컨테이너는 이 정보를 기반으로 프로그램 실행시에 동적으로 객체를 만들어서 의존관계를 주입한다.
- 다시 말해 DI는 컨테이너가 프로그램 실행 흐름의 주체가 되어서 애플리케이션 코드에 의존관계를 주입해주는 것이다. 이를 제어의 역전(Ioc)라고 한다.

## Ioc/DI가 적용되지 않은 경우

### 애플리케이션 코드

```java
package kr.co.example;

public class Person{
	private Phone phone;
	
	public Person(){
		phone = new FeaturePhone();
	}
}
```

- Ioc/DI가 적용되지 않는 경우, Phone 인터페이스를 구현하는 FeaturePhone 클래스를 new 키워드를 통해 직접 생성해서 초기화 하고 있다. 
- 이런 경우 동적으로 새로운 구현 클래스를 적용하기가 어렵다. 
- 만약 Ioc/DI를 사용한다면, SmartPhone 클래스로 바꾸고 싶을때 빈 설정 정보만 수정해주면 된다. 

## Ioc/DI가 적용된 경우

### 컨테이너 빈 설정 정보

```xml
<beans>
  <bean id = "phone" class="package kr.co.example.Phone">
  <bean id = "person" class="package kr.co.example.Person">
  	<property name="phone" ref="phone"/>
  </bean>
</beans>
```

### 애플리케이션 코드

```java
package kr.co.example;

public class Person{
	private Phone phone;
	
	public Person(Phone phone){
		this.phone = phone;
	}
}
```

- 빈 설정 정보를 바탕으로 사용할 객체들을 컨테이너에 등록한다. 
- 프로그램을 실행하면 컨테이너는 애플리케이션 코드에 등록한 객체를 넣어준다.
- 즉, Person 객체의 생성자 매개변수로 Phone 객체를 생성해서 넣어준다.
- 이렇게 하면 Phone 인터페이스를 구현하는 클래스가 애플리케이션에 등록하지 않는다. 따라서 동적으로 구현 클래스를 마음대로 바꿀 수 있다.

- Ioc/DI를 사용하면 객체를 생성할 때 해당 객체가 참조하고 있는 다른 객체에 대한 종속성을 애플리케이션 코드 외부에서(컨테이너가) 설정하게 함으로써 결합도(Coupling)를 낮추며 유연성과 확장성을 향상 시킬 수 있다는 장점이 있다.

>  소프트웨어 공학에서, **결합도**(coupling) 또는 **의존도**는 어떤 모듈이 다른 모듈에 의존하는 정도를 나타내는 것이다.

# Spring Container

- 스프링 Ioc 컨테이너가 관리하는 객체를 빈(Bean)이라고 부른다.
- 스프링에서는 이 빈(Bean)들을 관리한다는 의미로 컨테이너를 빈 팩토리(Bean Factory)라고 부른다.
- 스프링의 컨테이너는 단순한 DI 작업뿐만 아니라 더 많은 일을 한다. 그래서 DI 기능에 엔터프라이즈 애플리케이션을 개발하는데 필요한 여러 가지 컨테이너 기능을 추가하여 애플리케이션 컨텍스트(Application Context)라고 부르기도 한다.
- 스프링에서는 xml에 Configuration 정보를 담아 컨테이너를 구성할 수 있다.

# 참고

- https://www.nextree.co.kr/p11247/