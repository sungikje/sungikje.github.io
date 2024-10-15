---
title: "Issue of 'background-image'"
parent: Web Debug 
layout: home
nav_order: 6
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# 배경
_퍼블리셔 파일을 받았을 때 이미지를 불러오는 형식이 `style="background-image:url(../imgs/mypage/)"` 해당 형식이었다_
<br>
_회사 프로젝트 내에서 이미지 path의 경우 특정 메서드를 이용해 동적 변수를 할당해 사용하고 있었다_
  + `(변수 | 함수)` js 형식으로 동적 변수를 할당해 return 받는 형태 
<br>

_위와 같은 형식을 백틱을 이용해 :style=\`"background-image:url(${변수 | 함수})"\`  사용했지만 메서드가 실행이 되질 않았다_
  + 0이 return 되거나 아예 읽히지 않았다
  + 0이 읽혔을 땐 함수가 제대로 실행이 안된 것이며 아예 읽히지 않은 것은 작업 과정에서 html 태그 형식이 제대로 작동이 안된 것이라 예상된다 
<br>

_html 태그 class에 위치를 바꾸는 등의 여러 작업들을 했지만 기존의 템플릿의 레이아웃이 맞지 않는 등의 문제 발생_
<br>
_때문에 component 내에 script 부분에 동적 변수를 return 받는 메서드를 사용해야될 필요성을 느꼈으며 실행에 옮겼지만 함수 실행되지 않는 문제 발생_
<br>
_프로젝트를 참고하며 `globalFiter.js`와 `globalMethod.js`라는 공통 메서드들이 위치한 파일들을 확인했고 하위 컴포넌트들에서 해당 메서드들을 어떻게 사용했을까 확인해봤다_
  + 여기서 global method로 등록이 되지 않아 있다는 것이 실행이 되지 않는 원인이었고 global method에 사용하고자 하는 함수를 추가하며 함수를 사용할 수 있었다
<br><br><br><br><br>

# 결론
사용하고자 하는 메서드를 `globalMethod.js`에 등록하고 아래와 같은 형태(단순히 논리적인 구조, 실 코드 X)로 메서드 사용
```js
<template>
  <div class='test' :style="`backgroundImage:url('${A.b}')`"> </div>
</template>
<script>
    this.A.b = this.$method(b)
</script>
```
  + script 부분에서 A 객체 내에 b라는 키의 담겨있는 value를 globalMethod.js에서 등록한 사용하고자 하는 method를 사용해 작업했다