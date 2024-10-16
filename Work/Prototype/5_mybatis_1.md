---
title: Mybatis test
parent: Prototype
layout: home
nav_order: 5
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_steammend 마지막 pj에서 사용한 mybatis 잊을까봐 관련해 재공부 목적_

<br><br><br><br><br>
# Git
- https://github.com/sung-ik-je/practice
  - mybatis0

<br><br><br><br><br>
# 진행하며
_진행에 앞서 MyBatis 구현과 관련해 추가적인 정보를 말하자면
  steammend에서 ```controller, class``` <=> ```Service, interface``` <=> ```ServiceImpl, class(Service 상속)``` <=> ```mapper, interface``` 구조로 진행했는데 사실 ```mapper```가 존재하는 상황에서 interface(```service```)가 추가로 존재할 필요는 없다고 생각하며 존재해도 ```service```가 아니라 ```serviceImpl```가 interface 형태로 존재했어야 된다 생각한다_

## Mybatis 구현
- 2가지 방법 존재
  1. mapper에 직접적으로 sql 코드 삽입
  2. mapper에 메서드 정의하고 정의한 메서드를 ```.xml``` file에 sql 쿼리로 등록
- 여기선 2번 방법으로 진행

## 구조
- 구조는 ```Controller``` <=> ```Service``` <=> ```Mapper``` <=> ```DB```로 운영
- resource에 mapper 폴더 내에 ```.xml``` file들 위치

## .xml file - sql query
- ```.xml``` file에 sql query를 기입
![](https://velog.velcdn.com/images/sung-ik-je/post/539bd7e2-c3a0-49cf-b8f0-12d49cd4bdfc/image.PNG) 그림과 같은 형태이며 여기서
```namespace``` mapper(interface)에 위치
```id``` mapper에 해당 메서드명
```parameterType```, ```returnType``` 입력, 출력 타입을 지정

# application.properties
![](https://velog.velcdn.com/images/sung-ik-je/post/530740a4-1d1a-4278-a71a-395dee1d505a/image.PNG) 
- resource 내에 mappers 폴더에 ```.xml``` file들 존재하기에 경로 지정
- 두번째 줄은 return type, 즉 DTO가 위치한 경로
- 마지막은 컨벤션 자동 변환(언더 => 카멜) 설정
```
mybatis.mapper-locations: mappers/*.xml
mybatis.type-aliases-package=com.example.demo.model.domain
mybatis.configuration.map-underscore-to-camel-case=true
```

## nullpointexception
- 진행함에 있어 객체가 제대로 운용되지 않고 nullexception이 발생했는데 이는 Controller에서 Service 객체를 사용할 때 ```@autowired```를 정의해주지 않아서 발생하는 문제였다





<br><br><br><br><br>
# ref
- <a href="https://needjarvis.tistory.com/771">mybaits 1</a>
- <a href="https://devlog-wjdrbs96.tistory.com/200">mybatis 2</a>