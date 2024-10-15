---
title: Conditional Rendering
parent: Web Debug 
layout: home
nav_order: 2
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_유지보수 중에 api를 이용해 데이터를 받아와 테이블 형태로 출력하는 과정에서 데이터는 제대로 넘어오되 화면에 보여지지 않는 문제 해결을 목적으로 진행_

<br><br>
_위에 언급한 것처럼 데이터는 가져왔지만 화면에 출력이 되지 않았고 vue의 조건부 렌더링이라는 것을 확인할 수 있었다_
<br><br><br><br><br>




# 조건부 렌더링
조건부 렌더링의 종류로 ```v-if```, ```v-show```가 있는 것을 알게 되었으며 ```v-if```를 사용하게된다면 조건에 해당하지 않은 경우 렌더링 하지 않는다는 것<br>
밑에 참조된 블로그에 동작원리를 보면 <br>
```template 태그에 html 입력```	=>	```html에 css 정의```		=>	```new vue 생성자를 통해 html, css를 하나의 묶음으로 생성```	=>	```script 태그의 vue 객체와 관련해 id, class 등의 js function, property 값들을 사용```할 수 있다
<br>
여기서 보면 html 태그가 template에 입력될 때 조건부 렌더링(v-메서드 등)을 정의하지 않으면 해당 태그에서 바로 사용하는 내용들은 렌더링하는데 나의 경우 해당 태그에 조건부 렌더링을 걸지 않았기에 ```template 태그 내 html 입력값이 들어갈 때 오류 발생```했던 것(script 태그 내의 property들은 아직 존재하지 않았기에)
<br><br><br><br><br>
# 과정
결과를 정리하자면 가져온건 성공이었지만 해당 과정에서 ```데이터가 불려우는 시점```이 ```html 코드에서 데이터를 읽는 시점```보다 뒤였기에 조회가 안되는 문제 발생
<br>
이 때 나의 경우 ```create``` 과정에서 메서드를 호출했었고 v-메서드(```v-for```, ```v-if```)를 사용한 경우는 비동기적 요청이 가능했다 
<br>














# ref
- <a href="https://jess2.xyz/vue/data-undefined-error/">v-if</a>
- <a href="https://simplevue.gitbook.io/intro/05.-v-if-v-show">조건부 렌더링</a>
- <a href="https://devraphy.tistory.com/197">vue 동작원리</a>