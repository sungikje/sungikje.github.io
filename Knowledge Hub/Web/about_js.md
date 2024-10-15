---
title: About JS
parent: Web
layout: home
nav_order: 4
---

## Table of contents
{ .no_toc .text-delta }
1. TOC
{:toc}

_회사 내 프로젝트를 위해 js를 한번도 사용해본 적이 없는 상황에서 기존의 조금이나마 사용할 수 있는 java, python을 토대로 비교하며 js의 핵심이라 생각드는 부분과 인상 깊은 부분들 위주로 정리_
<br><br><br><br><br>


# js 언어적 특징
주로 ```웹 브라우저```에서 사용, 클라이언트 측에 사용한다고 보면 된다. ```node.js``` 등을 통해 서버 측 프로그래밍도 가능하다.<br>
인터프리터 언어로 컴파일 과정을 거치지 않는다.<br>
변수의 경우 동적 타입으로 Java처럼 데이터 타입별로 선언하지 않는다.
객체형, 함수형 모두 지원<br>
```ECMA```라는 국제 표준안 존재하며 일종의 버전이라 생각하면 된다
HTML에 내용, 속성, 스타일 변경 역할을 한다
<br><br><br><br><br>
# 동적 타입의 언어
동적 타입이라는 것은 변수의 선언이 아닌 할당 때 변수의 타입이 정해진다는 의미이다. 때문에 변수 재할당을 통해 언제든 데이터 타입 바뀔 수 있다.<br><br>
## 형변환
```typeof```라는 연산자를 이용해 타입을 보며 연산을 진행했는데 js의 경우 언어 자체적으로 연산을 통한 타입 형변환이 가능했다. 타입만 ```number```가 아니며 숫자로 취급 가능한 경우, 예를 들어 ```true => 1```, ```'10' => 10``` 등 연산을 통해 형변환 가능했다. 
이는 js 내부적으로 ```Number + String``` 구조에서 결과를 ```string```으로 유도하는 것이 내재되어 있기 때문이었다.
<br><br><br><br><br>

# 변수
JS는 모든 수를 실수로 표현, 10진법을 베이스로 하며 소수점 0은 자동으로 내린다. 수와 관련된 타입은 ```double``` 하나뿐이며 20년도에 더 큰 수를 표현하기 위해 ```bigint```라는 타입도 나왔다.<br>
```+-infinity```를 이용해 무한대 표현이 가능하며 0을 포함한 불가능한 연산들은 infinity로 표현된다.<br>
```NaN(Not-A-Number)```의 경우는 연산불가를 포함한 수가 아님을 의미한다.<br>
변수 관련해 여러 형태의 수를 출력하는 과정에서 ```01010100```, ```01010104```로 정의한 경우 해당 수를 그대로 출력하는 것이 아닌 ```8진수```로 인식해 ```10진수```로 바꿔 출력하는 문제를 겪었다. 이는 js 진법 표기법과 관련이 있었고 0으로 시작하는경우 ```8진수```로 인식, 출력은 ```8진수```를 ```10진수```로 바꿔 출력하는 것을 알 수 있었다.<br>
## 타입
```var```, ```let```, ```const``` 3가지 변수 선언 타입 존재한다. 2015년도까지는 ```var```만 존재하다 ```let```,  ```const```가 2015년에 추가되었다. 때문에 예전 브라우저를 사용할 때 ```let```, ```const```가 사용 불가능할 수 있다는 점을 알고 있어야한다.<br>
보통의 경우 변수는 ```const```를 이용해 선언한다. ```const```는 변수 재할당이 불가능한 타입이기에 상수 표현이 가능하다. 만약 변수를 재할당하며 사용할 목적이라면 ```let```을 이용해야 한다.<br> 
```let```, ```const``` 모두 재선언은 불가하다. ```let```, ```var```로 선언되어 있는 변수를 ```const```로 재선언 불가하며 반대의 경우도 불가하다.<br>
**유의해야 할 점**은 ```const```의 경우 변수 재정의가 불가능한 것이지 변수 내에 모든 내용들이 고정이라는 것은 아니다. ```const```를 이용해 배열을 선언한 경우 변수에 새로운 데이터 타입을 재할당하진 못하지만 배열 내용을 추가, 삭제 등 유연하게 사용할 수 있다.<br>
```const```, ```let``` 모두 ```scope``` 사용 가능하다.<br>
```var```의 경우는 할당을 먼저하고 이 후에 타입 선언 진행해도 ```호이스팅```과 동시에 변수 초기화 되어 dom 구동과 동시에 사용 가능하지만 ```let```, ```const```의 경우는 할당을 먼저하고 이 후에 타입 선언 진행한 경우 ```호이스팅```은 되지만 변수 초기화가 되지 않아 dom 구동 후에 바로 사용 불가하다.
<br>
### undefined, null
```undefined```, ```null```은 타입이자 같은 이름의 변수만을 가진다. ```undefined``` 타입의 값은 ```undefined``` 밖에 없다. ```null```의 경우는 참조 제거라고 생각하면 된다
<br>
### 타입 변환
JS는 기본적으로 명시적 타입 변환과 암묵적 타입 변환 2가지를 지원한다. 타입 변환에 있어 타입 변환 함수를 사용하는 방법도 있지만 암묵적 타입 변환이 가독성이 더 좋은 경우도 존재한다. ```(10).toString()``` vs ```10+''```, 두 결과 동일하게 10이라는 문자열을 의미한다.
<br><br>
## 메모리 할당
js 메모리의 경우 값을 기준으로 값에 대해 메모리 공간을 관리한다. 값을 ```할당```한다는 것은 특정 값이 존재하는 ```메모리 주소```를 변수로 ```참조```할 수 있다는 것을 의미한다.<br> 
만약 변수의 값을 바꾸면 이전에 참고하던 메모리 주소 내에 값이 변경되는 것이 아닌 ```새로운 주소```로 바뀌게 된다.<br> 
즉 값에 메모리에 한번 저장되면 그 메모리 공간은 ```가비지 콜렉터```가 아닌 이상은 수정되지 않는다고 이해하면 된다. 앞서 언급했던 것처럼 메모리 주소는 고정이되 참조하는 변수들이 바뀌다 만약 참조하는 변수들이 한개도 없는 경우(값 입장에서 아무도 참조하지 않는 경우)는 ```가비지 콜렉터```에 의해 메모리 공간이 수정된다.


<br><br><br><br><br>

### 가비지 콜렉터, Garbage Collector
application이 할당한 메모리 공간을 주기적으로 검사해 더 이상 사용하지 않는 메모리를 해제하는 기능을 담당한다.<br>
바로 위에 언급했던 것처럼 여기서 더 이상 사용하지 않는 메모리는 어떤 식별자도 참조하지 않는 메모리 공간을 의미한다.
<br><br><br><br><br>
# object data type
js는 객체 기반의 스크립트 언어이며 원시 타입을 제외한 나머지 값들 모두를 객체라고 할 수 있다. 객체는 ```key-value``` 형태로 구성된다.<br>
타입은 컴퓨터의 안전한 연산을 위해 중요하다 여겨야 하는 부분이지만 언급했던 것처럼 js의 경우 타입이 굉장히 유연하다. 여기서 타입은 ```let```, ```const```와 같이 선언말고 ```data type(number, string 등)```을 의미한다.<br>
js에서 데이터 기본 타입이 아닌 경우는 모두 객체 타입이라 했지만 배열의 경우는 문서에 값 그대로 출력이 가능, 하지만 object type인 경우는 값이 출력이 되지 않는점 참고
<br><br><br><br><br>
# { }, scope
```{ }```를 이용해 공간을 나눌 수 있으며 나눈 공간을 ```scope```라고 한다. js 코드 블록(```{ }```) 사용하는 경우 자체 종결성을 갖기 때문에 마칠 때 세미콜론 붙이지 않아도 된다.
이를 ```ASI(automatic semicolon insertion, 세미클론 자동 삽입 기능)```라 부르며 ```ASI```가 암무적으로 수행된다고 보면 된다. 그 외 상황에서는 세미콜론 필요하다.<br>
```scope```를 이용해 지역 변수, 전역 변수를 나눌 수 있으며 공간을 나누는 것을 ```block scope```라고 지칭한다. 하지만 ```var```의 경우 ```block scope``` 사용 불가한데 정확히 얘기하면 var은 지역, 전역 변수의 차이가 없기에 의미가 없다.
<br><br><br><br><br>
# 호이스팅
JS 코드 실행은 ```소스 코드 평가```, ```런타임``` 과정을 거치는데 선언문의 경우 ```런타임``` 전인 ```소스 코드 평가```에 우선적으로 코드 맨 상단에 위치시킨다. 이를 ```호이스팅``` 이라고 부른다.<br>
**변수 선언은 호이스팅되지만 값의 할당은 호이스팅되지 않는다는 것 유의**<br>
```값의 할당```의 경우는 런타임에 코드 순서의 맞게 순차적으로 실행된다. 변수 선언 뿐만 아니라 ```키워드```를 사용해서 선언하는 모든 ```식별자(변수를 포함한 함수, 클래스 등)```들은 ```호이스팅``` 된다고 보면 된다.
<br><br><br><br><br>
# 컴파일 vs 인터프리터 언어
```컴파일 언어```의 경우 소스코드 전체를 분석해 실행 파일을 만들고 파일을 실행할 때 만들어진 파일을 실행하는 구조이며 ```인터프리터```의 경우 위에서 언급한 호이스팅 이후에 컴파일 과정을 거치지 않고 코드가 한줄 한줄 읽히며 실행되는 구조이다.<br><br>
## 실행 속도
```컴파일 언어```의 경우 코드 전체를 컴파일하는 과정을 거치면 실행 파일이 생겨 실행할 때 해당 파일만 실행하기에 ```인터프리터 언어```에 비해 속도가 빠른 편이다. ```인터프리터 언어```는 실행 파일이 만들어지는 컴파일 과정은 없지만 매 실행마다 코드를 한줄식 해석하기에 ```컴파일 언어```보다 실행 속도가 느리다.
<br><br><br><br><br>

# 문
프로그램 구성하는 ```기본 단위```이자 ```최소 실행 단위```이다. 종류로는 선언문, 할당문, 조건문, 반복문 등이 있다. <br>
JS 실행 과정에서 코드를 한줄씩 읽는다고 위에서 언급했는데 정확하게 말하자면 글에서 말하는 한 줄이라는 것은 하나의 문이라고 보면 된다.<br>
문은 여러 토큰으로 구성되어 있으며 토큰은 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소이다
## 문 - 표현식 관계
문 안에 표현식이 포함되는 관계라고 생각하면 된다. 문일 순 있지만 그렇다고 모두 표현식은 아니다.<br>
문 중에서도 변수에 할당될 수 있는 경우, 즉 값으로 사용할 수 있는 경우는 표현식이라고 한다. <br>
그 외 값으로 사용하지 못하는 경우 표현식이 아닌 문이라 한다. 예를 들어 (```,```), (```;```), ```변수명``` 등 
## swtich
```swtich```문에서 ```break``` 없는 경우 case 문에 해당하는 경우 들어간 다음 탈출하지 못하고 다음 case가 해당하지 않아도 연속적으로 ```default```까지 모든 문을 거치게 된다.<br>
```default```의 경우는 맨 마지막에 위치해 실행되기 때문에 ```break``` 필요하지 않다.
## 반복문
반복문에 식별자를 붙여 ```break```를 이용할 수 있지만 이용할 경우 프로그램 흐름이 복잡해져 가독성이 나빠지기에 비추
### for문
```for(;;){ }```
  for문 무한루프
  
<br><br><br><br><br>

# 렌더링
HTML, CSS, JS로 구성된 문서를 해석해 브라우저에 시각적으로 출력하는 것을 말한다.

<br><br><br><br><br>

# Ajax 
js를 이용해 서버와 브라우저가 ```비동기``` 방식으로 데이터 교환 받는 기술<br>
페이지 내용의 변화가 있을 때마다 웹 페이지 전체를 렌더링하는 비교적 불필요한 작업들 급격히 줄일 수 있다. 이는 성능적인면에서 월등히 개선할 수 있다.


<br><br><br><br><br>

# 실행 환경
JS는 ```브라우저```, ```node.js``` 두 환경에서 실행 가능하다. ```브라우저``` 환경에서는 html, css 코드들을 제어하는 역할로 JS, HTML, CSS를 렌더링하는 것을 목적으로 하며 ```Node.js```는 브라우저 외부에서 JS 실행을 목적으로 한다. ```브라우저``` 환경의 경우 DOM API를 기본적으로 제공, ```Node.js```의 경우는 DOM API 제공하지 않는다
<br><br>
## Node.js
JS 엔진의 경우 브라우저 환경에서만 동작하는 것을 목적으로 만들어졌지만 브라우저에서만 동작하던 자바스크립트 엔진을 ```브라우저 이외의 환경```에서도 동작할 수 있도록 엔진을 독립시킨 자바 스크립트 실행 환경


<br><br><br><br><br>

# 리터럴
사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법을 의미한다.


<br><br><br><br><br>

# Window
브라우저 안의 모든 요소들이 소속된 객체(최상위 객체), 어디서든 접근할 수 있게 전역 객체이며 ```window```를 이용해 브라우저를 제어하는 다양한 메서드를 사용할 수 있다.
## document 객체?
웹페이지 자체를 의미한다.JS를 이용해 웹 페이지에 접근하고자 할 때는 반드시 ```document``` 객체부터 시작해야한다.


<br><br><br><br><br>


# Identifiers, 식별자
모든 js 변수들은 그들의 특별한 이름을 가지고 있으며 이를 ```식별자```라고 한다<br>
## $
_코드를 보게 된다면 template와 script 두 가지 경우에 $를 사용하는 것이 있었는데 이해가 되질 않았다_<br>
식별자, 일반적인 js문에서 변수명 앞에 사용되면 ```식별자```로 취급한다는 것을 의미하며 ```jQuery```에서는 제이쿼리에 접근할 수 있는 식별자이다. 단일 변수를 선언할 때 사용하며 js에서는 ```camel, undersocre, $``` 3가지를 식별자로 사용한다.<br>
```$http.post```   http post 하는 메서드
```$moment```  js 날짜 관련 lib
<br><br><br><br><br>


# 연산
## &&= 
연산자 왼쪽의 값이 true이면 오른쪽의 값이 왼쪽 값에 할당

## ||= 
&&=과 반대의 경우, false이면 오른쪽의 값이 왼쪽 값에 할당

<br><br><br><br><br>


# 함수
_함수의 존재 의미를 까먹고 있었던 것 같아 적는다_
함수는 동일한 기능의 코드의 재사용성을 증대시키기 위해 존재하며 특정 구간을 묶어 정의해 여러 작업에 사용될 수 있도록하기 위해 사용한다.<br>
함수를 호출하는데 있어 ```()```를 생략한다면 함수 선언식 코드 그대로를 가져온다.
함수를 제대로 이용할 경우에는 무조건 ```()``` 붙여줘야 한다.
<br>
## 화살표 함수
_회사 내부 pj에 addEventListener(event, () => {}) 식으로 되어있었다. 화살표 함수가 뭘까?_
```() => {}```로 정의된 부분이 함수라 생각이 들었고 addEventListener의 parameter가 궁금해 찾아봤다. parameter는 수신할 ```event```와 수신받을 ```객체``` or ```메서드```가 정의되어있다고 한다. 정의한 event가 발생하면 정의되어 있는 ```객체``` or 메서드 ```실행```
<br><br><br><br><br>
# this
1. object method에서 ```this``` = object
2. ```this``` 단일로 쓰이는 경우 or 함수 내부에서 쓰이는 경우(```strict mode``` 아닌 경우) = global object
3. 함수 내부에서 쓰이는 경우(```strict mode```) = undefined
4. event 내부에서 ```this``` = event receive하는 element
<br>
js에서 ```this```는 객체를 가리킨다 생각하면 된다
객체를 지칭하며 ```this.```는 객체의 정도로 해석하면 될 것 같다

<br><br><br><br><br>



# strict mode란?
JavaScript의 엄격모드로 JavaScript의 제한된 버전을 선택하여 암묵적인 "느슨한 모드 (en-US)(```sloppy mode```)"를 해제하기 위한 방법이다.
여기서 sloppy mode의 경우는 치명적이지 않은 일부 에러들을 넘기는데 ```strict mode```는 기존에 무시되던 에러들 throwing한다.


<br><br><br><br><br>


# html template에서의 실행
html 템플릿 태크 내에서 이벤트 관련해 js 코드를 직접 실행하고자 한다면 이벤트 내에 string 타입으로 js 코드를 삽입하면 된다.
## script 위치
script 구문의 위치가 head, body 두 개 위치에서 모두 사용되는 것을 확인했었는데 이는 봤던 것과 동일하기 head, body 둘 다 상관없다고 한다.


<br><br><br><br><br>

# lib
_js로 html 상태를 바꾸는 lib 찾아보며 기록_
## addEventListner
지정한 유형의 이벤트를 대상이 수신할 때마다 호출할 함수를 설정
여기서 받는 객체는 일반적으로 Element, Document, Window

<br><br>

## querySelector
html에서 특정 요소를 가져오는 것
시도해보니 정의된 태그 전체 내용을 가져온다

<br><br>

## element
_querySelector() 구글링하는데 element라는 단어가 굉장히 많이 나온다
element는 뭘까?_
html은 요소의 집합이라 생각하면 된다
요소는 시작 태그, 내용, 종료 태그로 이루어져있다
  html에서 태그를 이용한 하나의 문장을 요소라고 칭하는 것 같다

<br><br>

### 결과적으로
document.getElementById, document.querySelector()에 html element에 사용된 id를 통해 조회하는 것 2가지 모두 똑같은 작업을 진행한다. <br>
간단하게 생각해보면 js 자체가 클라이언트 사이드에서 html과 관련된 작업들을 처리를 목적을 시작으로 만들어진 언어이기에 결국 html에서 정보를 가져와 작업하는게 주 역할이기에 해당 lib들이 대거 포진되어 있다고 생각한다.


<br><br><br><br><br>


# 함수 내 this, 중첩 함수 내 this
_vue js 함수 안에 this와 함수 안에 함수의 this는 무슨 차이점일까?_
js에서 함수 내 함수, 즉 중첩함수의 this는 해당 객체가 아닌 글로벌 객체(window)이다. 중첩 함수 2개 이상일 때부터는 this 계속해서 window 지칭한다.

<br><br><br><br><br>

# jquery
jquery는 js의 lib이고 $는 jquery 식별자이다. js에서 $를 이용해 선언한다는 것 자체가 jquery 객체라는 것을 의미한다. DOM과 이벤트에 대한 코드를 간소화해 이벤트 손쉽게 구현할 수 있다.


<br><br><br><br><br>
_회사 프로젝트 FE 코드 보며 모르는 부분들 찾아 공부할 목적으로 진행_

<br><br><br><br><br>

# ...
- 비구조화 할당
  - 이해한 방향은 변수와 값이 정량적으로 같지 않아도 할당될 수 있게끔 하는 것 같다
- 값 10개인 경우에 보통 다른 언어들은 리스트 한개 또는 10개의 개별 변수를 통해 값을 할당하는데 js의 경우 값을 할당할 때 꼭 그 값들의 갯수들이 변수들과 매칭될 필요 없다

<br><br><br><br><br>
# map
- map 함수는 배열의 각 각의 값을 자동으로 접근해주는 함수, 자동 for문이라 생각하면 된다, 자동으로 for문을 돌려 변수를 빼주는 형식
- return 받은 결과를 가지고 새로운 배열을 만들 수도 있으며 배열 내 각 변수들의 추가적인 처리도 가능하다
<br><br><br><br><br>
# filter
- 링크 참고
<br><br><br><br><br>
# _.
- underscore js, underscore lib
- 배열과 객체를 다루는 함수형 프로그래밍 라이브러리
## _.has
- ```_.has(object, path)```
  - 입력받은 path에 해당하는 경로에 element가 object에 있는지 확인, 결과는 boolean으로 return
<br><br><br><br><br>



# ref
- <a href="http://www.tcpschool.com/javascript/intro">js</a>
- <a href="https://velog.io/@congaweb/compiler-interpreter">컴파일 언어 vs 인터프리터 언어 1</a>
- <a href="https://losskatsu.github.io/os-kernel/compiler-interpreter/#2-%EC%9D%B8%ED%84%B0%ED%94%84%EB%A6%AC%ED%84%B0interpreter">컴파일 언어 vs 인터프리터 언어 2</a>
- 모던 자바스크립트 Deep Dive
- <a href="https://poiemaweb.com/js-object">js object 1</a>
- <a href="https://velog.io/@surim014/%EC%9B%B9%EC%9D%84-%EC%9B%80%EC%A7%81%EC%9D%B4%EB%8A%94-%EA%B7%BC%EC%9C%A1-JavaScript%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-part-7-Object-35k01xmdfp">js object 2</a>
- <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode">strict mode</a>
- <a href="https://developer.mozilla.org/ko/docs/Web/API/EventTarget/addEventListener">addEventListner</a>
- <a href="https://nonipc.com/entry/%EC%9A%94%EC%86%8Celement%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80">html element</a>
- <a href="http://www.tcpschool.com/javascript/js_dom_document">html document</a>
- <a href="https://webclub.tistory.com/74">js 중첩 함수 this</a>
- <a href="https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%99%94%EC%82%B4%ED%91%9C-%ED%95%A8%EC%88%98-%EC%A0%95%EB%A6%AC">js 화살표 함수</a>
- <a href="https://yuddomack.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%AC%B8%EB%B2%95-%EB%B9%84%EA%B5%AC%EC%A1%B0%ED%99%94-%ED%95%A0%EB%8B%B9">...</a>
- <a href="https://velog.io/@daybreak/Javascript-map%ED%95%A8%EC%88%98">map 참고 1</a>
- <a href="https://mjn5027.tistory.com/80">map 참고 2</a>
- <a href="https://velog.io/@jonghwan2_y/underscore-js-%ED%95%A8%EC%88%98-%EA%B5%AC%ED%98%84">_.</a>
- <a href="https://7942yongdae.tistory.com/49">filter</a>
- <a href="https://ibks-platform.tistory.com/392">_.has</a>
- <a href="https://velog.io/@parkseonup/JS-%EB%B3%80%EC%88%98%EB%AA%85%EC%97%90-%EC%82%AC%EC%9A%A9%EB%90%9C-%EB%8B%AC%EB%9F%AC-%EA%B8%B0%ED%98%B8%EC%9D%98-%EC%9D%98%EB%AF%B8">$</a>
- <a href="http://www.tcpschool.com/javascript/js_intro_syntax">식별자</a>
- <a href="https://inpa.tistory.com/entry/AJAX-%F0%9F%93%9A-%EC%84%9C%EB%B2%84-%EC%9A%94%EC%B2%AD-%EB%B0%8F-%EC%9D%91%EB%8B%B5-jQuery#.post">http 메서드</a>