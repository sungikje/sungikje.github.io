---
title: v-for, In-Place Patch
parent: Web
layout: home
nav_order: 7
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_v-for을 이용해 작업을 하는데 굳이 key라는 것을 사용해야될까?_
<br><br><br><br><br>
# in-place patch
vue에서 기본적으로 사용되는 in-place patch라는 것을 보게 된다면 이해할 것이다
<br>
vue는 dom 최적화 작업에 있어 효율을 중요시 하기에 기존의 상태와 비교해 바뀐 부분만 즉, 땜빵처리한다고 생각하면 된다
<br>
예를 들어 `v-for`로 사용되는 데이터와 `html` 태그로 조합해 사용하는 경우 `v-for`에 사용되는 데이터의 순서가 바뀌었을 때 `v-dom`에 바뀐 순서가 적용되면서 데이터가 바인딩 된다. 
하지만 기존의 `html` 태그의 변화가 없다면 `html` 태그는 변화 없이 그대로 존재
  + `vuex`의 입장에서는 `html`태그는 변함이 없음
  + 하지만 우리의 입장에서 `v-for` 데이터와 `html` 태그를 조합해 사용하는 것이기에 `html` 태그도 `v-for` 데이터의 따라 변화해야된다  
<br>

이 때 `key`라는 키워드를 사용하면 해당 `v-for` 데이터와 연관된 모든 부분들을 바인딩 처리
  + `html` 태그도 함께 바인딩 해준다 생각하면 된다
<br>

`key`는 고유한 값만 사용해야되며 index를 사용해서는 안된다
<br><br><br><br><br>

# ref
- <a href="https://goodteacher.tistory.com/534">참고</a>
- <a href="https://simplevue.gitbook.io/intro/04.-loop-condition">key 참고 1</a>
- <a href="https://mine-it-record.tistory.com/657">key 참고 2</a>