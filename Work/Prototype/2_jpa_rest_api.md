---
title: Practice REST API use JPA
parent: Prototype
layout: home
nav_order: 2
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>





_REST API를 운영하는 것이 목적이며 REST 조건 중 CRUD Operation을 그에 따른 HTTP 전송 방식에 맞추는 것 목표_


<br><br><br><br><br>
# Git
- <a href="https://github.com/sung-ik-je/practice">Git Link</a>
  - jpa0

<br><br><br><br><br>
# 구조
- 구조는 jpa0과 동일하며 java file들을 수정
- https://velog.io/@sung-ik-je/JPA-%EA%B5%AC%ED%98%84-0

<br><br><br><br><br>
# 진행하며
## Bean
### package와 bean 관련?
- 시작 이전에 전에 구현했었던 "JPA 구현 - 0" 에서 다른 components들을 bean 객체로 인식하지 못했던 문제를 확인하고자 ```@ComponentScan``` 없이 진행했는데 갑자기 무리없이 실행되었다
  - pom.xml file도 차이가 없는 것 보면 단순히 STS 오류일 가능성 크다고 판단된다
  

### method와 bean 관련
- 호출하는 method들이 제대로 명시되지 않은 경우 = 정의되어 있는 method가 없는 경우에도 bean이 발생했다
  - 해당 함수에서 parameter를 넣지 않고 호출했을 경우
<br>
- 밑에 사진처럼 Controller - Service에서 ```save``` 함수를 호출할 때
![](https://velog.velcdn.com/images/sung-ik-je/post/d22c8fc8-2dce-464c-b3c8-3aa81928a37e/image.PNG)
- 밑에 Service에서 Peoples type에 parameter를 정의해주지 않아 bean 오류 발생했었다
![](https://velog.velcdn.com/images/sung-ik-je/post/74df5a57-278c-4a0c-b0dc-cefa5ff389ab/image.PNG)




<br><br>
## Test 진행
- test는 postman을 이용해 진행했으며 test 과정에서 HTTP 전송 규칙을 유의할 필요 느꼈다
![](https://velog.velcdn.com/images/sung-ik-je/post/27b1ddb7-1752-4fda-a453-889df8739fd8/image.PNG)

<br><br>
## ```@RequestBody``` VS ```@RequestParam```
![](https://velog.velcdn.com/images/sung-ik-je/post/5b820534-edc2-4a43-bca1-8cbe896c88f6/image.PNG)
- 초기에 ```@RequestBody``` 이용해 name이라는 String type으로 DB에 추가하려했기 때문에 문제 발생
- ```@RequestBody``` : Client의 request(요청)들을 객체 형태로 받음
- ```@RequestParam``` : Client의 request(요청)들을 변수에 할당해 받음
- ```@ResponseBody``` : ```@RequestBody```와 반대 상황으로 인지하면 된다
  - Server -> Client 상황, Server가 응답 담아 Client에 보냄
  
<br><br>
## ```@RequestBody```, ```@RequestParam```, ```@ModelAttribute```
_간단하게 본다면_
- ```@RequestParam``` : 변수 정의해 request 받음
- ```@RequestBody``` : 객체로 request 받음, 기본 생성자만으로 역직렬화 가능, setter 없어도 getter로만 가능
  - 정확히 말하면 데이터가 적합한 java 객체로 변환된다 생각하면 된다
    - 데이터가 java 객체로 직접적으로 변환된다
  - 역직렬화 : 생성자를 거치지 않고 리플렉션을 통해 객체를 구성하는 메커니즘
- ```@ModelAttribute``` : 객체로 request 받음, ```@RequestBody```와는 다르게 setter 필요
  - java 객체로 바인딩 된다(```@RequestBody```의 경우는 변환이었다)
  - 데이터가 setter를 이용해 1:1로 객체에 할당된다 
    - java 객체를 생성하고 생성한 객체에 setter를 이용해 할당되는 방식

<br><br>
## ```@PathVariable```?
- REST API에서 URL에 직접적 request 정의하는 경우
- 기존의 ```@RequestParma```을 이용했던 경우
![](https://velog.velcdn.com/images/sung-ik-je/post/b27580e9-52d5-4754-b828-3c98f148db7c/image.PNG)
- ```@PathVariable``` 이용한 경우
![](https://velog.velcdn.com/images/sung-ik-je/post/15199c99-d35e-48a2-aadd-4fc37522a4a7/image.PNG)
- 요청의 경우 URL에 변수 포함해서 요청
![](https://velog.velcdn.com/images/sung-ik-je/post/f2fcc8d3-4952-47a3-92b3-9b7d17d9f6a8/image.PNG)


<br><br>
## 생성자 관련 이슈?
- Model에서 사용하는 Data에 기본 생성자가 없는 경우 트러블(<init\> 관련) 발생
![](https://velog.velcdn.com/images/sung-ik-je/post/5c57c997-5c9f-42a7-b4a7-ece7452ee6e0/image.PNG) Controller에서 DB Update하는 logic
![](https://velog.velcdn.com/images/sung-ik-je/post/564ff12f-299c-44db-8625-3022a8a94e99/image.PNG)
- Entity에 lombok 이용해 생성자 정의하며 트러블 개선
- 왜 기본 생성자를 가져야 하나?
```Spring Data JPA에서는 객체 생성 시 Reflection API를 활용하는데 이 때 DB 값을 객체 필드에 주입할 때 기본 생성자로 객체를 생성한 후 Reflection API를 사용하여 값을 매핑하기 때문에 기본 생성자가 필요하다```


<br><br>
## 로컬, 원격 브런치?
- git branch를 운용하는 과정 중에 원격 저장소와 로컬 저장소 관계 관련해 이슈들 발생
- 원격(git 홈페이지), 로컬(folder)를 의미하며 bash에서 폴더와 깃 홈페이지 둘 다 삭제할 수 있는 것인지
  - 중간에 한번 sts 내에 jpa1 폴더가 벽돌이 되었는데 로컬 branch 삭제해서 그런 것인지 => 이건 sts에서 잘못 눌러 벽돌 된 것
<br>
- 다루고자 했던 문제를 정확히 따지자면 로컬 브런치 삭제, 원격 브런치 삭제 두 가지 명령어가 다른 것을 확인했고 위에 벽돌 된 상황과 겹쳐 혼란 겪음 
  - 브런치에 대해 더 자세히 이것 저것 실험해봤다
<br>
- 이전에 로컬 저장소와 원격 저장소의 차이는 알고 있는 상태
<br>
- 진행함에 있어 git bash를 통해 ```checkout -b branch```로 branch를 만들고 ```add```, ```commit``` 등의 작업까지는 local branch에서 작업을 하는 것이라 생각하면 된다
- push하기 이전에는 원격 저장소에 branch 생기지 않은 상태이며 branch는 local에만 존재
- push를 한 경우에 원격에도 같은 저장소의 branch가 생기는 것
- 때문에 로컬, 원격 브런치 각 각 존재하는 것이라 생각하면 될 것
- 원격 저장소에 push한 후에 인위적으로 다시 원격 저장소에 branch를 삭제했지만```git branch```라는 명령어를 통해 local에는 branch가 남아있다는 것을 확인할 수 있었다 
  - 또 이 과정에서 ```master```에 위치해야만 branch를 삭제할 수 있으며 default branch의 경우는 삭제할 수 없다는 것을 알 수 있었다

<br><br><br><br><br>
# ref
- <a href="https://cheershennah.tistory.com/179">```@RequestBody```</a>
- <a href="https://lifere.tistory.com/entry/Spring-Boot-REST-API-CRUD-%EA%B5%AC%ED%98%84">spring boot rest api 구현</a>
- <a href="https://hongku.tistory.com/119">```@RequestParmas```</a>
- <a href="https://parkadd.tistory.com/70">```@RequestBody```, ```@RequestParmas```, ```@ModelAndView```</a>
- <a href="https://tecoble.techcourse.co.kr/post/2021-05-11-requestbody-modelattribute/">```@ModelAndView``` vs ```@RequestBody``` 1</a>
- <a href="https://maivve.tistory.com/298">```@ModelAndView``` vs ```@RequestBody``` 2</a>
- <a href="https://byul91oh.tistory.com/435">```@PathVariable```</a>
- <a href="https://velog.io/@yyy96/JPA-%EA%B8%B0%EB%B3%B8%EC%83%9D%EC%84%B1%EC%9E%90">생성자 관련</a>