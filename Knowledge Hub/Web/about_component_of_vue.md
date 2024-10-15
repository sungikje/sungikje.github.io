---
title: About Component Of Vue
parent: Web
layout: home
nav_order: 2
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_Front 업무를 진행하며 모르는 부분들 공부_
<br><br><br><br><br>
# Component
Vue에서 화면에 표시되는 구성 요소 중에 하나로 여러 Component들이 모여 하나의 화면을 구성한다<br>
Vue는 해당 컴포넌트 각자가 Data를 관리
  - 만약 Data를 단일 오브젝트로 생성해 컴포넌트에서 js를 이용해 접근하는 방식으로 이용한다면 객체의 데이터 침범이 일어날 수 있다
  - 컴포넌트를 재사용하는데 있어 생길 수 있는 부작용(객체의 동시성과 관련) 방지 목적
    - 객체들의 싱크 안맞을 수 있다
  <br>
  - 컴포넌트에서 Data 함수 선언할 때 버전 별로 조금씩 다름
  <br>
  - 여기서 버전은 ES를 의미, 정확히는 ```ECMA Screapt```라 부르며 JS 규격이라 생각하면된다. 이는 JS의 배경과 관련되어 있는데 JS는 10일 남짓한 기간만에 만들어진 언어이고 때문에 보완할 점이 굉장히 많다. 때문에 점점 버전을 업그레이드하며 진행되는 것이고 이를 ES5, ES6 등으로 부른다
<br><br><br><br><br>

# 구조
_Template, Script, Style 3가지로 구성_

## Template
html 화면상에 표시할 요소들로 html 구조라 생각하면 된다

<br><br><br>

## Style
script 템플릿 꾸며줄 CSS 요소들
  - 회사 프로젝트는 여기에 CSS를 운영하는 것이 아닌 .CSS 다른 확장자가 있는데 어떻게 되는지 알아봐야될듯
  <br>
  - 프로젝트의 경우 ```<style scoped>```라는 정의가 있었는데 이는 여러 컴포넌트들이 서로 간의 영향을 주지 않게끔 하기 위해, 즉 고유한 스타일을 선언하기 위한 방법으로 사용
<br>
- ```<style scoped>``` :  scoped 속성을 추가하면 Vue는 그 안의 내용을  SFC(단일 파일 컴포넌트) 내부 범위에서만 적용  
<br><br><br>

## Script
Template 관련 JS 코드, 내 외부 Component 관련 내용들 존재

import, export 존재
  - import 구문을 통해 사용할 컴포넌트를 호출
  - export 구문을 통해 import를 통해 호출한 컴포넌트가 불러와질 수 있도록 하는 역할
<br>

```prop```
상위 컴포넌트의 정보를 전달하기 위한 사용자 지정 특성
  - 모든 컴포넌트 인스턴스에는 자체 격리 된 범위 존재
  - 하위 컴포넌트의 템플릿에서 상위 데이터를 직접 참조할 수 없으며 해서도 안됨

이 때 상위 컴포넌트의 데이터 props로 정의해 하위 컴포넌트로 전달 가능
  - 컴포넌트의 관계가 부모 자식 관계일 경우 가능
<br><br>

### Script 자세히
```data``` : Component(.vue file)에서 사용할 정보들을 가지고 있는 속성
  - 객체 형태, 함수 형태 2가지 경우 존재하며 회사 프로젝트는 함수 형태로 되어 있었다
  <br>
  - 보통 ```key : value``` 형태로 구성
  <br>
  - ```data```내의 변수들을 template에서 사용하고자 하는경우 ```{{ }}``` 이용해 사용 
    - 유연하게 변수 사용 가능
    <br>
  - method에서 사용하고자 하는경우는 ```this.```키워드 사용해 접근
  ```this.``` 키워드의 경우 자동으로 바인딩되는 효과 존재, vue내에서 vue를 지칭하는 의미
  <br>
 - 보통 ```data```를 return을 포함한 함수 형태로 사용하는데 이는 위에 Component 부분에 언급했던 것과 마찬가지로 동일한 컴포넌트가 여러 번 사용되더라도 동일한 객체를 가리키는 것이 아니라 함수가 호출될 때마다 만들어지는 객체가 리턴되어 ```같은 컴포넌트에서 서로 다른 객체```를 참조할 수 있게 하기 위함이다
<br>  
- Option API의 경우 data()를 이용해 반환된 속성들은 반응적인 상태가 되어 ```this```에 노출이 가능하다
여기서의 ```this```는 컴포넌트 객체를 의미
<br>

```meta``` : 라우터 이동 시 권한이나 정해진 상태값에 따라 이동에 제약을 거는 기능
  - 만약 로그인 상태 유무를 예로 권한을 판단한다면 비로그인은 redirect, 로그인이 되어 있는 경우는 정보 그대로 이동시키는 등의 작업 가능
<br><br><br>

## 참고
```export default``` : ```export```와 마찬가지로 다른 파일에 있는 내용을 참조해 오기 위한 방식으로 ```default```를 붙인 경우 해당 모듈엔 개체가 하나만 있다는 사실을 명확히 나타낸다
  - 때문에 파일 하나엔 대개 ```export default```가 하나 존재
  - 구체적으로 .vue 파일(template, script, style)로 컴포넌트를 구성하는 것을 단일 컴포넌트라고 하는데 
  ```현재 컴포넌트 외에 다른 외부 컴포넌트들에서도 데이터를 사용하려는 목적으로 export default 사용```
  
```export```를 사용한 경우는 외부 컴포넌트에서 이용할 수 있도록 하기 위해(다른 컴포넌트에서 현재 컴포넌트를 import 가능하게 하기 위해) import해서 사용하는 경우는 변수명 그대로 이용해야되지만 ```export default```의 경우 그대로 사용하지 않아도 된다
  
<br><br><br><br><br>
# ref
- <a href="https://whitepro.tistory.com/241">구조 1</a>
- <a href="https://www.nextree.co.kr/p10155/">data 저장 관련</a>
- <a href="https://namgyungkim.github.io/javascript/JS-ES/">data 운영 관련</a>
- <a href="https://velog.io/@yanz/Vue.js-Data-%EC%99%80-Method">data, method 사용</a>
- <a href="https://bono915.tistory.com/entry/VueJS-step-5-%EB%A9%94%EC%84%9C%EB%93%9Cmethods">data 접근 참고 1</a>
- <a href="https://medium.com/@hozacho/%EB%A7%A8%EB%95%85%EC%97%90-vuejs-002-vuejs-methods-b3d92ad255bf">data 접근 참고 2</a>
- <a href="https://be-a-weapon.tistory.com/m/224">meta</a>
- <a href="https://velog.io/@yeyo0x0/Vue.js-vue-router-%EB%9D%BC%EC%9A%B0%ED%8A%B8-%EB%AA%85%EB%AA%85-%EA%B2%BD%EB%A1%9C-%EB%B7%B0">name</a>
- <a href="https://sysgongbu.tistory.com/58">export default 참고 1</a>
- <a href="https://engineer-mole.tistory.com/336">export default 참고 2</a>
- <a href="https://codingapple.com/unit/vue-data-import-export/">export default 참고 3</a>
- <a href="https://jsdev.kr/t/export-export-default/5469">export default 참고 4</a>
  - <a href="https://ko.javascript.info/import-export#ref-4122"></a>
- <a href="https://v3-docs.vuejs-korea.org/guide/introduction.html#the-progressive-framework">SFC</a>

