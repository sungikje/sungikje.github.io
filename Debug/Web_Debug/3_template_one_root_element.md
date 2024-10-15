---
title: Component template should contain exactly one root element
parent: Web Debug 
layout: home
nav_order: 3
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_Vue를 진행하며 error 접함_

_처음 퍼블리셔의 작업 파일을 받고 Vue로 옮기는 과정 중에 발생한 에러이다_

<br><br><br><br><br>

# Err 내용
Component template should contain exactly one root element. If you are using v-if on multiple elements, use v-else-if to chain them instead. 

# 관련 내용
`Vue Component`는 `template`, `script`, `style` 3가지 요소로 구성되어 있으며 `template`에는 `html` 태그, `script`에는 `js` 코드, `style`에는 `css`가 들어간다고 간략하게 이해하면 된다
<br>
이 때 `Vue Component` 내에 `template`의 태그들은 하나의 최상의 영역부터 트리 구조로 내려가야 된다
<br>
*잘못된 예*
```js
<template>
  <div>
  
  </div>

  <div>
  
  </div>
</template>
```
  + 이처럼 template 최상위 트리에 다수의 영역이 존재할 수 없다
<br>

```js
<template>
  <div>
  
  </div>
</template>
```
  + 이렇게 하나의 영역만이 가능하다
  
<br><br><br><br><br>
# ref
- <a href="https://jainn.tistory.com/318">참고</a>

