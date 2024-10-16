---
title: Crontab Permission Denied
parent: Application
layout: home
nav_order: 2
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}
<br><br>

crontab을 이용해 추천 로직을 실행시키는데 결과적으로 업데이트가 되어야 하는 데이터들이 업데이트 되질 않는 문제 발생

crontab의 경우는 프로세스가 등록되어 있었으며 실행이 되는 것으로 확인

원인은 `path` 때문이었다.

crontab에서 특정 파일을 실행시킨다고 가정했을 때 현재 crontab에 등록을 하고 있는 상태에서는 root 계정으로 로그인이 되어 현재 쉘에서 실행하는 것이지만 crontab을 이용한 스케줄링에서는 현재 쉘의 상태가 아닌 OS의 또 다른 쉘에서 실행하는 것을 의미

때문에 crontab을 등록하면서 해당 파일을 실행할 수 있는 권한을 줘야하며 crontab을 실행시키는 새로운 쉘의 맞는 경로(path) 또한 기입해줘야 한다.
  + 여기서 경로는 사용하고자 하는 가상환경들을 실행시킬 수 있는 리소스들이 존재하는 경로를 의미한다

<br><br><br><br><br>

# ref
- <a href="https://ncookie.tistory.com/12">스크립트 path 및 로그 확인</a>
- <a href="https://codechacha.com/ko/linux-assign-execute-permission-to-script/">권한 설정 참고</a>