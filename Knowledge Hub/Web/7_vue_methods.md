---
title: Methods of Vue
parent: Web
layout: home
nav_order: 6
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>



# Vue 요소
## $emit?
- 하위 컴포넌트에서 상위 컴포넌트로 이벤트를 전달하기 위한 방식
  - 하위 컴포넌트에서 emit을 통해 상위 컴포넌트로 이벤트를 전달
  - emit을 이용해 상위 컴포넌트로 전달하면 상위 컴포넌트에서 v-on을 통해 사용 가능







## v-on?
- vue에서 이벤트 핸들링하는 속성
<br><br><br>

## v-bind
html의 속성들을 vue model에서 사용할 수 있게끔 하는 역할

코드 참고 : ```<div class="col" v-bind:title = "변수">{{ 변수 }}</div>```, title 속성을 사용하는 경우

vue 객체 내에서 사용하는 변수로 html 태그 바인딩 가능
  - 위에 코드는 `title`이라는 속성을 관리한 것이며 `class`에 vue 변수를 이용하고 싶은 경우 `v-bind` 이용
  
`<li v-bind:class="'string'+ variable"` 이처럼 작성하는 경우 `string`이라는 문자열에 vue 객체의 변수 `variable`을 합쳐 `class` 속성명으로 지정해 사용할 수 있다





<br><br><br>



## v-confirm?
- 간단하게 확인창이라 생각하면 된다
  - 확인창 팝업

<br><br><br>

## v-directive
v- 접두사가 있는 특수 속성

<br><br><br>

## v-model
사용자 입력 받는 UI 요소들을 자동으로 뷰 데이터 속성에 연결
`v-bind:value` + `v-on:input`

<br><br><br>



## "javascript:void(0);"
_Vue pj 코드를 보다 확인을 했고 예상했던 것처럼 url 태그인건 알겠는데 코드 내용처럼 href="javascript:void(0);"는 뭘까_
javascript는 가상 URL이라고 할 수 있다, javascript:에서 :(쌍점) 뒤에 오는 js 코드를 순차적으로 해석한다
<br>
여기서 void는 undefined 의미, 이는 페이지가 다시 로딩되는 것을 원하지 않을 때 사용, 현재 페이지에 아무런 변화 없이 코드 실행할 때 사용
<br>
이를 토대로 VUE는 SPA이기에 페이지 이동, 재로딩을 막기 위한 것이 아닐까 싶다
프로젝트 상 작업 이력, 재실행 버튼에 해당 태그가 존재했는데 이는 특정 테이블의 내용만 재조회하는 작업이기에 맞다고 생각한다
<br>
이벤트 메서드를 작업하면서 해당 코드를 적지 않는다면 마우스를 올렸을 때 손바닥 모양으로 변하는 변화 없다


<br><br><br>


# this?
_.vue 컴포넌트들에서 this.변수 = this.작업 or 변수로 선언하는데 혹시 왼쪽 this는 vue 인스턴스에 오른쪽 this는 현재 route 객체를 가르키는 것이 맞는가?_
- script 내에 this.는 vue 객체를 가리킨다
  - 이걸 구글링을 하는데도 결과가 안나오고 vue 홈페이지 들어가서 봐도 제대로 명확히 나오질 않았다
  - vsc에서 마우스 오버 시켜놓고 뜨는거 봤더니 여기서 this는 .vue 컴포넌트 객체를 가리키는거였다
  - ex) this.$route의 경우는 .vue 컴포넌트 객체의 라우트 인스턴스 말하는듯



<br><br><br><br><br>


# ref
- <a href="https://webruden.tistory.com/925">emit 개념만 참고</a>
- <a href="https://velog.io/@tobo/vue.js-Prop-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95">props</a>
- <a href="https://joshua1988.github.io/vue-camp/vue/event-emit.html#%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3-%E1%84%87%E1%85%A1%E1%86%AF%E1%84%89%E1%85%A2%E1%86%BC-%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3-%E1%84%92%E1%85%A7%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8">emit</a>
- <a href="https://velopert.com/3148">v-on</a>
- <a href="https://nativescript-vue.org/ko/docs/elements/dialogs/confirm/">v-confirm</a>
- <a href="http://www.tcpschool.com/html-tag-attrs/a-href">html href 태그</a>
- <a href="https://www.freecodecamp.org/korean/news/jabaseukeuribteu-void-0-dodaece-javascript-void-0-neun-museun-ddeusilgga/">javascript:void(0)</a>
- <a href="https://eddie2yim.tistory.com/48">v-model = v-bind:value + v-on:input?</a>