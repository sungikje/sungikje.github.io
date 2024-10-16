---
title: Spring Web Programming 2장
parent: Web
layout: home
nav_order: 14
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# context
`org.springframework.context.ApplicationContext` 인터페이스는 1장에서 언급한 스프링 IoC 컨테이너를 표현

해당 인터페이스를 구현한 스프링 애플리케이션 컨텍스트 객체는 스프링 빈의 인스턴스를 생성하고 관리하는 기능을 제공하며 POJO(Plain Old Java Object)로 정의된다

<br><br><br><br><br>

# Spring Bean
`스프링 빈(Spring bean)`은 스프링 프레임워크가 관리하는 클래스의 인스턴스를 말한다
  + 어노테이션(annotation)을 사용해 자바 클래스에 스프링 빈을 설정하는 방법
  ```java
  // bean 설정 클래스
  @Configuration
  public class AppConfig {
  
  }
  
  // bean 설정 클래스 객체 생성
  ... {
  	ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class)
  }
  ```
  + xml 파일에 설정하는 방식, 그루비(Glovvy) 언어로 설정하는 방식 등 다양한 방법 존재
  ```java
  // xml file 생성 후 해당 xml file 이용해 객체 생성(beans.xml 파일에 bean 설정 존재)
  ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
  ```
  
  ```java
  // DSL(Groovy Bean Definition DSL)
  // bean 설정 file, groovy 언어로 정의된다
  beans {
  
  }
  
  ... {
  	ApplicationContext context = new GenericGroovyApplicationContext("beans.groovy")
  }
  ```
  
  ```java
  // xml, DSL(groovy) 사용하는 경우 추가로 사용 가능한 방법
  GenericApplicationContext context = new GenericApplicationContext();
  new XmlBeanDefinitionReader(context).loadBeanDefinitions("beans.xml");
  context.refresh();
  ```
  + xml, Glovvy 방식은 main 디렉토리 밑에 resources 서브 디렉토리에 위치하는게 좋다

`groovy` : 자바에 파이썬, 루비, 스몰토크 등의 특징을 더한 동적 객체 지향 프로그래밍 언어
<br>

## vs Java Bean
`Spring bean`은 IoC 컨테이너 즉, 애플리케이션 컨텍스트 안에서 생성되고 관리되는 자바 클래스의 인스턴스
`Java bean`은 new 연산자를 사용하여 인스턴스를 생성하는 빈이다.
  + `Java bean`의 경우 Ioc 컨테이너 안에서 관리되지 않는다

모든 `bean`을 IoC 컨테이너에서 관리할 수는 있지만 이렇게 되면 IoC 과부하 걸림
  + 때문에 IoC 내부에 위치해야 될 `bean`과 외부에 위치해야 될 `bean` 구분 필요

## 의존성 주입
의존성 주입(DI, Dependency Injection)을 사용하는 이유의 핵심은 인터페이스와 함께 스프링 빈 사이의 결합성(coupling)을 아주 느슨하게 하여 변경과 유지 보수를 쉽게 할 수 있는 이점을 얻게 되기 때문이다.

## @scope
스프링 컨텍스트 세부 설정이라 볼 수 있으며 스프링 컨텍스트 생성 시 함께 생성되어 컨텍스트 안에서 관리된다

## bean 설정, xml 설정의 효과
스프링 설정 변경만으로 직접적인 코드 변경 없이 유지보수, 수정이 가능하게끔 한다
`하지만` bean의 갯수와 bean 설정 파일, xml 파일은 비례 관계로 소프트웨어가 커질수록 설정 파일이 늘어나는 것과 코드와 설정 파일이 분리되어 있어 마찬가지로 유지보수가 어려워지는 문제 존재

### Wiring
`wiring`이란 의존성 주입이라 생각하면 된다
종류로 `auto wiring`과 `anotation wiring`가 있다

`auto wiring`은 XML 파일을 사용하는 경우의 XML 설정 파일의 사용을 최소화 하며 `anotation wiring`은 빈 설정 클래스, XML 파일을 설정하지 않거나 가능한 억제하며 어노테이션으로 대체한다

### Wiring 종류
`auto wiring` : xml file 내에서 설정을 통해 정의되어 있는 객체들의 의존성을 주입해주는 효과(설정을 통해 객체들의 의존성 만듬)
  + `byName` : 필드와 같은 `이름(또는 ID)` 갖는 빈과 자동 연결(id로 연결)
  스프링 빈 클래스 예
  ```java
  
  public class Bean1 {}
  public class Bean2 {
  	private Bean1 bean1;
    public void setBean1(Bean1 bean1) {
    	this.bean1 = bean1;
    }
  }
  public class Bean3 {
  	private Bean1 bean1;
  	public Bean3(Bean1 bean1) {
  		this.bean1 = bean1;
  	}
  }
  ```
  XML file
  ```xml
  <!-- 
결국 spring bean으로 사용하고자 하는 class들을 xml file 내에 정의
 코드 내에서 의존성을 관리하는 것이 아닌 xml file 내에서 의존성을 관리
구체적으로 2번 설정 라인을 볼 때 byName으로 autowire가 지정되어 있으며 상단 코드 내 Bean2 클래스의 내부에 bean1 필드명 존재
  이 때 Bean2의 byName을 따라 bean1 <=> id=bean1 이름을 따라 의존성을 주입한다(2번 설정 파일의 조건을 이용해 1번 설정 파일을 사용, 1번과 2번의 의존성 관계 xml file에 설정)
-->
  1.<bean id="bean1" class="Bean1"/>
  2.<bean id="bean2" class="Bean2" autowire="byName"/>
  3.<bean id="bean2" class="Bean2" autowire="byType"/>
4.<bean id="bean3" class="Bean3" autowire="constructor"/>
  ```
  + `byType` : 필드와 같은 `타입`의 빈과 자동 연결(type으로 연결, type 같을 시 primary 설정 필요)
  >
  3번 설정을 보면 Bean2 클래스 내의 객체들은 해당 type과 같은 경우(Bean1 = 1번 설정)을 주입 받는다 
  + `constructor=생성자` : `생성자 매개변수의 타입`과 일치하는 빈과 자동 연결
  > 
  4번 설정은 Bean3 클래스의 생성자 타입 = Bean1에 따라 1번 설정을 주입

### ref
- <a href="https://padak-padak.tistory.com/24">참고</a>


<br><br><br><br><br>

# 주요 Annotation
## Configuration
Bean 설정 클래스라는 것을 IoC에 알려주는 역할
## ComponentScan
지정된 패키지 내부에 어노테이션이 부여된 클래스들을 스캔해 자동적으로 Bean에 등록해주는 역할
## Component
개발자가 작성한 Class를 Bean으로 등록하는 역할, (`Service`, `Repository`, `Controller` 등은 Component의 한 종류)
```java
@Component("이름")
```
  + 형태로 사용되며 이름이 정의되어 있지 않은 경우는 해당 클래스의 이름이 카멜 케이스로, 설정되어 있는 경우는 `이름`으로 Spring Bean이 지정된다

### Service
개발자가 작성한 Class를 Bean으로 등록하는 동시에 서비스 로직(업무 로직)의 위치를 언급하는 역할

### Repository
개발자가 작성한 Class를 Bean으로 등록하는 동시에 데이터 레파지토리를 정의하고 있는 역할
  + 데이터 엑세스 기능을 제공하는 레포지토리
  
### Controller
개발자가 작성한 Class를 Bean으로 등록하는 동시에 MVC 컨트롤러를 정의하고 있는 역할
