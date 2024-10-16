---
title: Spring boot with ES
parent: Web
layout: home
nav_order: 12
---
## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_회사 CMS 관련 소스들을 분석하며_
<br><br><br><br><br>

# 참고
_기본적으로 목적을 알아야 이해가 쉬울 것이라 생각_
<br>
- ElasticSearch에서 하던 작업들을 Spring boot에서 ES 작업 하는 것이 목적이기에 Spring Boot는 ES API 사용한다는 것을 알고 넘어가야 할 듯
<br>
- API가 무슨 작업을 의미하는지 찾아보고 우선 ES에서 어떤 작업을 진행하는지 확인 필요
<br>
- ES가 하는 작업들을 알아야 될 것이며 관련 API는 무엇이 있는지도 알아야 할 듯
<br>
- 이거 코드보면서 딱봐도 API인데(ctrl + 클릭으로 해당 class 정보 볼 수 있는경우) 구글에 돌려도 안나오는 경우 해당 기술 문서에서 서칭 필요
  - java.doc에는 주로 코드(=메서드) 설명이기 때문에 해당 기술 플랫폼(ex, elasticsearch 홈페이지)에서 검색하자

<br><br><br>

# Class
## SearchResponse 
- documents(문서) search, aggregations(집계), suggestions(제안기) and also offers ways of requesting highlighting on the resulting documents
### 제안기
- 쿼리 오타인 경우에 유사한 명령어로 제안
#### 종류 
1. term : 예상되는 의미로 제안
2. phrase : 예상되는 의미로 제안하는데 단어의 위치도 고려함
3. completion : 자동 완성
<br><br><br>

## QueryBuilder 
- Query를 만드는데 사용, Query DSL이 지원하는 모든 타입의 query builder 존재

### Query DSL
- HQL(Hibernate Query Language) 쿼리를 타입에 안전하게 생성 및 관리할 수 있게 해주는 프레임워크
  - 쿼리가 복잡해지는 경우 단순히 Spring에서 제공해주는 메서드로는 깔끔하고 효율적으로 사용하지 못하는 문제 발생
  - 가독성은 물론 실수 없이 깔끔하게 쿼리 작성 가능
<br><br><br>

## AnalyzeRequest 
- 분석기
- 사용자 정의 혹은 기존의 존재하는 분석 방법 정의
- 여기서 정의한 분석 방법으로 document 맵핑


<br><br><br>

## AnalyzeRequestBuilder 
- Analyzerequest 인스턴스 만드는 Class

<br><br><br>

## AnalyzeResponse 
- 토큰화된 Document 토큰 반환

### AnalyzeToken
- Response에 Token 관련 Class
  - term, offset, position 등의 token 관련 정보 저장되어 있음
<br><br><br>

## AnalyzeToken
<br><br><br>

## ElasticOption.java
- 검색결과에 Option을 다루는 Class
- sort, highlight, source
  - source : 볼 Filed, 보지 않을 Filed 설정
- fulfill은 모르겟음 (???????????????????????????)


<br><br><br><br><br>

# ref
- <a href="https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-high-search.html#java-rest-high-search-request">ElasticSearcher 참고</a>
- <a href="https://opster.com/guides/elasticsearch/how-tos/elasticsearch-suggestion-term-phrase-completion/#overview">Suggestions 참고</a>
- <a href="https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-high-java-builders.html ">QueryBuilder 참고</a>
- <a href="https://madplay.github.io/post/introduction-to-querydsl">Query DSL 참고</a>
- <a href="https://u2ful.tistory.com/28">Analyze 참고</a>
- <a href="https://devuna.tistory.com/38">Tokenizer, token filter</a>
- <a href="https://icarus8050.tistory.com/48">역색인</a>
- <a href="https://victorydntmd.tistory.com/315">ElasticSearch 검색 결과 Option 참고</a>






















