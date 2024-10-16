---
title: Infra settings of Steammend
parent: Web Project
layout: home
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

<br><br>

_Steammend PJ 배포를 담당하지 않기도 했고 배포를 경험해보고 싶어 PJ 마감 이후에 추가로 GCP를 이용해 배포를 시도해봤다._

<br><br><br>

# PJ 구조
![](https://velog.velcdn.com/images/sung-ik-je/post/8e253b36-4f96-44ab-9188-8698f49a907f/image.png)
  - 그림처럼 react, spring boot, flask로 전반적인 웹을 mysql, redis, elasticsearch db를 사용

<br><br><br><br><br>

# GCP 구조 및 초기 상태
- 초기 구조는 GCP 초기 화면에서 SQL Storage 또한 무료 크레딧을 운영한다기에 ![](https://velog.velcdn.com/images/sung-ik-je/post/324de2cb-a2b4-431a-a65f-4de59f5d2ad8/image.PNG) 
- 이렇게 진행하려 했지만 진행하면서 약간의 트러블로 ![](https://velog.velcdn.com/images/sung-ik-je/post/10dc0496-fa58-4778-a26a-3297217c962c/image.PNG)
- 이렇게 VM 한 곳에 모든 기능을 넣는 방향으로 진행했다. 다양한 클라우드 서비스를 사용해보려했지만 당장은 배포와 linux 사용에 초점을 맞췄다

<br><br><br><br>

# 방화벽 규칙 설정
- GCP 내에서 IP Port를 사용하기 위해서는 VM의 방화벽 설정이 필요하다
1. GCP 콘솔 => 인스턴스 작업 더보기 클릭 -> 네트워크 세부정보 보기
![](https://velog.velcdn.com/images/sung-ik-je/post/98a24306-5311-4dc6-9b00-e6964d6d1894/image.PNG) 2. 왼쪽 VPC 네트워크 방화벽 -> 방화벽 규칙 만들기![](https://velog.velcdn.com/images/sung-ik-je/post/f8006519-370a-45a2-a5a0-7e6880cf414a/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/1f5f424e-9261-4c41-8b2c-66eb44624d6a/image.PNG)
- 우선 배포 테스트 목적이기에 ```대상(모든 인스턴스 허용), 소스IPv4 범위(0.0.0.0/0), TCP(해당 서버 포트)```로 만들었다
- PJ의 경우
  - ElasticSearch : 7200
  - Spirng Boot: 8080 - .jar의 경우도 규칙 만드는 것 지향
  - Flask : 5000
  - Redis : 6379
  - React : 3000
  - MySQL : 3306


<br><br><br><br><br>

# 배포 환경 설정
- React, Spring, Flask : git clone
- Redis : debian에 내장되어 있는 Redis 사용
- ElasticSearch : 추가 다운로드
- MariaDB : debian에 내장되어 있는 MariaDB 사용

# VM - debian
- VM으로 debian 선정
  - 처음 cent os를 사용했지만 npm 환경 설정과 관련해 PJ 버전(16, 로컬은 18)과 맞추지 못해 바꿈
  - debian은 ubuntu랑 debian 같은 계열, cent os는 red hat 계열
- 참고 : https://nirsa.tistory.com/193

## VM 생성
- Compute Engine -> VM 인스턴스 -> 인스턴스 만들기
  - 해당 리전과  VM 용도와 맞는 환경 설정 
![](https://velog.velcdn.com/images/sung-ik-je/post/2ca57669-5505-474e-8483-6fb37cb39b3c/image.PNG)
- 첫번째 사진에 부팅 디스크 -> 변경으로 VM의 OS 선정 가능 ![](https://velog.velcdn.com/images/sung-ik-je/post/04852a3b-c385-4859-a9f4-5e9003bdac80/image.PNG)![](https://velog.velcdn.com/images/sung-ik-je/post/e3e841cc-457b-4092-b35c-e255a0234b51/image.PNG)
- 엑세스 범위 -> 모든 Cloud API에 대한 전체 엑세스 허용으로 해야 된다
  - 안할 경우 proxy 관련 이슈![](https://velog.velcdn.com/images/sung-ik-je/post/a9ef226a-578a-4415-9d83-3fbb21a6de48/image.PNG) 
- ```Port```를 열어도 트래픽을 허용해주지 않으면 문제 발생
- 참고 : https://earth-95.tistory.com/53
- gcp vm 및 debian 초기 설정 참고 : https://curryyou.tistory.com/303
## debian 구조
```
a010--------@instance-1:~$ sudo su
root@instance-1:/home/a010--------# ls
es  python  steam-env  steammend-be  steammend-de  steammend-fe
```
- ```es``` : ElasticSearch 다운 폴더
- ```python``` : python 다운 폴더
- ```steam-env``` : Flask 가상환경
- ```steammend - be, de, fe``` : 백엔드, 데이터, 프론트 git clone folder


## Linux 명령어
- ```sudo su``` : root 권한 계정 접속
- ```ls``` : 해당 위치에서 folder list
- ```mkdir 디렉토리``` : 디렉토리 생성
- ```cd 디렉토리``` : 디렉토리 이동
- ```rm -r 디렉토리``` : 내용물 존재하는 폴더 삭제
- ```sudo apt install git``` : git 다운
- ```git clone 'git repository url'``` : 해당 PJ repo url clone
- ```git --version``` : git 버전 확인
- 참고 : https://codechacha.com/ko/linux-delete-dir-with-rm/


<br><br><br><br><br>

# React
## Linux 명령어
- node 다운 : NodeSource에서 유지 관리하는 리포지토리에서 패키지를 설치
- ```curl -sL https://deb.nodesource.com/setup_18.x | sudo bash -``` : 시스템에 NodeSource 리포지토리를 추가
  - 나의 경우는 18.12.1 버전 사용했기에 18.x로 사용
- ```sudo apt install nodejs``` : Node.js 및 npm을 설치
- ```node -v or node --version``` : node 버전 확인
- ```npm -v or npm --version``` : npm 버전 확인
- ```npm install package.json --save``` : package.json 환경설정 다운로드, --save 해줘야 패키지에 적용된다
- ``` npm ls or npm list``` : package list 확인
- 참고 : https://jjeongil.tistory.com/1298
- npm package.json 이용해 환경 설정 참고 : https://developer88.tistory.com/270
## 실행
- 현재 FE 위치 : /home/a010--------/steammend-fe
- ```npm start``` : FE 위치에서 npm 서버 가동


<br><br><br><br><br>

# Spring
## JDK
- ```sudo apt install default-jdk``` : JDK 11 다운
- ```java --version``` : java version 확인
- ```java -jar steammend-be-0.0.1-SNAPSHOT.war``` : .war file 실행
- 참고 : https://jjeongil.tistory.com/1641

## JAVA_HOME
- ```which java``` : javac 경로 확인, /usr/bin/javac
- ```readlink -f (javac 경로)``` : which java로 읽은 javac 경로, /usr/lib/jvm/java-11-openjdk-amd64/bin/javac
- ```sudo vim /etc/profile``` : 설정 파일 저장소 open
  - 파일 연 상태에서 ```i```눌러 insert mode로 설정
- ```export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64 > /etc/profile``` : javac 경로에서 /bin/javac 전까지 경로 JAVA_HOME 등록
  - ```esc -> :wq!``` : 설정 맞춘 후 나오는 설정 파일에서 나오는 명령어
- ```source /etc/profile``` : 설정 파일 저장
- ```echo $JAVA_HOME``` : JAVA_HOME 조회
- 참고 : https://studying-penguin.tistory.com/2



<br><br><br><br><br>

# ElasticSearch
- ```sudo apt install wget``` : wget 환경 설치
- ```wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-linux-x86_64.tar.gz``` : PJ에서 사용한 ES 7.8.1 다운
  - 위에 줄 특정 버전 다운 받을 때 링크를 넣으면 되는데 해당 링크는 domain쪽 링크가 아니라 다운 받는 부분에 마우스 가져다 되면 압축 링크 복사해서 붙여넣어주면 된다
![](https://velog.velcdn.com/images/sung-ik-je/post/2626afa5-e3f7-41b1-8886-cc1cf88baed5/image.PNG)
- ```tar xvzf elasticsearch-7.8.1-linux-x86_64.tar.gz``` : 다운받은 압축 파일 해제
- ```useradd es``` : es라는 user 추가
- ```chown -R es:es /home/a010--------/es``` : es 폴더 소유자 es(user)로 변경
- ```su es``` : es로 계정 변경
  - root 계정으로 실행할 수 없기에 es 계정 만들어 ElasticSearch가 존재하는 폴더의 소유자로 인정하고 es 계정으로 실행
- ```./elasticsearch``` : elasticsearch bin 폴더에서 실행
- ```curl -XPOST http://localhost:9200/_bulk -H "Content-Type: application/json" --data-binary @final_top_seller_games.json``` : final_top_seller_games.json bulk API 이용해 upload
- 참고 : https://jjeongil.tistory.com/1291
- 참고 : https://triest.tistory.com/46

<br><br><br><br><br>

# Redis
- debian 내장되어 있는 redis 사용
- ```sudo apt install redis-server``` : redis 다운
## 비밀번호 설정
- ```sudo nano /etc/redis/redis.conf``` : redis config file open
  - security부분에 requirepass foobared => requirepass abcd1234
  - PJ에서 abcd1234를 비밀번호로 사용
- ```sudo systemctl restart redis``` : config 변경사항 저장
- ```redis-cli``` : redis server 실행
- 다운 참고 : https://jjeongil.tistory.com/1827
- 비밀번호 설정 참고 : https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-redis-on-debian-9

<br><br><br><br><br>

# Flask
- 배포 테스트 때는 wget 이용해 다운받아 했지만 인스턴스 다시 만들어서 진행할 때 확인해보니 debian은 기본적으로 python3.9.2 내장되어 있었다
  - 내장되어 있는 python3로 진행
## 가상환경
- ```sudo apt install python3-venv``` : python3용 venv 모듈 설치
- ```python3 -m venv steam-env``` : steam-env라는 가상환경 생성
- ```source steam-env/bin/activate``` : steam-env 가상환경 활성화
- ```deactivate``` : 가상환경 비활성화
- ```pip install -r requirements.txt``` : requirements.txt에 있는 pip 패키지 다운로드
- ```pip list``` : 가상환경 pip list 확인
- ```python app.py``` : 실행 메서드
- 참고 : https://heytech.tistory.com/295

<br><br><br><br><br>

# MySQL, Maria DB
- MySQL 다운 : https://jjeongil.tistory.com/1320
  - 다운했지만 MySQL: Package 'mysql-server' has no installation candidate 에러 발생했고 찾아본 결과 mariaDB가 mysql과 거의 동일하다 확인해 MariaDB로 사용
- Maria DB 다운 : 
- ```sudo apt-get install mariadb-server``` : Maria DB 다운
- 참고 : https://stackoverflow.com/questions/20259036/mysql-package-mysql-server-has-no-installation-candidate
### 명령어
- ```mariadb -uroot -p``` : root 권한으로 접속
  - password 입력 후 접속 완료
- 접속 후 메서드는 일반 sql문과 동일


<br><br><br><br><br>

# 생각 확장
## linux ssh
- 처음 서버를 어떻게 돌릴까 고민을 많이했지만 사실 VM도 가상이지만 컴퓨터이고 로컬에서 빌드 테스트 할 때 여러 쉘에 여러 작업들을 진행했기에 SSH도 여러개 띄워서 진행했더니 맞았다
- 추가로 특별한 설정이 없을 때 외부 ip주소 뒤에 port번호를 적어줘야 해당 서비스를 사용 가능했다
  - ip 주소만 치면서 접속이 안되 한참 찾아봤다

## enableRedisKeyspaceNotificationsInitializer
- 원인 : redis 비밀번호 미설정
- <a href="https://yongku.tistory.com/entry/Redis-redis-cli%EC%97%90%EC%84%9C-%EB%B9%84%EB%B0%80%EB%B2%88%ED%98%B8-%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95">redis 비밀번호 설정이 원인</a>



## Window to Linux file upload 실패
- Window OpenSSH 이용해 원격 서버에 파일 직접 전송하려했지만 실패해 git 이용했다
## Spring boot Build 
- Spring의 경우 build하면 target file에 올라가는데 이는 git에 upload되지 않음
- 새로운 폴더로 이동해 업로드 필요
- build하는데 빌드 안됨 => 수정한 user id, pw 존재하지 않기 때문 + redis 실행안해서
  - sts에서 spring app형태로 돌리면서 debug하면서 확인
  - 그리고 로컬에서 실험할 때 회원, 커뮤니티, 댓글 table 중에 회원만 사용했는데 build 할 때 없다고 에러는 뜨는데 성공적으로 빌드 되긴 한다
## git clone
- private로 설정하면 clone되지 않음
  - 필요한 경우 권한 설정 필요


## debian python
- debian에 python3가 내장되어 있다는 사실 모른채 다운로드 진행
  - python과 python3는 다른 것이라는 것을 인지하지 못함
- python은 버전 업데이트가 되는데 python3가 되지 않아 pip 패키지 버전을 못맞추는 문제 발생
  - 추가적으로 버전 검색에 있어 ```python3.9 --version```, ```python3.8 --version``` 이런식으로 조회하는 경우 다운 받았던 버전(ex, 3.9.1 or 3.8.6)이 뜨지만 기본 버전 설정이 업데이트가 되지 않았다
- 때문에 python <=> python3 기본 설정을 하는 것을 찾았고 나의 경우는 python이 최신이고 python3가 최신이 아니였기에 ```alias python3=python```으로 python3도 버전 업데이트 시켜 가상환경을 만들었다
  - 가상환경은 버전 업데이트 후에 생성되어 최신 버전이 유지되지만 vm 껐다 키니깐 os 자체는 그대로 낮은 기본 버전으로 되어있음
상관은 없는 것 같다
- <a href="https://webisfree.com/2020-10-18/python-%EA%B8%B0%EB%B3%B8-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EB%B2%84%EC%A0%84%EC%9D%84-python3%EB%A1%9C-%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95">참고</a>



### VM - SQL Storage 연동 이슈가 있는걸 몰랐을 때
- mysql db 테이블 만들고 spring boot 서버 돌리는데 Access denied for user 'root'@'localhost' 발생
  - db에 권한 설정안해서 그런가 싶었는데 아니었음
  - port 관련 오류 내용 떠있길래 혹시나 해서 8080 방화벽 허용함 
  - 갑자기 mysql 자체 접속 안됨
  - 인스턴스 껏다 켜도 안됨
  - 컴퓨터 껏다 키니깐 됨
- 권한 관련 이슈라 생각해 찾아봄 ```https://dololak.tistory.com/467``` 참고해 두번째 명령어 치자마자 Access denied; you need (at least one of) the SYSTEM_USER privilege(s) for this operation 직면 
- 때문에 새로운 계정을 만들었고 권한 주는데 성공해 다시 build test 진행
  - 아이디 만들어서 권한까지 줬는데 같은 오류 발생

### SQL Storage 연동 이슈 존재하든 것 인지하고 VM 내부의 MariaDB로 사용 전환했을 때
그냥 sql storage 사용안한 debian 자체에 다운 받았던 mariadb에 설정 다 박으니깐 문제 없이 돌아갔다
- 위와 같은 설정을 똑같이 MariaDB에 적용했을 때 전체 서비스 성공
  - 단순히 VM이랑 sql storage랑 연동과 관련해 설정 이슈가 있었던 것
  - 당연히 없는 db에 없는 계정이 권한 요청하니 에러 발생하던 것
    - MariaDB에는 아무것도 하지 않았기에



<br><br><br><br><br>

# 23.07.25
22.12.01 이후로 오랜만에 들어옴

위에 인프라 배포 관련해 나의 경우는 프로세스를 포어그라운드로 배포한 경우이다

당시에는 프로세스를 실행할 때 백그라운드, 포어그라운드 환경을 구분하지 못했고 포어그라운드로 GCP 내에서 여러 VM(=SSH)창을 띄워 진행했는데 서버 개발 환경에서 백그라운드 환경에 프로세스를 실행함으로서 배포하는 것이 보다 일반적이라고 생각한다.

linux 환경에서 bash에 nohub 작업을 통해 백그라운드 작업 진행

## ref
- <a href="https://studymake.tistory.com/621">참고</a>