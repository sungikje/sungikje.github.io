---
title: About CMake
parent: CS
layout: home
nav_order: 2
---

## Table of contents
{: .no_toc .text-delta }
1. TOC
{:toc}

_회사에서 CMake, Make 등 빌드 도구들을 이용한 빌드 자동화 과정에 대한 개념 구체적인 정리 목적_

<br><br><br><br><br>

# Make와 CMake
<span style="color:orange">Make</span>는 자동화 된 빌드 도구로 C/C++ 등의 `컴파일 언어`에서 사용되며 여기서 자동화는 소스 코드를 컴파일하고 링크하는 과정을 자동으로 해주는 것을 의미한다
  + 특정 플랫폼에 종속적이다(주로 Unix 계열)

<span style="color:orange">Makefile</span>은 make 명령어가 참고하는 설정 파일이며 파일 간의 의존성, 컴파일 명령어 등이 저으이되어 있고 이를 기반으로 빌드가 진행된다
  + 
Make의 경우 변경된 파일만 재컴파일하기 때문에 프로젝트가 커질수록 빌드 효율을 크게 개선할 수 있다
+ `빌드 스크립트`라 불린다 

<span style="color:orange">CMake</span>는 크로스 플랫폼 빌드 시스템 생성 도구로 직접 빌드를 수행하지 않고 `CMakelist.txt` 프로그램을 기반으로 여러 플랫폼에서 사용할 수 있는, 즉 플랫폼(운영체제)에 적합한 `Makefile`을 생성, 생성된 `Makefile`은 Make 도구에 의해 빌드된다
  + 여러 환경에서 동일한 소스 코드를 쉽게 빌드할 수 있도록 해준다

✅ **CMake, Make 도구를 이용하는 최종 목표는 다양한 환경(OS)에서 프로젝트의 소스 코드를 컴파일하고 링크하는 과정을 자동화하며 실행 가능한 프로그램이나 라이브러리를 생성하는 것이다**


## Makefile 구성
1️⃣ <span style="color:orange">타겟(target)</span> : `빌드해야 할 파일이나 작업의 이름`
2️⃣ <span style="color:orange">종속성(dependencies)</span> : `타겟을 만들기 위해 필요한 파일들`
3️⃣ <span style="color:orange">명령(command)</span> : `타겟을 만드는 데 사용되는 셸 명령어` 기본 구조로 구성되어 있다

## CMakeLists.txt
CMake라는 크로스 빌드 시스템 생성 도구에서 사용되는 설정 파일
  + CMakeLists.txt는 플랫폼 독립적인 빌드 스크립트로 여러 플랫폼에 맞는 빌드 파일을 생성할 수 있다
  + Make와 같은 저수준 빌드 도구를 추상화하여 보다 유연하고 강력한 빌드 시스템을 제공
  
1. 프로젝트 설정 : `프로젝트 이름과 요구되는 CMake 최소 버전, 사용 언어 등을 설정`
2. 소스 파일 지정 : `빌드할 소스 파일들을 지정`
3. 타겟 정의 : `실행 파일이나 라이브러리를 정의`
4. 빌드 옵션 설정 : `컴파일러 옵션, 링크 옵션 등을 설정`

CMake를 이용한다면 프로젝트 코드들의 <span style="color:orange">모듈화</span>가 가능해 빌드 설정을 보다 효율적으로 관리가 가능하다
  + 구체적으로 보자면 프로젝트 코드를을 부분 부분 구분해 빌드 설정이 가능하다는 것
  + 이는 CMake 옵션을 통해 코드들의 의존성을 관리하며 라이브러리들의 <span style="color:orange">캡슐화</span>가 가능하다

<br>

✅ 결론을 정리하자면 `CMakeList.txt`를 <span style="color:orange">CMake</span> 프로그램을 이용해 다양한 플랫폼에 맞는 <span style="color:orange">Makefile</span> 생성하고 <span style="color:orange">Make</span> 프로그램을 이용해 프로젝트 소스 코드를 컴파일하고 링크해 실행 가능한 프로그램이나 라이브러리 생성하는 것이다

<br><br><br><br><br>

# 코드 예시 
```c
cmake_minimum_required(VERSION 3.10)

project(MyProject VERSION 1.0 LANGUAGES CXX)

# 설정 변수
set(CMAKE_CXX_STANDARD 11)
set(SOURCES main.cpp utils.cpp)

# 실행 파일 생성
add_executable(MyExecutable ${SOURCES})

/*
소스를 추가할 타겟의 이름
	PRIVATE : 해당 타겟에만 적용
    PUBLIC : 해당 타겟과 이를 링크하는 모든 타겟에 적용
    INTERFACE : 해당 타겟을 링크하는 모든 타겟에만 적용 
*/
target_sources(${MyExecutable} [option] fileA.c fileB.c fileC.c)

/*
포함 디렉터리 설정, 헤더 파일 경로라 생각하면 된다 
include_directories : CMakeLists.txt 파일의 범위 내에서 전역적으로 적용
target_include_directories : 특정 타겟에 대해서만 포함 디렉토리를 지정
*/
include_directories(${CMAKE_SOURCE_DIR}/include)
target_include_directories(MyExecutable ${CMAKE_SOURCE_DIR}/include)

/*
라이브러리 생성 및 링크
	지정된 소스 파일들을 여러 조건을 기반으로 컴파일해 라이브러리 생성
	STATIC : 정적 라이브러리(.a)로, 컴파일 타임에 실행 파일에 포함
    SHARED : 동적 라이브러리(.so, dll), 런타임에 링크 
    MODULE : 모듈 라이브러리, 런타임에 동적으로 로드되는 플러그인 모듈로 특정 환경에서 사용된다
*/
add_library(MyLibrary STATIC lib.cpp)
target_link_libraries(MyExecutable MyLibrary)

# 서브 디렉터리 추가, 하위 디렉토리의 CMakeLists.txt 포함시킴
add_subdirectory(src)


/*
타겟에 의존성 설정 방법
	MyExecutable 타겟 전에 MyLibrary가 빌드되며 타겟에 의존성을 추가해준다
    add_subdirectory()의 CMakeLists.txt로부터 빌드된 라이브러리 설정도 가능 
*/
add_dependencies(MyExecutable MyLibrary)

# 빌드 옵션
option(USE_MY_LIBRARY "Use MyLibrary" ON)

# 조건문 예제
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
endif()

/*
특정 이벤트 발생 시 사용자 정의 명령을 실행하는데 사용
빌드 시스템 외부의 작업을 자동화 할 수 있다
	ex) 특정 타겟의 빌드 종료 후에 결과를 특정 경로에 복사한다든지, 스크립트를 실행한다든지 등
*/
add_custom_command()

# 파일 관련 작업(파일의 생성, 읽기, 삭제 등)
file(GLOB SOURCES src/*.cpp)

# 반복문 예제
foreach(source ${SOURCES})
    message(STATUS "Source file: ${source}")
endforeach()

# 외부 패키지 찾기
find_package(OpenGL REQUIRED)

# 메시지 출력
message(STATUS "CMake version: ${CMAKE_VERSION}")
message(STATUS "Project name: ${PROJECT_NAME}")
message(STATUS "Project version: ${PROJECT_VERSION}")
```

<br><br><br><br><br>

# ref
- <a href="https://growingdev.blog/entry/CMake-소개">참고</a>