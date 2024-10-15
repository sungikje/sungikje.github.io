---
title: These relative modules were not found
parent: Web Debug 
layout: home
nav_order: 4
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_Vue 의존성 설치 이후에 front 모듈을 실행시켰을 때 발생_

<br><br><br><br><br>
# 원인 1
제목 그대로 err 내용이며 해당 err의 원인은 말 그대로 `module`을 찾지 못했다는 것
<br>
보통 front의 경우 `package.json`에 의존성과 관련된 여러 외부 `module`들이 존재하고 이를 설치함으로 개발 환경을 조성한다
<br>
나의 경우 부트캠프에서 `react`를 사용했을 때 `npm install package.json` 비슷한 명령어를 통해 의존성을 갖추고 실행시켰던 기억을 통해 해당 과정을 반복했고 계속해서 err를 직면했다
<br>
계속해서 찾아보며 `node_modules`라는 `package.json`으로 의존성을 추가했을 때 실질적으로 `module`들이 존재하는 파일을 삭제도 해보고 `package-lock.json` 파일도 삭제 해보고 여러 시도를 해봤지만 결국 git을 안읽은데서부터 오는 문제였다
<br>
회사 `readme` 파일을 통해 단순히 `npm install`이라는 명령어를 통해 개선할 수 있었다
<br><br><br><br><br>
## 결론
*결론적으로 git을 유의있게 관찰할 필요가 있으며 err를 만났을 때 우선적으로 어떤 것이 문제인지 고민해보자*

*말 그대로 module을 못 찾는 것이고, 이는 의존성이 제대로 설정되어 있지 않았던 것이며 의존성 추가로 문제를 해결할 수 있다는 것을 err를 통해 알 수 있었다*

<br><br><br><br><br>
# 원인 2
나의 경우 이미지 파일을 css 폴더에서 가져올 때 경로 관련 이슈인 경우에도 해당 err를 만날 수 있었다

이 때 경로에 대해 더 찾아볼 수 있는 계기가 되었다
  + ```import ... from ...``` 할 때 `./` or `../` 등의 문구들을 접할 수 있었을 것이다
  + 이 때 `../`의 경우는 상위 폴더, `./`는 현재 같은 위치에 파일을 의미한다

경로를 수정해 찾은 경우 외에도 애초에 파일이 없는 경우도 존재할 것이다
  + ex) 퍼블리셔 파일을 관리해주는 사람의 누락 등의 이유로

## 결론
2가지 요소 확인 필요
1. 실제 그 파일이 존재하는지
2. 경로가 맞는지

<br><br><br><br><br>

# ref
- <a href="https://wotres.tistory.com/entry/vue-error-%ED%95%B4%EA%B2%B0%EB%B2%95-This-relative-module-was-not-found-routesindexjs-in-srcmainjs">원인 1</a>
- <a href="https://im-designloper.tistory.com/81">원인 2</a>
- <a href="https://itteamb.blogspot.com/2022/11/vuejs-css-css-import-scoped-css-variable.html">원인 3</a>