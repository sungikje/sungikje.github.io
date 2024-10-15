---
title: "'webpack-dev-server'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다."
parent: Web Debug 
layout: home
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_회사 CMS front 단을 실행시키는데 오류 발생해 찾아봄_
<br><br><br><br><br>
# ERR 내용
- ```'webpack-dev-server'은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는 배치 파일이 아닙니다.```
<br><br><br><br><br>

# 과정
## 원인 추측
1. 처음 환경 설정할 때 이 전에 부트캠프 프로젝트(react 사용)할 때 처럼 ```package.json```을 다운로드해 사용하는 과정에서 오류 발생했다고 짐작

2. 두번째는 프로젝트에 다른 이슈가 있어 삭제하고 다시 pull해서 진행하는데 webpack 관련 프로그램들을 다운받지 못하는 이슈 발생
   - 명령어 뒤에 ```--force``` 이용해 강제로 다운받아 진행
<br><br>

## 원인
원인으로는 ```npm```에 webpack-dev-server 관련 lib를 즉, 의존성 설치가 제대로 되지 않은 것이 원인이었다.
<br>
프로젝트 의존성을 위해 ```package.json``` 파일을 설치하는데 ERR가 발생했고 이를 해결하기 위해 ```npm install``` 명령어 뒤에 ```--force``` or ```--legacy-peer-deps``` 이용해 설치해봤지만 마찬가지로 설치 과정에서 이슈가 있었고 ```npm start```시에 똑같은 에러 내용을 출력받았다.
#### 명령어 설명
```--force``` 말 그대로 강제로 lib 설치
```--legacy-peer-deps```  의존성 있는 lib 설치할 때 해당 lib가 현재 버전보다 하위 버전의 의존성이 있는 경우 현재 설치되어 있는 상위 버전을 하위 버전으로 취급해 에러 무시

<br><br>

## 해결
초기에는 npm 관련 캐시를 삭제하고 프로젝트를 다시 내려받고 ```npm install```을 계속해서 진행했는데 해결하지 못했다
<br>
프로젝트 개발 환경 조건에 ```node version```은 최소 조건만 존재하며 이상이면 상관없다 확인했기에 가장 최신 버전도 상관없다 생각했지만 가장 최근 LTS version의 npm을 사용했을 때의 오류였기에 버전을 낮추면서 초기 작업을 반복(18 버전에서 16, 14까지 내려오다 14에서 성공)
<br>
#### node_modules, package.json
해당 과정을 거치며 Vue의 구조를 조금 더 알 수 있었는데 이전에 알다시피```package.json```은 프로젝트를 운영하는데 필요한 여러가지 환경에 대한 조건들이 담겨져 있고 ```node_modules```에는 ```package.json```을 통해 다운 받은 실질적인 모듈들이 위치하는 것을 알 수 있었다.
<br>
#### package-lock.json
```package-lock.json```은 ```package.json```으로 미처 관리하지 못한 의존성에 관해 추가적인 관리 하는 역할이다. ```package.json```이 보다 추상적(버전을 범위로)으로 기록되어 있다면 ```package-lock.json```은 직접적(정확한 버전)이며, ```node_modules```과 ```package.json```의 수정 내용도 기록된다.<br>
만약 프로젝트 파일 내에 ```package-lock.json```이 있는 경우는 ```package.json```이 아닌 ```package-lock.json```으로 ```node-modules``` 파일을 형성한다.
  - ```package.json```보다 우선


<br>

### 유의
이 문제 겪은 이후에 똑같은 상황을 한번더 겪게 되었고 해당 과정에서 마찬가지로 ```npm version```을 동료에게 물어 맞춰 ```npm install```으로 종속성을 다운 받고 진행했다.
<br>
처음 부트캠프 프로젝트에서 ```npm install package.json```으로 다운 받는 기억이 있어 해당 방법으로 진행했었는데 회사 내 ```gitlab``` ```readme```에 환경설정이 적혀 있었다.
  - 가장 기본적인 것부터 해결하고 문제 진행해야 된다.

그리고 위에서 언급했던 것 처럼 ```package-lock.json```, ```node_modules``` 등의 파일들은 설치함에 생기는 파일이기에 종속성 이슈에서 지우면서 진행하는 것 유의 


<br><br><br><br><br>
# ref
- <a href="https://ashespia.tistory.com/71">해결 참고 1</a>
- <a href="https://jaehyun8719.github.io/2020/06/24/webpack/dev-server/">해결 참고 2</a>
- <a href="https://softchief.com/2022/06/10/solved-eresolve-unable-to-resolve-dependency-tree-while-installing-a-pacakge-while-working-with-pcf/">해결 참고 3</a>
- <a href="https://jhhan009.tistory.com/74">package-lock.json</a>
- <a href="https://github.com/facebook/create-react-app/issues/9148">해결 참고 4</a>