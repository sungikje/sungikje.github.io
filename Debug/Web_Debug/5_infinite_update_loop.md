---
title: You may have an infinite update loop in a component render function.
parent: Web Debug 
layout: home
nav_order: 5
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_v-for을 이용해 작업하던 중 err 발생_

<br><br><br><br><br>
# 원인
err 내용은 제목과 같으며 `v-for`문을 돌던 중 데이터의 변화가 추가 감지된 경우에 발생했다

vue는 데이터를 바인딩하며 데이터의 변화가 감지되면 기존 상태에서 변화된 부분들을 감지해 렌더링하게 되어 있는데 `v-for` 루프를 돌 때 계속해서 데이터의 변화가 감지되는 경우 계속해서 렌더링 되며 무한 루프에 빠질 수 있고 이로 인해 err 발생

<br><br><br><br><br>
# 해결
이 때 조건부 렌더링 `v-if`, `v-else-if`, `v-else`를 이용해 루프에서 나올 수 있었다


<br><br><br><br><br>

# ref
- <a href="https://tech.amefure.com/js-vue-error-infinite-update-loop">참고</a>
