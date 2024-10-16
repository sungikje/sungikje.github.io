---
title: JSP Interlocking, Action Tag
parent: Prototype
layout: home
nav_order: 3
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_JSP 구현 목적_
_JSP 운영 구조 파악 및 연동 확인 목적으로 간단하게 돌아가나 확인해봤다_<br>
_JSP 액션 태그 관련 공부 목적
액션 태그는 JSP 내에서 특정 동작을 지시하는 태그_
<br><br><br><br><br>

# GIT
- https://github.com/sung-ik-je/practice
  - jsp0


<br><br><br><br><br>

# 구조 
- Spring에서 웹을 정의하는 root 폴더인 webapp 폴더와 J2EE 사양에 따라 정의된 표준 폴더 구조 사용

#### J2EE
- 자바 기술로 기업환경의 어플리케이션을 만드는데 필요한 스펙들을 모아둔 스펙 집합
- 구성 요소로는 Servlet, JSP, EJB, JDBC 등이 있다<br>
![](https://velog.velcdn.com/images/sung-ik-je/post/72c8ebd2-8fc0-49fc-93ec-fd87dc89cb3d/image.PNG)

<br><br><br><br><br>

# 진행하며
## Contollrer Class 정의?
- 처음 Controller로 사용하려는 Class를 Controller로 지정했는데 애너테이션과 겹치며 오류 발생
  - Class 이름 바꿔 개선<br>
![](https://velog.velcdn.com/images/sung-ik-je/post/2d79aa65-cfc4-4173-b5b8-8f04be724feb/image.PNG)

<br><br>
## Web 애너테이션 관련
- 처음 아무 lib 설정 안하고 PJ를 진행
- Spring Web Lib를 설정하지 않아 애터네이션을 사용하지 못했고 Lib를 추가하며 이를 개선했다

<br><br>

## JSP 태그
_간단하게 태그 정리_
- ```<%@ %>``` : import, 응답 포멧 설정
- ```<%! %>``` : 선언자, 변수와 메서드 선언 태그
- ```<% %>``` : 메서드를 이용한 로직 들어가는 태그, 서비스를 기반으로 각 종 반복문, 조건문 등 알고리즘 들어가는 태그
- ```<%= %>``` : 메서드 호출해 결과 출력
- 또 body 안에 태그 구조를 가진 모든 것을 태그로 인식하는 것을 확인
  - System.out.println(<br\>)을 기입한다해도 <br\>이 출력되는 것이 아닌 줄바꿈이 된다

## Lib 설정
- JSP Lib를 설정해주지 않아 처음 버벅거렸다
- maven lib 설정
![](https://velog.velcdn.com/images/sung-ik-je/post/86a1cc8a-7d0b-4b3b-adb1-9d5279b82b9b/image.PNG)

<br><br>

## Forward, Include, Param
### Forward
- forward의 경우 이 전에 버퍼에 저장했던 내용들 모두 삭제하고 page로 이동
![](https://velog.velcdn.com/images/sung-ik-je/post/26bf9610-7a5a-465c-ab24-b8e34acd1a9a/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/c6f3357a-aae0-49c4-add1-dca6d257a33f/image.PNG)

### Include
- include의 경우는 이 전에 버퍼에 저장했던 내용 + include page 가져와 출력한다
![](https://velog.velcdn.com/images/sung-ik-je/post/4e92f5b0-8aa4-4694-a639-ad1284b6ff80/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/40a36513-17d0-4fdd-8c52-342dcfd088af/image.PNG)

### param
- forward, include 없이 독립적으로 사용할 수 없는 태그
- .jsp 상호 데이터 전송 가능하게 한다
- 마찬가지로 forward의 경우 버퍼를 삭제, include의 경우 포함해 작업된다
![](https://velog.velcdn.com/images/sung-ik-je/post/ff82d57e-87dc-4516-95ea-9c93595b7f92/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/f6496e98-f6ab-49dc-b510-cc3b1bb03648/image.PNG)
<br><br>

## useBean
- Class 객체를 JSP 내에서 사용하기 위한 태그
  - 인스턴스를 JSP 내에서 여러 작업 가능하게 하는 태그라 보면 된다
- JSP 태그 내에 ```id```라는 이름으로 객체를 생성하고 생성한 객체를 통해 메서드를 호출해 사용하는 태그
![](https://velog.velcdn.com/images/sung-ik-je/post/00988fa4-e415-4b1b-97e1-a08711c3111e/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/d6f2f6ca-8b3d-4fcf-a78e-d325e6aca079/image.PNG)

<br><br><br><br><br>


# ref
- <a href="https://7942yongdae.tistory.com/115">PJ 관련</a>
- <a href="https://java.ihavenomoney.co.kr/?page_id=455">J2EE 관련</a>
- <a href="https://kimcoder.tistory.com/192">JSP 태그</a>
- <a href="https://codevang.tistory.com/197">Action Tag 1</a>
- <a href="https://velog.io/@ansalstmd/JSP4.-%EC%95%A1%EC%85%98-%ED%83%9C%EA%B7%B8">Action Tag 2</a>