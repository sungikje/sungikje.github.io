---
title: thymeleaf test
parent: Prototype
layout: home
nav_order: 4
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_html 파악에 더해 spring-html(front - back) 개발 환경을 익히는 것 목표_

<br><br><br><br><br>

# Git
- https://github.com/sung-ik-je/practice
  - html0
<br><br><br><br><br>

# 구조
- JSP와는 다르게 html, css 같은 정적인 요소들은 resource에서 관리한다
![](https://velog.velcdn.com/images/sung-ik-je/post/5f7810c8-32ac-4a23-abd9-26a59776c191/image.PNG)

<br><br><br><br><br>

# 진행하며
## Lib
- .html file 사용 관련 lib를 설정하지 않아 문제 발생
- lib 설정으로 개선
![](https://velog.velcdn.com/images/sung-ik-je/post/309f8fb6-6ca1-4a01-8272-1c2c7406e9d5/image.PNG)

### thymeleaf
- 템플릿 엔진의 일종
- html 태그에 속성을 추가해 페이지에 동적으로 값을 추가하거나 처리할 수 있다

#### 템플릿 엔진
- 미리 정의된 구조에 우리가 사용하는 데이터만 변하는 배경
- 이와 같은 배경에서 html 코드에서 고정적으로 사용되는 부분은 템플릿으로 만들고 동적으로 변하는 부분만 템플릿에 끼워넣는 방식으로 동작할 수 있게끔 해주는 기술
- JSP, Thymeleaf 등이 있다

## ```Controller```에 관해
- jpa1을 기반으로 로직을 짜려했지만 jpa1의 경우는 ```@RestController```로 진행해 Controller에서 어떻게 .html로 이동할까 의문이었다
<br>
- 애초에 ```@Controller```는 View 형식을 사용하는 것이 목적이고 ```@RestController```의 경우 json, xml file return 목적이기에 ```@Controller```로 수정해서 진행
### ```@RestController```에서 View?
- 하지만 수정하기 이전에 ```@RestController```를 사용했을 때 .html로 넘어가기 위해서는 ```ModelAndView``` 객체를 사용해야 하는 것을 알 수 있었다![](https://velog.velcdn.com/images/sung-ik-je/post/bef41f97-24bd-4fd0-9376-32a70671073e/image.PNG)
<br><br>

## form tag에서 put, delete?
- 앞서 언급했던 것 처럼 jpa1을 기반으로 View를 이용해 CRUD Operation을 진행하는데 있어 form tag는 get, post 두가지 방법만 지원하기에 put, delete method 호출하는데 문제 존재
<br>
- 찾아본 결과 form tag 바로 밑에 ![](https://velog.velcdn.com/images/sung-ik-je/post/08e9d81a-9369-430d-974d-17cc1372d4f7/image.PNG) ```<input type="hidden" name="_method" value="PUT"/>```을 기입해 개선하려했지만 왠지 모르게 정상 작동하지 않았고 이유는 ```application.properties```에 ```spring.mvc.hiddenmethod.filter.enabled=true```설정을 추가하지 않았기 때문이었다
  - spring 2.2버전 이상부터는 자동으로 구성되지 않는다고 한다(나의 경우는 아마 2.7.8)
<br><br>

## HTML read 작업 관련
- DB 조회한 내용들을 HTML 상에서 어떻게 표현했는지 기억이 나질 않아 찾아봤다
<br>
- Model, ModelAndView 모두 객체를 return하는 공통점
<br>
- 차이점으로는 Model은 객체만을 ModelAndView는 객체 + View page file 이름까지 return한다

### ModelAndView 객체 운영 관련
#### ModelAndView code
- 처음 객체를 조회하고 id = value 형태로 저장된 경우
![](https://velog.velcdn.com/images/sung-ik-je/post/348c2013-a8d8-4481-a2e5-34c356d6bbfd/image.PNG)
- List 전체를 한번에 peoples 객체에 id = value 라는 이름으로 저장
![](https://velog.velcdn.com/images/sung-ik-je/post/9f290170-2d17-4001-82d1-1a9c755061bd/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/5cb4312c-c47b-46a0-92f0-fd425fc95f97/image.PNG)```체크 : ModelAndView [view="allSearch.html"; model={peoples=[Peoples(id=3, name=변변경익제), Peoples(id=4, name=해익제), Peoples(id=5, name=뉴익제), Peoples(id=6, name="재교체익제"), Peoples(id=7, name=1234), Peoples(id=8, name=기미기미), Peoples(id=9, name=앗살라익제), Peoples(id=10, name=성공익제)]}]```
- model이라는 객체 안에 id = value의 형태로 저장되는 것과 model 안에 peoples이라는 객체의 id = value 형태로 저장
- 아래와 같은 형태로 html 표기를 할때 id = value 형태로 진행한 경우 html 상에서 조회를 어떻게 해야되는지 한참 찾았지만 찾지 못했고 peoples라는 이름으로 객체를 저장한 경우 name으로 조회 가능했다

#### html code
```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>

	<span th:text="${peoples}"></span> 
	<br><br><br><br>
</div>
</body>
</html>
```
#### 결과![](https://velog.velcdn.com/images/sung-ik-je/post/47a5b61d-b675-4395-b895-a94ff52314b9/image.PNG)
<br><br>

# View
## 초기 화면
![](https://velog.velcdn.com/images/sung-ik-je/post/ae9412e4-88a4-4b1a-8ad6-ec17d2af6756/image.PNG)
## 조회 결과
![](https://velog.velcdn.com/images/sung-ik-je/post/2be138f9-d0c2-4971-b656-9a14da1a4ef3/image.PNG)
- 첫번째는 객체를 한번에 출력, 두번째는 객체 안의 내용 순차적으로 출력

<br><br><br><br><br>

# ref
- <a href="https://yunbinni.tistory.com/63">html 전반적인 틀</a>
- <a href="https://www.inflearn.com/questions/77842/html-%ED%8C%8C%EC%9D%BC%EB%A1%9C-%EC%9D%B8%EC%8B%9D%EB%AA%BB%ED%95%98%EB%8A%94-%EB%AC%B8%EC%A0%9C-%EA%B6%81%EA%B8%88%ED%95%A9%EB%8B%88%EB%8B%A4">lib</a>
- <a href="https://ofcourse.kr/html-course/form-%ED%83%9C%EA%B7%B8">form, input 태그</a>
- <a href="https://yeonyeon.tistory.com/153">thymeleaf, 템플릿</a>
- <a href="https://www.leafcats.com/28">HTML에서 정보 전달하는 방법</a>
- <a href="https://needneo.tistory.com/135">submit 이용한 정보 전달</a>
- <a href="https://antstudy.tistory.com/240">html http method 한계(get, post) 개선 참고</a>
- <a href="https://javaoop.tistory.com/56">Model, ModelAndView 관련</a>
- <a href="https://shinsunyoung.tistory.com/28">html Read Operation 관련</a>
- <a href="https://ssd0908.tistory.com/entry/thymeleaf-if-else-%EC%A1%B0%EA%B1%B4%EB%AC%B8-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95">thymeleaf 코드 참고 1</a>
- <a href="http://yoonbumtae.com/?p=1847">thymeleaf 코드 참고 2</a>
- <a href="https://www.dofactory.com/html/table/class">thymeleaf 코드 참고 3</a>