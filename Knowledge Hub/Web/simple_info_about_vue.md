---
title: Simple Info about Vue
parent: Web
layout: home
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# Vue
- SPA, Single Page Application
  - 한 화면 내에서 모든 변화가 이루어짐
## 배경
- JS는 html 구조를 변경, 변형하기 위한 언어이며 데이터를 주고 받을 수 있는 언어 규격이기도 하다
<br>
- JS를 기반으로 UI에 필요한 컴포넌트, 기능들을 불러와 재배치하는데 이 과정에서 새로고침 없이 깔끔하게 해당 위치만 새로 그려내는 정밀한 컨트롤에 사용할 목적으로 개발됨
<br>
- 만약 가상 DOM 사용을 하지 않는 상황에 상호작용이 많다면 DOM 관리와 상태값 업데이트의 어려움
  - 이를 개선할 목적으로 만들어진 것들이 프론트 프레임워크


<br><br><br><br><br>


# 특징
JS 많이 알지 못해도 html 구조 거의 사용할 수 있도록 만들어짐<br>
html 구조에 vue를 얹는 방식으로도 사용 가능<br>
가상 DOM 사용<br>
반응적이고 조합 가능한 컴포넌트 제공<br>
코어 라이브러리에 집중하며 라우팅 및 전역 상태를 관리하는 컴패니언 라이브러리 존재<br>
사용자와의 상호작용이 별로 없다면 사실상 프론트엔드 라이브러리는 필요 X<br>
## mount
가상 dom tree를 탐색하고 실제 dom 트리를 구성하는 프로세스
해당 과정은 렌더러가 진행한다

```vue template``` => ```렌더 함수 코드``` => ```가상 dom 트리``` => ```실제 dom```
<br><br>
## 선언적 렌더링
"어떤 방법으로 보여주냐가 아닌 어떤 것을 보여주냐"

vue의 경우 컴포넌트 단위로 운영

최상위 컴포넌트를 여러 단위 컴포넌트로 채워놓은 구조로 운영되는데 html 형태의 컴포넌트를 선언만 해주면 해당 부분을 컴포넌트를 가져와 채움(전체 페이지를 어떻게 구현할지 구구절절 명시하지 않아도 된다)
<br><br>
## 반응성
데이터의 변화를 자동으로 감지해 화면에 표시해주는 vue의 특성
<br><br>
## 참고
랜더러는 랜더링을 진행하는 모듈이며 랜더 함수 코드는 html, css, js
랜더링은  html, css 등을 묶어 작동 가능하게 만드는 행위



<br><br><br><br><br>



# V-DOM
#### Virtual DOM, 가상 돔<br>
DOM 구조를 하나하나 체크하고 변경하는 방식이 너무 복잡했고 이를 단순화, 자동화 시키려고 만듬
## 원리
V-DOM을 실제 DOM과 직접적인 비교를 통해 운영하는 것이 아니다

```DOM Tree```를 ```js object```로 구현한 것이 V-DOM이라 생각하면 된다

```DOM Tree```를 ```js object```로 바꾼 후에 기준이 되는 ```js object``` <=> ```update js object``` 두 가지를 비교해 diff를 생성하고 실제 dom에 ```diff```를 적용해 운영한다

```js object``` 형태이기에 dom api 호출 없이 자유롭게 조작하고 update 가능
### diff
```js object```들을 비교해 변경 내용을 어떻게 적용할지 알려준다

<br><br><br><br><br>


# 구성
1. Vuex
2. Vue CLI
3. Vue Router 3가지로 구성
## Vuex
- V-DOM 관리, 매니저 역할
- SPA의 핵심적인 역할
- Vue에서 사용되는 컴포넌트들을 만들어내기 위한 명령어들을 담고 있고 실제 V-DOM들을 이용해 원하는 컴포넌트들을 생성
## Vue CLI
**Vue Command Line Interface**<br>
프로젝트 자동 생성, 세팅 등의 자동화 역할<br>
Webpack을 자동으로 모아 세팅해주는 역할
  - **Webpack** : 웹 개발에 사용되는 여러 기능들을 모아둔 것
  - 각기 흩어져 있는 소규모 단위 기능들을 연결해주는 역할
  - 실시간으로 업데이트 된 내용들을 실제 웹페이지에 그대로 반영
- 텍스트 기반의 인터페이스
<br>

## Vue Router
Vuex가 V-DOM을 확인할 때 이동할 통로의 역할
<br>Vuex상에 개별 컴포넌트들을 올려놓고 Router를 통해 간단히 끌어다 다양한 곳에 반복적으로 사용 가능
<br>한번 만들어진 여러 컴포넌트들을 Vuex가 여러 곳에서 동시에 재배치, 변형해 사용할 수 있도록 도와준다
<br>
## 결과적으로
```Vuex```는 컴포넌트 관련 V-DOM을 매니징하며 이 때 ```Routrer```를 이용해 DOM을 관리한다. ```Vue CLI```는 컴포넌트 관련 작업 외에 앱을 운영하는데 사용되는 여러가지 자원들(Wabpack 등)을 관리한다.<br>
=> ```Vuex```는 DOM을 매니징한다면 ```Vue CLI```는 개발자를 매니징




<br><br><br><br><br>


# Project 구조
## node_modules
- 위에 언급한 모듈들이 실제로 설치되어 있는 장소
  - ```package.json```에 종속된 라이브러리들이 모여있는 디렉토리
## public
- Webpack을 통해 관리되지 않는 정적 리소스(static assets)가 모여 있는 디렉토리
### assets
- css나 이미지 등의 정적 자산을 저장하는 디렉토리


## src
_실제 코딩하는 부분이라 생각하면 된다_<br>
```App.vue``` : Vue 객체 컴포넌트, 통합 컴포넌트<br>
```main.js``` : npm 실행되었을 때 가장 먼저 실행되는 js file, Vue 객체 실행 시 App.vue를 이용해 객체 생성<br>
```components```  _template, script, style 3가지로 구성_
  - ```template``` : HTML 화면상에 표시할 요소들
  - ```script``` : 스크립트 코드, (import, export) 
  - ```style``` : template의 HTML 요소를 꾸며줄 css 구문


<br>

```.vue``` 확장자 file, SFC(Single-File Component)라고도 부른다.
component 폴더에 위치한 ```.vue``` 확장자들은 컴포넌트들의 집합이라 생각하면 된다. 위에서 언급한 ```App.vue```의 경우 최상위 컴포넌트 객체이고 component 폴더 내에 위치한 컴포넌트들은 화면 전체가 아닌 부분으로 구성되어 재사용할 수 있는 컴포넌트들이다 
<br>

```router``` _path, name, component 등으로 구성_
  - **name** : unique하게
  - **component** : path로 접근했을 때 실제 컴포넌트 파일 이름
<br>

```assets``` : font, icons, images, css 등 어플리케이션에서 사용되는 정적 파일이 모여져 있는 디렉터리
<br>
```Store``` : Vuex와 관련된 파일을 저장하는 Vuex 스토어 디렉토리 
<br>
```js/plugin``` : plugin 생성 or 연결
<br>
```bable.config.js``` : 바벨 설정 파일
### babelrc
- 프로젝트에 babelrc라는 폴더가 있어서 뭔가 했었는데 모든 브라우저가 ES6를 100% 지원하는 것이 아니기에 구형 브라우저들을 고려해야되는 상황에서 ES6보다 낮은 버전으로 다운 그레이드 해주는 트랜스 파일러라고 한다
#### bable
개발용으로 사용하는 js 기능을 상용 브라우저 호환이 가능하도록 구버전으로 번역하는 역할


<br><br><br>

## 그 외
```package.json``` : 프로젝트에 대한 정보를 담고 있다
그 중 ```dependencies```에 설정된 것들이 배포에 사용될 모듈들<br>
```package-lock.json``` : package.json dependencies에 정의되어 있는 오픈 소스 모듈들이 동작하기 위한 정보 <br>
```index.html``` : Vue에서 운용하는 Single Page, 이 페이지 하나로 Vue Application을 구동한다는 것
<br>
_main.js 실행하면 App.vue 통합 컴포넌트가 실행되고 실행된 컴포넌트들이 index.html에 mount된다_



<br><br><br><br><br>

# 운영
_개인적으로 공부하며 이해한 방향이며 정확하지 않을 수 있다
Vue 운영 원리와 관련해 기능, 비기능적인 요소로 나눌 수 있다고 생각했다_
## 자원적인 경우
1. Vuex : V-DOM 관리

2. Vue CLI : 웹 작업에 쓰이는 개발 환경 관리

3. Router :  Vuex가 V-DOM 확인할 때 쓰이는 통로

## 코드적인 경우
1. 최상위 컴포넌트를 index.html에 덮어씌움

2. 여러 컴포넌트들의 조합 이용해 최상위 컴포넌트를 구성

3. 컴포넌트들은 template(뼈대), script(작업, 동작), style(스킨)로 구성

4. script : 함수, 데이터
			return 받을 내용 데이터 바인딩, 함수들 선언해서 진행
			이 때 컴포넌트 생명주기 유의해서 데이터나 함수 맞춰 실행 가능



<br><br><br><br><br>


# ref
- <a href="https://brunch.co.kr/@clay1987/138">개념 참고</a>
- <a href="https://wildeveloperetrain.tistory.com/161">디렉토리 구조 1</a>
- <a href="https://velog.io/@seulgea/Vue-%ED%8F%B4%EB%8D%94-%EA%B5%AC%EC%A1%B0">디렉토리 구조 2</a>
- <a href="https://blog.naver.com/PostView.naver?blogId=hj_kim97&logNo=222458611638">vue project 생성 및 실행 및 디렉토리 구조</a>
- <a href="https://goodteacher.tistory.com/532">v-bind 1</a>
- <a href="https://joshua1988.github.io/web-development/vuejs/v-model-usage/">v-model</a>
- <a href="https://ko.vuejs.org/guide/extras/rendering-mechanism.html">vue dom 운영 참고</a>
- <a href="https://medium.com/sjk5766/virtual-dom%EC%97%90-%EB%8C%80%ED%95%B4-7222d752ee65">생명주기 - 랜더러</a>
- <a href="https://analogcode.tistory.com/5">반응성, 선언적 렌더링</a>







