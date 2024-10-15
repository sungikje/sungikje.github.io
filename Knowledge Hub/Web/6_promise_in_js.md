---
title: Promise in JS
parent: Web
layout: home
nav_order: 6
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>



js인지 jquery인지는 모르겠지만 .then이라는 것이 뭔지 찾다가 promise라는 것을 찾음



# Promise
- 자바스크립트 비동기 처리에 사용되는 객체
  - 비동기 : 특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바 스크립트의 특성
  - 비동기 요청에 대한 결과를 효율적으로 다루는 객체라 생각하면 된다

<br><br>

## 자바스크립트의 비동기란?
- js에서 비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미
  - 특정 로직의 실행이 끝날 때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것
  - ex) ajax-jquery, setTimeout() - 지정한 시간만큼 기다렸다가 로직 실행
### 사용 이유?
- 서버가 요청에 대한 응답을 언제 줄지 모르는 상황에서 무작정 기다릴 수 없기 때문에, 서비스 운영 규모가 큰 경우에 동기로 운영된다면 지연되는 시간이 상당하기 때문

<br><br><br>

## 상태?
_프로미스는 3가지 상태 존재_
### Pending(대기) 
- 비동기 처리 로직이 아직 완료되지 않은 상태, 객체 선언한 상태 new Promise();

### Fulfilled(이행) 
- 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태, 메서드를 호출할 때 callback 함수를 선언한 경우 new Promise(function(resolve, reject))

### Rejected(실패) 
- 비동기 처리가 실패하거나 오류가 발생한 상태

<br><br><br>

## 결과?
_프로미스 함수의 결과 값은 요청에 대한 응답이 정상적으로 받은 경우(resolve)와 아닌 경우(reject에) 2가지_
<br>
promise는 비동기 요청에 대한 결과를 효율적으로 다루는 객체라 생각하면 된다
<br>
요청에 대한 응답값의 성공과 실패를 각 resolve, reject에 담을 수 있으며 결과적으로 요청 결과를 각 then, catch를 이용해 받을 수 있다 

<br><br><br>

## 과정
promise 객체를 선언해 요청, 요청 결과가 정상적으로 받는다면 resolve에 담고 then으로 응답 받을 수 있으며 실패한 경우 reject 이용해 대응 할 수 있다

<br><br><br>




# ref
- <a href="https://joshua1988.github.io/web-development/javascript/promise-for-beginners/">promise 간단한 개념 및 실제 예</a>
- <a href="https://ko.javascript.info/promise-basics">promise 개념</a>



