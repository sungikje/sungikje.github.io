---
title: Practice JPA 1
parent: Prototype
layout: home
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_간단하게 Spring boot를 이용해 JPA 연동 테스트_


# Git
- <a href="https://github.com/sungikje/practice">Git Link</a>
  - jpa0

<br><br><br><br><br>

# 구조
## 초기 구성
![](https://velog.velcdn.com/images/sung-ik-je/post/12ef60ba-122b-4fbb-9c0f-b656f50e717c/image.png)
1. Entity, DTO
2. Controller
3. Service
4. DAO or Repository

## STS package
![](https://velog.velcdn.com/images/sung-ik-je/post/13c2186d-be47-4348-952e-24d4207e6f04/image.PNG) 


<br><br><br><br><br>
# 진행하며
## 404?
- 처음에 서버는 돌아가는 것 같은 느낌, 사이트를 연결할 수 없는 것이 아니라 404(파일을 찾지 못했다 뜨기에)
- 시작 페이지 관련 Controller나 pom.xml에서 설정해야되는 부분들이 있을까?
### 404란?
- HTTP에서 file을 찾지 못했을 때 발생하는 에러
  - 추측대로 서버는 돌아가되 파일을 찾지 못해 사이트를 연결하지 못한 것
- HTTP 상태코드 관련 : https://velog.io/@sung-ik-je/HTTP-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C-%EA%B4%80%EB%A0%A8
### 원인
- 이는 Jpa0Application.java file이 controller와 repository 패키지를 인식하지 못해 발생했던 것

<br><br>
## Bean?
- bean이라는 것이 Spring에서 객체를 보다 효율적으로 다룰 수 있게 해주는 것으로 알고 있는데 각 각의 Controller, Service .class와 관련해 Bean 설정 이슈가 있었다
- 이 문제는 Application clss에서 ```@ComponentScan```으로 개선했는데 정확히 Bean이 뭐고 Bean으로 자동 인식되지 않는 이유가 있을까? 패키지 구조 때문인건가?
### 관련
- https://velog.io/@sung-ik-je/Bean
<br><br>

## Spring boot 실행 시
- Java Application, Spring Boot App, Run on Server의 차이는 뭘까?
- 이게 배포?의 차이라는건가?
- 특별하게 찾지 못했다
- 추측으로는 Java Application은 말 그대로 .java 확장자의 실행이고 Spring Boot App은 Spring 전용 실행이라고 예상된다
<br><br>

## @?
- 에너테이션과 관련해 정보들을 찾아봐야 될 필요성 느낀다
- ex) 
  - ```@Controller``` vs ```@RestController```
  - ```@Autowired```
  - ```@Id```, ```@GeneratedValue```등

### 참고
- https://velog.io/@sung-ik-je/Spring-annotation
  
<br><br>

## Spring boot 시작 페이지 관련
- index.html로 바로 들어가는 경우가 있던데 초기 페이지 설정이 따로 있는건가?

### 해결
- Spring boot에서 초기화면(localhost:8080)은 ```@Controller```, ```@RestController``` 상관 없이 resource에 index.html file을 띄운다
- 이는 Controller에서 Mapping("/") 에너테이션을 통해 설정이 가능하다
![](https://velog.velcdn.com/images/sung-ik-je/post/9e13f261-be8f-4674-8dca-6f90ba77a381/image.PNG) 
  - 나 같은 경우는 check.html file로 설정해봤고 정상적으로 작동했다






