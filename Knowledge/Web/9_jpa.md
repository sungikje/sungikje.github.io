---
title: Simple Contents of JPA
parent: Web
layout: home
nav_order: 9
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# JPA
## JPA란
- DB 연동 표준 프레임워크
  - 자바 클래스와 DB table 매핑해 사용
- ORM 기술 표준으로 사용되는 인터페이스의 모음
  - 함수를 java class를 이용한 실질적 구현아닌 구현된 클래스와 RDB table mapping해준다
    - SQL 쿼리를 직접 짜지 않고 간단한 메소드 이용해 CRUD 처리
    - JDBC API 사용
- ORM 기술의 경우 궁극적으로 객체 중심적으로 개발할 수 있는 환경 만들어준다
- hibernate는 대표적인 JPA open source
![](https://velog.velcdn.com/images/sung-ik-je/post/08c4e4f8-0cc0-40fb-8e97-5a531fe8c05a/image.PNG)
  - JPA( ex, Hibernate) --> JDBC --(sql)--> DB

## Entity
- DB table과 mapping해주는 class
  - table의 구조 자체를 의미
- dto와 구조 같아도 분리해야 한다
  - 보안 목적, end user한테 table 구조 오픈되기 때문

## DTO(Data Transfer Object)
- 일회성으로 Data를 전달해주는 목적
  - - value object
  - get, set을 이용해 데이터를 전달 목적으로 사용, 일회성이기에 entity와 분리
  - 계층간(Model, Controller, Service) 데이터 교환이 이루어질 수 있도록 하는 객체
  - getter, setter 메서드를 포함하며 외에 비즈니스 로직은 포함 X(getter, setter로만 구성)
  - 데이터의 전달이 목적
  - DB로부터 조회된 Entity를 그대로 view에 넘기게 되면 불필요한 정보 및 노출되면 안되는 정보까지 노출되기에 이를 다른 로직으로 분리한 것이 DTO
    - table의 column명의 노출 및 entity 정보의 수정으로 entity와 연결된 다수의 class들이 영향을 받는 등

### Entity <=> DTO
- 유사하지만 간단하게 entity는 고정, DTO는 유연하다 생각하면 될 듯
- entity의 변화는 수 많은 클래스와 함수에 영향을 줄 수 있기에 어느 상황에도 고정적이어야 한다
- DTO의 경우는 단순히 쿼리 결과 운반 객체라 보면 될 듯
  - 데이터 및 컬럼을 수정해도 큰 영향 X

## DAO, Repository
- DAO, Repository 모두 개발 pattern 중에 하나
- Data Access한다는 공통점
  - Repository는 객체 중심, DAO는 DB 테이블 중심이다
- DAO의 경우는 DB table에 매핑되어 있으며 데이터 접근에 중심적으로 운영
  - 단순히 CRUD 명령어를 통해 작업 가능 : query들이 숨겨져 있다
- Repository의 경우 마찬가지로 query 숨겨져 있지만 객체 중심적으로 운영 
- 완전히 이해한건진 모르겠지만 DAO의 경우는 DB table에 맵핑되어 있으며 entityManager의 메서드를 통해 DB에서 데이터를 바로 받아와 사용할 수 있으며 API 형식으로 return도 가능
- 하지만 Repository의 경우는 위에 과정처럼 메소드를 이용해 받아와서 바로 사용한다기보다 객체를 통해 데이터를 저장해 활용하는 방식
- 참고 : https://www.baeldung.com/java-dao-vs-repository

### Spring boot에서의 일반적인 구조
- table별로 Data access pattern(ex, DAO, Repository 등) 존재
  - Controller에서 @Autowired 이용해 해당 table 객체 정의
    - 정확히 말하면 Repository type(table 종류)를 기준으로 bean 찾아 주입하는 애너테이션

## CRUDrepository, JPArepository
- Spring Data가 공통으로 사용하는 인터페이스들
  - Repository, CrudRepository, PagingAndSoringRepository 등
- CrudRepository : CRUD 관련 기능들 제공
- PagingAndSortingRepository : 페이징 및 sorting 관련 기능들 제공
- JpaRepository : JPA 관련 특화 기능들
  - CrudRepository + PagingAndSortingRepository의 기능들
- 목적에 맞는 Repository 사용

## JDBC
- Java Database Connectivity
- 자바에서 DB에 접속할 수 있도록 하는 자바 API
- driver 로딩 -> Connection 생성 -> Statement 생성 -> ResultSet생성(검색인 경우) -> 활용 -> 자원반환

### JDBC Driver
- DBMS와 통신을 담당하는 Java Class
- DBMS별로 개별적으로 존재
- Java App -> JDBC API -> JDBC Driver

## JPQL
- java persistance query language

## 참고
- MyBatis라는 ORM 기술과는 다른 SQL 주입 관련 기술도 존재
<br><br><br><br><br>

# ORM - JPA
## 영속화(Persistant)
- 영구저장이라 생각하면 될 듯하다
  - App의 class와 RDB의 테이블을 매핑한다는 뜻으로 간주
- java app의 데이터가 app의 process보다 지속하게끔 하는 것을 말한다
- 객체의 상태가 JVM 범위를 넘어서서 지속하여 추후 동일하게 사용하는 것을 목적으로 한다
  - JVM을 넘어서면 객체 소실(java는 JVM 위에서 실행되기 때문)

## ORM
- App의 class와 RDB table 매핑, 영속화
  - ex) hibernate
  - 직접적인 sql 작성 X
  - 객체를 ORM 프레임워크에 저장
  - ORM 프레임워크에서 적절한 SQL문 생성해 DB 객체에 저장

<BR><BR><BR><BR><BR>
# Spring Entity 운영 관련
## EntityManagerFactory 
- EntityManager 객체 작성 및 관리
- persistence class에 정적 메소드 이용

## EntityManager 
- entity 관련 CRUD method 존재

## persistence contest  
- 다수의 entity를 관리하는 container
  - 가상의 db
  
## EntityTransaction 
- EntityManager에 대한 작업을 유지 관리하는 클래스
- entity manager마다 존재
- JPA 모든 데이터 변경은 트랜잭션 내에서 수행되어야 한다
- begin과 close 사이
- SELECT의 경우는 필요 X