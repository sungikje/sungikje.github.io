---
title: Import in Vue
parent: Web
layout: home
nav_order: 3
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

# 배경
- front 과제 중에 component 관련 import가 코드의 맨 상단에 위치한 경우도 있지만 component 내에 에로우 함수를 이용해 있는 경우도 존재
<br><br><br><br><br>

# SPA 특징
- component 정의 시에 import를 사용하지 않은 경우는 모든 component들이 페이지 시작과 동시에 내려받는다
<br><br><br>

## 장, 단점으로 인한 사용 배경
이는 SPA의 단점을 알면 이해하기 쉬운데 SPA의 경우 컴포넌트들을 불러오는데 많은 시간이 소요되는 단점이 있는 반면 한번 다운로드 받아지면 컴포넌트의 일부 데이터들만을 수정하기에 빠른 화면 전환이 장점이다
<br>
만약 시스템이 점점 커질 경우 당연히 사용하는 컴포넌트들의 갯수도 많아질 것이고 SPA가 처음 시작될 때 그 많은 컴포넌트들이 다운받아진다면 굉장히 많은 시간이 걸릴 수 있다
<br>
이를 방지하기 위해 특정 컴포넌트가 SPA가 시작될 때가 아닌 컴포넌트가 사용될 때 다운받아지게끔 하는 것이 import를 사용한 방법, 지연된 로딩이라고 부른다
<br>
SPA가 컴포넌트를 불러올 때 성능적인 이슈를 해결하기 위해 미리 불러오지 않고 필요할 때 불러오는 방식이라 생각하면 된다
<br>
#### 결론적으로 결국 보니 import 시점이 바뀌는 것
  - import가 리소스를 다운받는다고 했을 때 코드가 시작될 때 상단에 import를 시켜두는 것과 컴포넌트가 시작될 때 route 내에 component 요소에 import를 시켜두는 것, 두 가지 차이
  <br>
  - 그리고 component들은 .vue file들의 package를 정의한다고 보면 된다
<br><br><br><br><br>

# ref
- <a href="https://sunny921.github.io/posts/vuejs-router-05-lazyloading/">참고</a>
