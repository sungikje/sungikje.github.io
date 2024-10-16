---
title: Part of Spring Annotation
parent: Web
layout: home
nav_order: 11
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# Data

## ```@NoArgsConstructor```
- 파라미터가 없는 기본 생성자

## ```@AllArgsConstructor ```
- 모든 parameter를 채우는 생성자

<br><br><br><br><br>

# Controller

## ```@Controller```
- 전통적인 Spring MVC의 컨트롤러 설정
- View 반환 목적 위해 사용
- 만약 View가 아닌 데이터 반환하려면 ```@ResponseBody```와 함께 사용해야 된다
  - Json 형태로 반환 가능

## ```@RestController```
- ```@Controller``` + ```@ResponseBody``` 형태
- Json 형태로 객체 데이터 반환 목적
- REST API 개발에 주로 사용

<br><br><br><br><br>

# Mapping
- 클래스 혹은 메서드와 url 매칭 시켜주는 에너테이션

## ```@RequestMapping```
- Get, Post 두 가지 방식 설정 가능
- 클래스, 메서드 둘 다 맵핑 가능

## Get, Post
- Get의 경우 url에 변수 포함
- Post의 경우 url에 변수 미포함
- HTTP Method 참고 : https://velog.io/@sung-ik-je/HTTP-%EC%83%81%ED%83%9C-%EC%BD%94%EB%93%9C-%EA%B4%80%EB%A0%A8

## ```@GetMapping```
- Get 형태로 밉핑
- 메서드만 맵핑 가능

## ```@PostMapping```
- Post 형태로 밉핑
- 메서드만 맵핑 가능
<br><br><br><br><br>

# ```@Autowired```
- 필요한 의존 객체의 타입에 해당하는 빈을 찾아 주입

# ```@ComponentScan```
- 명시적으로 읽어들여야하는 Component들이 있는 package 정의
- JPA0을 진행하면서 Controller, Service 두 가지를 Application에서 읽지 못했기 때문에 Application.java file에서 두 가지 class가 존재하는 package를 명시해주었다

<br><br><br><br><br>

# ref
- <a href="https://mangkyu.tistory.com/49">```@Controller```, ```@RestController```</a>
- <a href="https://lsh2016.tistory.com/95">```post```, ```get```</a>
- <a href="https://devlog-wjdrbs96.tistory.com/166">```@autowired```</a>
