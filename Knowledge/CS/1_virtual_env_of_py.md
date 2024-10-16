---
title: Virtual Environments of Python
parent: CS
layout: home
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}


_평소에 python 가상환경을 사용할 때 단순히 처음 접했다는 이유로 anaconda를 계속해서 사용해왔는데 회사 개발 서버에 anaconda를 올리고 가상환경을 유지하는데 너무 많은 용량을 사용한다는 얘길 듣고 가상환경을 venv로 변경_
<br>
_이와 같은 상황에서 가상환경에 구성 방안에 간단히 정리하고자 작성한다_
<br><br><br><br><br>
_python 가상환경 중에 여러가지 방법들이 있겠지만 anaconda, venv 2가지를 위주로 참고한 자료, 진행 흐름에 대해 간략히 기록 예정_

# Anaconda
## window 기준
### 가상환경 패키지 리스트 저장 및 일괄 설치
_linux의 가상환경을 만들고 기존의 window(로컬)에서 작업했던 패키지만 그대로 전달해줄 수 있다면 가상환경 세팅이 가능할 것이라 생각했다_

`pip list` : 패키지 리스트 확인
<br>
`pip freeze > requirements.txt` : requirements.txt 파일에 가상환경 패키지 리스트 저장
<br>
`pip install -r requirements.txt` : requirements.txt 내에 모든 패키지 일괄 설치
<br>
_하지만 위와 같은 방법으로 가상환경 linux => window 실패_
`conda list --export > packagelist.txt` : conda list 저장(export)

`conda install --file packagelist.txt` : conda list 불러오기(새로운 가상환경에 install)
<br>
_두번째 방법도 실패_

`conda env export -n 가상환경명 --no-build > envrionment.yml` : OS 종속성 제거를 위해 `--no-build` 옵션을 사용해 가상환경 추출

linux 내에 가상환경을 만들고

`conda env update -n 가상환경명 -f environment.yml` : 추출한 가상환경 업데이트

_세번째 방법도 실패, 패키지 외에 다른 문제가 있을 수도 있다는 생각이 들었다_
  + _패키지 내에 실제 프로젝트 모듈에 필요 없는 패키지들도 존재했는데 그 부분들이 문제인가 싶었다_
  + _conda와 pip list가 달랐는데 종속성이 중간에 꼬였을 수도 있겠다라는 생각을 했다_
  
_위 작업을 진행하며 이래서 도커나 컨테이너 같은 작업을 하는건가? 라는 생각을 했다_

해당 작업을 반복하며 anaconda를 몇번을 지우고 실행했을 때 `InvalidArchiveError` err를 확인
  + 아무리 지우고 다시 설치해도 똑같았고 아나콘다 관련된 기록(캐시)들을 삭제하며 개선했다
  + `conda clean --all`

<br><br>
## linux 기준
### 설치
_링크 참고_

anaconda 공식홈페이지에서 linux 환경 installer wget 키워드 이용해 다운
<br>
`bash 파일명` : 다운받은 anaconda install 파일 실행
<br>
*설치 과정에서 anaconda path를 잡아줘야 conda 명령어 실행 가능*
  + 만약 설치하며 경로를 잡았는데 적용이 안되면 `source ~/.bashrc` 명령어를 이용해 최신화 필요
### 가상환경 생성
`conda create --name=가상환경명 python=버전` : 가상환경 생성
<br>
`conda install lib`, `pip install lib` : 모두 모듈 설치 명령어
  + 차이점은 conda의 경우 python 외에 여러 언어들의 가상환경을 지원한다
  + `conda` 명령어는 모든 언어에 대한 전역 환경이라 생각하면 되고 `pip`는 python 가상환경에만 적용되는 거라 생각하면 된다
<br>

`conda activate 가상환경명` : 가상환경 실행
<br>

`conda deactivate` : 가상환경 종료



<br><br><br><br><br>
# venv
## window 기준

`python -m venv 가상환경명` : 가상환경 생성
<br>
`가상환경명/Scripts/activate` : 가상환경 내 scripts 폴더에서 activate로 가상환경을 활성화 시킬 수 있다
<br>
`pip install lib` : 모듈 설치
  + `lib` 위치에 사용할 모듈들을 설치해주면 된다  
<br>

`deactivate` : 가상환경 비활성화
<br><br><br><br><br>
## vs Anaconda
anaconda에 비해 굉장히 적은 용량으로 가상환경을 유지할 수 있다
  + anaconda의 경우 python 뿐만 아니라 다양한 언어들의 가상환경을 구성할 수 있기에 파일이 더 무거운 것이라 생각 든다
<br><br><br><br><br>

# ref
- <a href="https://hello-bryan.tistory.com/441">anaconda on linux, 설치</a>
- <a href="https://hello-bryan.tistory.com/442">anaconda on linux, 가상환경 세팅</a>
- <a href="https://homubee.tistory.com/38">venv</a>
- <a href="https://heytech.tistory.com/296">anaconda 패키지 리스트 저장 및 일괄 설치</a>
- <a href="https://keepdev.tistory.com/27">anaconda 패키지 리스트 저장 및 일괄 설치 2</a>
- <a href="https://jjnomad.tistory.com/35">anaconda 패키지 리스트 저장 및 일괄 설치 3</a>
- <a href="https://cocobi.tistory.com/160">conda vs pip</a>
- <a href="https://github.com/conda/conda/issues/12235">anaconda cache</a>