---
title: Simple Contents of Servlet, JSP
parent: Web
layout: home
nav_order: 10
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# 배경
_Cilent <-> Server 구조에서 HTTP 프로토콜 기반의 통신을 한다고 했을 때 HTTP는 Java Class와 통신 불가능_

_Java를 기반으로 HTTP 통신을 하기 위해 사용되는 기술들이 Servlet, Jsp이다_
<br><br><br><br><br>

# Servlet란?
- Java를 사용해 웹 애플리케이션을 만들기 위해 필요한 기술 중에 하나
  - 서버, 브라우저 통신 가능하게 하는 API
    - HTTP <-> Servlet<br>
    
- 웹 요청과 응답의 흐름을 간단한 메서드 호출만으로 체계적으로 다룰 수 있게끔 함
<br>
- ```HttpServletRequest```(client가 server에 요청)와 ```HttpServletResponse```(server가 client에 응답) 두 객체 이용해 서블릿과 클라이언트 사이를 연결
  - HTML을 사용해 Response(자바 소스 코드 안에 HTML을 삽입)하며 Controller는 HttpServlet 클래스를 상속해 운영

<br><br><br><br><br>

# Jsp란?
- JavaServer Pages
<br>
- Servlet 기술을 기반으로 더욱 발전된 기술
  - Java Data 브라우저 화면 출력 가능하게 하며 Java Data를 출력하기 위해서 jsp는 필수
  - JSP는 서블릿을 이용하여 웹페이지를 직접적으로 제어하여 모양이나 내용을 변환하는 기술
<br>
- HTML 내에 직접 자바코드를 삽입하여 웹 서버에서 동적으로 웹 페이지를 생성하여 브라우저에 돌려주는 서버 측 웹 프로그래밍 중 하나
  - HTML 환경에서는 Java code 사용할 수 없지만 Jsp 내에서는 사용 가능하다
<br>
- HTML 페이지 안에 자바(Java) 코드 대신 템플릿 코드를 삽입하여 웹 서버에서 동적으로 웹 페이지를 생성하여 웹 브라우저가 표현할 수 있도록 전달해 주는 기술
  - 정확하게는 자바 소스코드로 작성된 부분은 웹 브라우저로 보내는 것이 아니라 웹 서버에서 실행된다, 이는 WAS가 알아서 작업해 배포를 더 쉽게 만든다
<br>
- 간략하게 HTML + CSS + JS + Java 이용해  View 개발
<br><br>

## 실행 과정
- ```브라우저 요청``` -> ```jsp -> servlet 변환``` -> ```byte code```로 해석해 ```servlet이 응답```
<br>
- 실제 실행 흐름 : Jsp Servlet 변환 -> 컴파일 -> 서버에 객체 생성 -> 서비스
  - 개발자 입장에서 JSP 개발만 맡으며 변환의 경우 tomcat(WAS)이 담당
<br><br>

## Jsp tag
- HTML 기반의 JSP 코드 내에 JAVA 코드를 삽입할 수 있게 해주는 태그

### Jsp 지시자
-  jsp 파일을 의미, 응답 포멧 설정, import 문장 선언구 등
- ```<%@ page %>```

### Jsp 선언자
- 멤버 변수와 메소드 선언 tag
- 멤버 변수는 servlet 객체 하나가 서비스 따라서 모든 user 공유
- ```<%!   %>```

### Jsp Scriptlet
- service() or doGet() or doPost() 와 같은 서비스 로직 구현 tag
- 순수 자바 코드 위주로 개발
- jsp 권장사항 : java 코드가 아닌 tag 위주로 개발 권장하기 때무에 현 추세에선 비추
- ```<%   %>```

### Jsp 표현식(expression)
- service() or doGet() or doPost() 와 같은 서비스 내에서 출력 담당
- ```<%= %>```

### Jsp 주석
- ```<%-- --%>```

### 정리
|제목|내용|
|------|---|
|```<%@ %>```|import, 응답 포맷 선정|
|```<%! %>```|변수, 메서드 선언|
|```<% %>```|서비스 로직, 알고리즘 관련 내용들|
|```<%= %>```|서비스 출력|
<br><br>
## EL 표현식
- EL(Expression Language)은 자바 빈의 프로퍼티, 값을 표현
- 기존의 JSP의 표현식의 업그레이드 버전
  - ```<%= %>```이나 액션 태그 ```<jsp:useBean>```를 사용하는것 보다 쉽고 간결하게 꺼낼수 있게 하는 기술
- 용도 : 철저하게 브라우저에 데이터 출력, 자바 데이터도 출력
- 장점 : jsp에는 순수 자바 코드 최소로 개발 권장 
  - 비교, 연산 등의 로직 처리 기능 보유
<br><br>

## JSTL
- jsp stardard tag library
- 외부 lib를 세팅
  - 어디에서 제공
    - apache 사이트 또는 tomcat의 sample에서
    - 주요 tag
      1. 조건 tag
      2. 반복 tag
    - 개발 단계
      1. lib 세팅
         - WEB-INF/lib/*.jar
      2. jsp에 jstl tag 사용하겠다는 선언
      3. 사용해서 구현
      
<br><br>

## Servlet Container란?
- 간단하게 Servlet Class를 관리해주는 컨테이너
- JSP 파일을 Servlet 클래스로 변환하고 실행시켜 주는 역할
- Java program 중에 하나
  - ex) tomcat
![](https://velog.velcdn.com/images/sung-ik-je/post/3d7bfa62-dee9-426b-9697-5b0490dd7d84/image.PNG)
- 컨테이너가 byte code로 변경하고 servlet이 응답한다
- 종류
  1. HttpServletRequest
  2. HttpServletResponse

<br><br><br><br><br>

# Servlet vs Jsp 비교
_Servlet은 Java로 작업해 HTML 형태로 전달, 브라우저는 응답받은 HTML을 View로 표기_
_JSP는 서버가 (HTML + Java Data)를 브라우저가 표현할 수 있도록 변환해 응답, 브라우저는 결국 HTML과 Java Data로 이루어진 View를 표시_
- 사용 목적은 동일하되 기능의 증가
<br>
- Servlet은 ```자바 소스 코드 안에 HTML을 삽입```하지만, JSP는 반대로 ```HTML 코드 안에 코드를 삽입```한다
  - Servlet은 ```HTML```로 응답을 JSP는 ```HTML+JAVA```로 응답
<br>
- 서블릿 규칙은 꽤나 복잡하기 때문에 JSP가 나오게 되었는데 JSP는 WAS(Web Application Server)에 의하여 서블릿 클래스로 변환하여 사용
  - Jsp의 경우 웹 프로그래머가 소스코드를 수정 할 경우에도 디자인 부분(HTML)을 제외하고 자바 소스코드만 수정하면 되기에 효율을 높여줌



<br><br><br><br><br>

# ref
- <a href="https://mangkyu.tistory.com/14">Servlet</a>
- <a href="https://gmlwjd9405.github.io/2018/11/04/servlet-vs-jsp.html">Servlet - JSP</a>
- <a href="https://insight-bgh.tistory.com/131">JSP 태그 관련</a>
- <a href="https://atoz-develop.tistory.com/entry/JSP-EL-%ED%91%9C%ED%98%84%EC%8B%9D-%EB%AC%B8%EB%B2%95%EA%B3%BC-%EC%82%AC%EC%9A%A9-%EB%B0%A9%EB%B2%95">EL 표현식</a>
- <a href="https://creamilk88.tistory.com/117">EL, JSTL</a>