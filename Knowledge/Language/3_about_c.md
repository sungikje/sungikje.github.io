---
title: About C
layout: home
parent: Language
nav_order: 3
---


## Table of contents
{ .no_toc .text-delta }
1. TOC
{:toc}

<br><br>



_회사에서 C를 다루게 되어 인프런 강의 및 책을 참고하며 간단한 이론을 정리하고자_

<br><br><br><br><br>
# 참고
### 프로그램 기본 절차
저장 공간 확보 ⇒ 입력 ⇒ 처리 ⇒ 출력 
# C 개발 배경
C 언어는 UNIX OS를 모든 기종에서 사용 가능하게끔 하기 위해 개발된 언어

OS는 컴퓨터의 여러 자원을 관리해주는 역할을 하는데  모든 기종에서 사용 가능하게 끔을 더 한다면 C는 여러 자원을 관리할 수 있는 역할을 목적으로 개발되었다 ⇒ 하드웨어를 직접적으로 다룰 수 있는 언어

때문에 하드웨어 제어, 호환성, 이식성 함수 면에서 뛰어나며 자원을 관리하는데 보다 효율적인 방안으로 비트 연산자, 포인터 등이 있다
## 표준
K&R C, 초창기의 전통적인 C 언어

ANSI, 미국 표준 기구에서 지정 

C99, ISO에서 정한 표준
### 참고
SCII- 아스키 코드, 미국 표준 정보 교환 부호 

`1`bit- `1`진수 1개
`3`bit- `8`진수 1개
`4`bit- `16`진수 1개
## 컴파일
소스 코드를 아스키 코드 값으로 작성을 하되 실제로 CPU가 이해할 수 있는 형태로 바꿔 주는 작업이 필요함 ⇒ `컴파일` 

문자들이 CPU가 실행시킬 수 있는 명령어의 형태로 바뀐다

프로그램은 운영체제에서 실행된다

### 아스키 코드
알파벳 소문자, 대문자, 특수 문자, 제어 문자 포함해 127가지

2^7, 7 bit로 모두 표현 가능 = 1byte 내로 표현 가능

⇒ 1byte면 표현이 충분하지만 정수와 포맷을 맞추기 위해 4byte로 사용한다(앞에 3byte는 0으로 채움) 

```c
/* 
char type은 1byte만 담을 수 있지만 위에 언급했던 것처럼 
아스키 코드는 맨 마지막 1byte만으로도 충분히 표현 가능하기에 아래처럼 정의 가능 
*/
char a = 'a';  

// 기능문자를 %c를 이용해 출력하는 경우 해당 기능 수행
printf("[%c%c]", 97, 10);  // 10은 줄바꿈 
/* 출력
[a
]
*/
```

입력 받을 때 제어 문자를 스킵하고 싶은 경우는 해당 입력에 스페이스 추가
```c
// 1 2를 입력하고 싶은 경우 
char ch1, ch2;
int a;

scanf("%c %c", &ch1, &ch2);
scanf("%c%c", &ch1, &ch2);  // %c 사이를 띄우지 않는다면 1하고 sb가 입력된다

a = getchar() // 단일 문자 입력 받을 수 있다, int 형태로 저장되기 때문에 a의 type은 int 
putchar(a) // 단일 문자 출력, a의 값 출력
```

### 전처리 지시자
컴파일러가 처리 X, 전처리기가 처리

전처리기- 컴파일러에 소스 코드 넘어가기 전에 소스 편집해주는 역할

항상 `#` 으로 시작

#### `#include`
지정한 파일의 내용을 읽어 지시자 위치에 붙여 넣는다 
`<>`- 컴파일러가 지정한 폴더에서 헤더 파일 가져옴 
`""`- 소스 파일이 저장된 디렉토리에서 먼저 찾고 없으면 include 디렉토리에서 다시 한번 찾음
직접 파일 경로 지정할 수도 있다 
```c
#include <stdio.h>
#include "right.h"
#include "C:\user\myhdr.h"
```
  + 전처리가 끝나면 include한 파일들의 내용이  복사되어 소스 파일에 포함된다 
    
#### `#define`
복잡한 상수나 문장에 대해 매크로 명을 정의한다 
```c
#define PI 3.14159
#define MSG "passed!"
#define ERR_PRN printf("범위를 벗어났습니다\n")
#define INTRO "Perfect C Language \
  & Basic Data Structure"
// 줄바꿈은 \ 이용해 표시
    
#define SUM(a, b) ((a) + (b))  // 괄호는 무조건 필요
#define MUL(a, b) ((a) * (b))
    
int a = 10, b = 20;
int res;
    
printf("%d", SUM(a, b));  
    
/*
여기서 만약 괄호 없는 경우 치환이 되면
30 / a * b, 형태로 우리가 원하는 형태가 아닌 다른 형태로 된다 
*/
res = 30 / MUL(a, b);
```

`typedef`와 차이점을 유의해야된다
  + `define`은 단순히 글자 대치, `typedef`는 컴파일러가 직접 처리(컴퓨터 시스템에 따라 유연하게 설정값 사용 가능)

    
#### 컴파일러에 이미 정의되어 있는 매크로들
코드 상에 매크로를 집어 넣어 사용하며 컴파일하면서 컴파일러에 이미 정의되어 있는 형태로 치환된다 
  + `#`- 문자열로 치환
  + `##`- 두 인수를 붙여 치환             
        
    
#### 조건부 컴파일 지시자
말 그대로 조건이 충족하는 경우만 컴파일 진행하며 `#`이용해 코드 정의  
  + ex) `#if` 구문, 이 때 `#else` 가 아니라 `#elif` 사용 
  + `#if defined x`- 만약 x가 정의되어 있는 경우로 해석할 수 있다
    + `#ifdef x` 와 똑같은 명령어 
  + `#undef`- 매크로명 해제하는 지시자
  + `#error`- 메시지 출력하고 컴파일 중단
  + `#pragma`- 컴파일러에 컴파일 방법을 제어
## 헤더 파일
header file
  + include file이라고도 부르며 컴파일러에 의해 다른 소스 파일에 자동으로 포함된 소스 코드의 파일 

main 함수 정의 이전에 전처리 지시자들을 이용해 현재 파일에 존재하지 않지만 필요한 함수들을 선언해준다
이 때 전처리 지시자에 헤더 파일을 정의해준다
  + 참고) C 소스 코드 환경에서 header file은 함수의 선언부만 위치해 있으며 .c, .cpp 확장자는 정의부가 선언되어 있다 
  + 컴파일러는 정의되어 있는 header file을 해당 header file의 내용(각 함수들의 선언부)으로 치환한다
  + 링커는 치환된 header file에 선언 부들을 이용해 header file의 정의 부가 존재하는 파일들을 사용할 수 있게 끔 해준다

<br><br><br><br><br>

# C 전반적인 특징
함수로 이루어져 있다 
  + `매개 변수` - 함수가 실행되는데 필요한 변수
  + `토큰` - 의미 있는 하나의 단어 
<br>

운영체제는 `하드 디스크` 에 저장하며 `메인 메모리`에 옮겨 프로그램 실행
`startup code`- 컴파일러가 소스 코드 컴파일 시 붙여줌, 이 친구가 main 함수를 호출함
  + 함수에서 return은 무조건 필요한데 프로그램이 실행되는 경우 운영체제는 프로그램에 실행 권한을 넘겨주고 프로그램이 종료 되면 권한을 돌려줘야 되는데 이를 return을 이용해 진행 
  + 정상이면 `0` return, 비정상이면 `1` return 

`#include` - 컴파일 전에 전처리를 해주는 전처리 기라는 것이 존재하는데 전처리 이 전에 사용하는 지시자를 의미 
<br>
C 운영체제는 출력이 8byte? bit? 단위인가? 
`\n` , `\r` , `\b` , `\t` , `\a`  제어 문자를 통해 출력 형태를 컨트롤 할 수 있다

커서를 컨트롤 하며 수정, 삭제, 하드웨어 제어 등이 가능 


## 프로그램과 데이터
프로그램과 데이터는 별개로 보면 된다
  + 자주 사용되는 고정적인 값들은 프로그램 내에 위치할 수 있지만 보통 데이터는 외부로부터 프로그램으로 이동되며 프로그램은 받은 데이터를 이용해 처리 작업을 진행한다
  + 이 때 프로그램 내의 고정적인 값을 `상수` 라고 한다

### 정수 표현 방법
`014` - 8진수 12
`12` - 10진수 12
`0xc` - 16진수 12

정수는 (`4byte` = 32bit) 크기의 2진수로 변환되어 사용 된다 
  + 만약 4byte 크기 이상의 수가 들어가는 경우 4byte를 늘려 핸들링한다
  + 4 ⇒ 8, `10ll` or `10LL` 형태로 사용하는 경우 4byte로 표현 가능한 10을 의도적으로 8byte 형태로 명시하는 것을 의미한다 
  + 음수도 마찬가지로 `4byte` 크기의 2의 보수 형태로 저장
    + 절대 값을 0과 1을 교체하고 + 1
    
### 실수 표현 방법
소수점 형태, 지수 형태 존재
컴파일러는 실수를 기본적으로 `8byte`로 핸들링
    
64bit에 `부호`, `지수` + `1023(bias)`, 그 외 비트에 유효숫자에 첫번째 자리를 제외하고 나머지를 적음
  + ex) 6.5(실수) ⇒ 110.1(2진수) (정규화)⇒ 1.101 * 2의 2승
  + 메모리 저장 형태- 0 10000000001 101000—
<br>

첫번째 섹션 양수이기에 `0`, 
두번째 섹션 `지수(=2) + 1023 = 1025`
세번째 섹션 유효숫자(1101)에서 맨 앞 1을 제외한 나머지 수를 앞에 적고 그 외 0으로 채움, 맨 앞에 1을 제외하는 이유는 정규화 한 경우 정수 부는 무조건 1이기 때문 

만약 6.5가 아니라 6.4 처럼 소수점 자리가 무한 소수인 경우 64bit에 모든 수가 표현이 되지 않기 때문에 엡실론(epsilon)이라는 오차가 발생한다 
    
### 문자와 문자열
`문자('')` 문자를 사용하면 해당 문자의 아스키 코드 값이 들어감(A인 경우는 65) ⇒ 정수형 상수는 `4byte`로 번역
    
`문자열("")` 문자열 내 문자를 `1byte`로 변환하고 문자열 마지막에 null 문자(00000000)을 붙임
  + 여기서 null은 문자열의 끝 = 마지막이라는 것을 명시해주는 것
## 변환 문자
ex) 실제 연산이 가능한 형태로 사용하기 위해 변환 
```c
printf("%d", 10);
printf("%lf\n", 3.4); // 3.400000 출력
printf("%.1lf\n", 3.4); // 3.4 출력(소수점 첫째 자리까지 표시, 반올림)
```

<br><br><br><br><br>

# 변수
## 정수
int `4byte`
short `2byte`
long `4byte`
long long `8byte`
char `4byte` 
  + 1byte에 저장될 수 있는 크기는 맨 앞 비트는 부호 비트이기에 -2의 7승(8-1)부터 2의 7승 -1까지 이다
    
양수에서 -1을 하는 이유는 0도 양수로 표현하기 때문 
    
```c
signed int a; // default로 양수, 음수 모두 사용한다는 의미
    
unsigned int b; // 양수값 적용으로 사용한다는 것
printf("%u", b); // unsigned로 출력하는 경우
```
    
int, long은 같은 byte인데 굳이?
  + 실질적으로 int, long이 과거와 현재의 하드웨어의 변화에 따라 적혀있는 byte를 정확히 따르지 않는다
  + 하드웨어 스펙에 따라 처리하는 int, long size 다름
        
## 실수
float `4byte`
double `8byte`
long double 10, 12, 16(컴파일러마다 다름), 그냥 double로 처리하는 컴파일러도 있음 
    
## 문자
```c
char str[20]; // char 20개를 저장할 수 있는 메모리를 연속적으로 할당한다는 의미 
char str[20] = "apple"; // a, p, p, l, e, null(종료 시점 체크)
    
str = "banana"; // 이렇게 재할당은 불가, str은 주소값을 지칭하고 있기 때문
strcpy(str, "banana"); // 사용해야된다
```
    
`const` 키워드
```c
const double tax = 0.17;   // 변수 재할당 불가하게함
```

### 명명 규칙
A~Z, a~z. 0~9, (_)- 4가지 표기법 이용해 사용
공백, 특수 문자, 숫자 시작 불가
  + 기존 다른 언어들과 마찬가지로 같음 
  
대입 연산자를 기준으로 왼쪽에 있는 경우와 오른쪽에 있는 경우를 다르게 취급
  + 왼쪽에는 변수의 공간(`L=VALUE`)을, 오른쪽에는 변수가 들어갈 값(`R-VALUE`)을 취급

### extern, static
변수 선언 시 extern 키워드를 사용하는 경우 해당 소스 코드 외부에서 선언된 변수를 참조해서 사용할 수 있다
변수 선언 시 static 키워드를 사용하는 경우 해당 소스 코드 내부에서만 사용 가능하다는 의미이다
  + java와는 다른 개념, 유의

<br><br><br><br><br>

# 연산자
operand(피연산자), operator(연산자)

## 비교 연산
비교 연산자도 순차적으로 실행되는 것을 유의해야된다
    
```c
int x = 10;
if (0 < x < 5) printf("ok")   // ok 출력 
/*
0 < 10을 비교해 1을 반환하고 1 < 5를 비교해 조건문을 만족시키는 결과 도출 
*/
```
    
## and, or 연산자
and, or 연산자 `숏 서킷 룰`
첫 조건의 만족 유무로 이후 조건 검사 유무를 결정 


## 조건 연산
조건 연산자 참, 거짓에 따른 반환 값에 함수나 대입도 넣을 수 있다
이 때 함수는 반환 값이 존재해야된다
    
## 형변환
정수와 실수를 연산하면 4byte, 8byte로 단위 다르기에 직접적으로 연산 불가
연산을 진행하면 정수 ⇒ 실수로 자동(=암시, 묵시적) 형변환을 통해 연산 진행 
  + 코드 상에서 특정 부분에서만 다른 타입으로 사용하고자 하는 경우 명시적 형변환을 이용 
```c
int grad = 100;
double res;
res = (double)grad/90;  // grad만 실수형으로 바꿔주면 암시적 형변환된다 
```
    
## sizeof
변수의 크기를 byte 단위로 계산해줌 
```c
int a = 10;
sizeof a // 함수 아니고 연산자라 괄호 없이 사용 가능
    					// 4 출력(4 byte)
    
int arr[5];
sizeof arr // 20 출력, 배열의 전체 주소를 의미하기에 4byte 5칸 
sizeof arr / sizeof arr[0]  // 배열 요소의 수, 20/4
```
    
## 비트 연산, shift
우측 이동 `/= 2`, 좌측 이동 `*=2`
자료형에 따라 다름
int일 때 우측 이동한 경우 왼쪽에 남는 bit 부호에 맞게 채움, +면 0으로 -면 1로 
  + unsigned는 부호 고려 안하기 때문에 무조건 0으로

<br><br><br><br><br>

# for, continue
for문 내부 마지막으로 가는 것 유의
while문에서는 증감 직접 정의하기 때문에 continue 사용에 유의해야된다, 무한 루프 돔
```c
int i = 0;

while(i < 5){

	continue;

	i++;
} 
```

<br><br><br><br><br>

# 함수, func
`함수명`은 함수가 정의되어 있는 메모리의 시작 위치

매개변수(parameter) = 함수 정의할 때 함께 정의되는 변수 

인수(argument) = 전달 인자, 함수 호출할 때 전달되는 변수

`call by reference`- 주소 값이 전달되는 경우

`call by value`- 변수 값이 전달되는 경우

main 함수를 시작으로 프로그램들을 호출하기 때문에 main 함수에서 만약 다른  함수를 사용하는 경우 main 함수 보다 앞 서 정의 해줘야 된다

함수 선언부만 미리 적어주는 것으로 개선 가능 

```c
int sum(int a, int b);
int main(void) {

}

int sum(int a, int b) {  
	return a + b;
}
```

함수에서 매개변수 없는 경우 정의할 때 void 적어줘야 되며 호출할 땐 괄호만 표기

```c
// 함수 정의
int get_pos(void) {
	int b = 10;
	return b;
}

// 함수 호출
int a = get_pos();
```
  + 반환 값이 없는 경우는 void

보통 C 함수들은 포인터를 이용해 값을 변경하고 0, 1을 반환해주는 방식을 사용하는 것 같다 
## 재귀, stackoverflow
메모리를 안놔주고 계속 물고 있음 ⇒ 메모리 초과 

스택 영역에 함수 호출 관련 정보들이 저장되는데 재귀의 경우 함수가 종료되면서 다음 함수를 호출하는 것이 아니라 물고 있는 상태에서 호출되는 것이기에 메모리를 계속해서 사용하고 있다

<br><br><br><br><br>

# 배열
배열을 정의한 경우 컴파일러는 `배열명`을 배열이 할당 된 공간의 시작 주소로 명시한다 

배열 정의 시

1. 배열 정의할 때 요소 갯수보다 초기 갯수가 적은 경우 0으로 초기화 시켜줌
2. 배열 크기 미 선언 시 초기화 갯수에 맞춰 생성된다

```c
int arr[5] = {1, 2, 3};  // 1, 2, 3, 0 ,0 으로 초기화 된

int arr[] = {1, 2, 3};  // 1, 2, 3 총 3개를 담을 수 있는 배열 초기화된다
```
    
## 포인터 연산
    
컴파일러는 (`주소 값` + `정수`)는 (`주소 값` + (`정수` * `주소가 가리키는 크기`))로 연산을 한다
    
`정수` * (`sizeof 주소 데이터 타입`)이라 보면 된다
    
EX) 주소 값 + 1 진행 시 다음 주소를 가리킴
    
```c
// arr의 시작 주소가 100이라고 할 때 int = 4byte씩 4개 16byte(100~116)가 할당됨   
int arr[4];
    
// arr + 1은 100 + (1*4) = 104를 의미하며 배열의 두번째 요소에 추가된다
*(arr+1) = 2;  // 시작 주소 104가 가리키는 값
    
printf("%d", *(arr+1));  // 2를 출력
```
    
<br>
포인터의 뺄셈 연산을 하고 부호를 통해 어떤 요소가 앞인지 판단 가능
포인터 변수 a - b 가 음수면 b가 더 뒤 쪽 공간을 가리키고 있다는 의미  
구체적으로 (두 주소 간의 값의 차이 % 주소 자료형의 크기)를 반환 

```c
int arr[5];  // arr 변수는 배열의 시작 주소값을 갖고있다
    
arr[0] = 1;   // arr 배열 첫번째에 1이라는 값 할당
*arr = 1;   // 위와 같은 의미의 코드

arr[1] = 2;
*(arr + 1) = 2;  // arr 시작 주소 기준 다음 메모리에 할당

arr[2] = 3;
*(arr + 2);    // arr 시작 주소 기준 다 다음 메모리에 할당
```
  + 배열의 중간 요소들에 포인터를 달고 부분 배열처럼 사용할 수 있다
    
## 배열과 포인터
배열의 이름은 배열이 할당된 메모리의 시작 주소로 변경된다 라고 알 수 있었는데 배열의 시작 주소를 포인터 변수로 할당 했을 때 크기 관련해서 이슈가 발생
밑에 포인터 필기 보는 경우 cpu bit 수에 따라 포인터 변수의 고정적인 크기가 존재(16bit - `2byte`, 32bit - `4byte`, 64bit - `8byte`)
    
```c
int a[4];
double b[4];
int * p = a;
    
printf("%d\n", sizeof a);  // int는 4byte 크기이기에 4byte * 4 = 16 출력
printf("%d\n", sizeof b);  // double은 8byte 크기이기에 8byte * 4 = 32 출력
printf("%d\n", sizeof p);  // 현재 노트북이 64bit로 8byte 출력
```
  + 때문에 만약 배열의 크기를 통해 배열의 요소 수를 추출하고자 한다면 `배열의 시작 주소를 할당한 포인터 변수`가 아니라 `배열의 이름`을 직접적으로 사용하거나 배열의 크기를 따로 계산해서 인수로 전달해야된다  
    

## 문자열 저장
문자열은 기본적으로 char 배열에 저장됨
  + 문자열의 마지막에 null 문자를 넣어줘야 된다, 마침표로 취급, 때문에null이 들어갈 자리를 포함해 정의 필요 
  + 명시적으로도 넣을 수 있지만 크기보다 적은 갯수가 할당되는 경우 자동으로 null이 들어간다 
  + 문자열로 직접 대입도 가능

<br><br><br><br><br>

# 포인터
C는 메모리를 직접적으로 핸들링 할 수 있는 언어이며 이를 위한 수단을 포인터라 말한다
## 왜 사용하는지?
하나의 포인터로 다양한 자료구조 참조 가능

주소 값의 표기는 모두 동일하지만 가리킬 수 있는 데이터의 타입은 여러 종류일 수 있기 때문 

전역 변수의 사용 억제 가능

배열, 구조체 등 복잡한 데이터의 쉽게 접근 및 조작 가능 
  + 동적 할당 함수로부터 메모리를 할당 받고 포인터가 참조하며 값을 핸들링
        
주소 값이 들어 있는 변수 
  + 변수를 저장하는 공간의 시작 주소로 메모리의 주소를 이용해 값을 직접적으로 다루는 방법
  + C 언어는 메모리에 접근해 원하는 방식대로 사용이 가능한 언어 

주소 연산자- `&` 
간접 참조 연산자- `*` , 역 참조라고도 불린다 
```c
int a;
&a // a의 시작 주소 = int 형 저장 공간의 시작 주소

printf("%d", &a);  // 주소값 확인 가능 
printf("%u", &a);  // 주소 값은 양수이기에, 만약 주소 값이 매우 커 sign bit가 1인 경우는 음수로 출력 됨
printf("%p", &a);  // 주소값 출력 전용 변환 문자

*(주소값)  // 시작 주소가 가리키는 공간을 통해 사용(변수값을 통해 X) 
					// 주소가 가리키는 공간과 값 모두를 사용할 수 있다 

/*
8byte(double) 저장 공간을 4byte(int) 포인터 변수로 참조한다면?
=> 이거 불가, 컴파일에서 에러 발생, 프로그램 멈추지 않지만 정상적으로 참조되지 않음  
*/
```

### null pointer
메모리가 할당되지 않은 포인터로 포인터에 메모리를 할당하기 전에 `NULL`인지 확인하고 `NULL`이면 메모리를 할당하는 패턴을 주로 사용 

## 포인터 변수
타입과 변수명 사이에 *를 붙임

이는 컴파일 시 전달하는 요소일 뿐 실제 변수명에 들어가거나 사용되지는 않는다 

간접 참조 연산자와 다른 점은 변수명을 선언할 때  *가 들어가는 경우와 *를 연산으로 사용하는 경우 
    
특정 변수의 시작 주소 값을 저장한다 
```c
int a, b;  // 변수 a의 주소는 100부터 시작한다고 가정, 100~104 총 4byte 존재 
a = 10;  // 변수 a에 10을 할당
int *p;  // 포인터 변수, 자료형에 따라 byte 공간 확보 
         // int 변수의 시작 주소를 넣기 위해서는 int type에 포인터 변수 필요 
    
p = &a;  // 포인터 변수 p에 변수 a의 시작 주소값 100이 적재된다
    
printf("%d", p);  // 100이 출력 
printf("%d", *p);  // 포인터 변수 p가 가리키는 시작 주소값에 들어 있는 변수 10을 출력
```
포인터 변수의 타입은 주소 값이 여러 형태로 들어갈 수 있는 지를 의미하는지 아니면 단순히 들어가는 시작 주소 관련 변수의 타입을 말하는 것인지?
  + 포인터 변수가 가리키는 시작 주소의 저장되어 있는 값의 타입을 의미, 주소 값은 `4byte` or `8byte`로 어떤 포인터 변수 타입으로 선언해도 모두 동일 
  + cpu 종류에 따라 다른데 32bit면 4byte, 64bit면 8byte로 처리 
```c
int a = 10, b = 20;
int *pa = &a;  
    
/*
변수의 값을 받기 위해서 scanf 함수를 사용
scanf는 주소 값을 인수로 사용
a 변수에 값을 입력하기 위해서는 a의 주소값이 필요
*/
scanf("%d", &a);  // a의 주소값
scanf("%d", pa);  // pa는 위에서처럼 a의 주소값을 의미하는 포인터 변수
    
scanf("%d", &pa);  // 형태는 포인터 변수 pa의 시작 주소를 의미하기에 X
    
/*
아래형태는 pa가 가리키는 값을 의미, a의 값을 넘겨준다는 의미
만약에 a의 값이 10이고 메모리 시작 주소 10을 사용하는 변수가 존재한다면 
크리티컬한 이슈가 발생할 수 있다
*/
scanf("%d", *pa);
```
### 초기화
포인터 변수를 따로 초기화 하지 않는 경우 쓰레기 값이 들어가기 때문에 null로 초기화 필요

프로그램에 문제 야기할 수 있다
```c
// pa라는 포인터 변수에 시작 주소가 100인 int 타입 변수의 주소값이라는 의미 
int *pa = NULL;   
pa = (int*)100;
```

메모리의 경우 참조하고 있는 포인터가 참조하지 않는다고 자동으로 해당 메모리가 재사용 가능하게 초기화 되는 것이 아니다
  + 포인터 참조 이전에 `free` 메서드를 통해 해당 포인터가 참조하는 메모리를 재사용 가능하게 초기화하고 참조를 변경하며 메모리 재사용성을 증가시킨다 
### const 포인터
포인터 변수의 저장되는 `시작 주소` 수정 가능 여부
포인터 변수의 저장된 `시작 주소가 가리키는 값` 수정 가능 여부
2개의 조건을 갖고 총 3가지의 경우의 수 존재
#### 참고
얕게 얘기하면 C는 메모리에 접근하는데 있어 일반 변수, 포인터 변수 총 2가지의 입구가 있다고 생각하면 된다
  + 하지만 main 내에 함수들이 포함되어 있는 것이 아니라 분리하는 순간 스코프 단위로 함수 내부에서 사용하는 경우와 외부에서 사용하는 경우 메모리는 공유하지만 일반 변수를 공유하지 못하는 문제(정확하게는 하나의 변수 밖에 반환하지 못함)
  + 때문에 포인터라는 것을 사용해 메모리 주소에 직접 값을 저장하며 사용
  + `const` 키워드는 어느 쪽이든 입구를 막는다는 개념이라 생각하면 될 듯 
  + const의 위치에 따라 수정 여부를 지칭하는 대상(주소, 값 수정 여부) 결정
    + 포인터 변수 타입 앞 뒤에 있는 경우는 시작 주소가 가리키는 값 수정 여부
    + 포인터 변수 직전에 있는 경우는 주소 수정 여부
#### 주소 수정 O, 값 수정 X
```c
int a = 10;
/*
아래 2개의 코드는 동일한 코드라고 보면 된다
자료형 기준 앞 뒤로 const가 존재하는 경우는 같은 것을 의미
변수명 앞에 const 유무로 값 수정 여부 
*/
const int * pa = &a; 
int const * pa = &a;
```
얼마든지 다른 주소를 넣을 수 있다, 
포인터 변수에 저장되는 시작 주소 값을 바꿀 수 있지만 포인터 변수가 가리키는 시작 주소에 있는 값을 바꾸지 못하게 한다
const 변수로 선언하게 되면 쓰레기 값을 계속해서 사용해야 되는 수고가 있는데 const 포인터 변수로 선언된 것을 어느 정도 유연하게 사용가능 하게끔 한다
주소 값을 바뀌며 선택적으로 변수를 상수로 사용할 수 있게끔 함
#### 주소 수정 X, 값 수정 O
```c
int a = 10;
int * const pa = &a;
```
처음 코드와 다르게 const가 포인터 변수명 바로 앞에 온다면 일반 const 변수 선언처럼 처음 선언된 주소 값 외에 수정이 불가하다
#### 주소 수정 X, 값 수정 X
```c
int a = 10;
const int * const pa = &a;
```
  + 단순히 변수 a를 통해서는 바꿀 수 있지만 포인터 변수 pa를 통해서는 바꿀 수 없다

## 포인터 배열
포인터들의 배열, 배열 포인터와는 다른 것 유의 
```c
char * sp[5];   // 총 20byte의 메모리 확보  
    
sp[0] = "dog";  // 첫번째 요소에 할당, sp[0]에 dog 문자열 저장되어 있는 주소값 저장된다 
    
int a[5] = {1, 2, 3, 4, 5};
int b[5] = {11, 12, 13, 14, 15};
int c[5] = {21, 22, 23, 24, 25};
    
int *ap[3] = {a, b, c};  // 위에 a, b, c 배열을 포인터 배열에 할당
    
printf("%d", ap[0][0]);  // 1 출력, 2차원 배열처럼 사용 가능 
```
    

## 응용 포인터
다중 포인터
`int *` → `int **` → `int ***` , 다중 포인터 자료형 예 
  + 이중 포인터, 포인터의 포인터
  + 포인터를 전달 인자(argument)로 사용할 때 매개변수(parameter)는 1depth를 추가한 포인터로 사용
```c
int a = 10;
int *p = &a;  // p라는 포인터 변수의 a의 주소값이 들어간다
int **pp = &p;  // pp라는 포인터 변수의 p의 주소값(a의 주소값이 들어있는 주소값)이 들어간다
    
/*
p를 전달해준다고 할 때 포인터 변수를 이용해 값을 핸들링해야되기 때문에 포인터 변수 이용해 받는다
이 때 int * type의 p이기 때문에 (int *)을 가리키는 포인터 변수로 (int *)* => int ** 사용  
*/ 
int a_method(int ** pa) {
  *pa = 20;  // p가 가리키는 값 a를 20으로 변경하는 코드
}
```
    

## 배열 포인터
배열 포인터는 배열 전체의 시작 주소를 의미
### 1차원
배열명 의미
  1. 첫번째 배열 요소의 시작 주소
  2. 배열 전체의 저장 공간 나타내는 논리적 변수, 해당 배열 전체를 지칭한다, 유의 
```c
int a[5];  // a 배열의 시작 주소 값은 100으로 가정, 100~119까지 저장되어 있다
        
// +1이 의미하는 바가 다르다는 것 유의 
a+1;  // 시작 주소 100 + 4byte = 104byte, 여기서 a는 배열 전체의 시작 주소
&a + 1;  // 시작 주소 100 + 1(배열의 총 크기, 20) = 120byte
```
        
```c
int a[5];  // a 시작 주소 100이라 가정
int (*p)[5];  // p는 int [5]형의 시작 주소를 가리키는 포인터 변수
p = &a;  // 배열 시작 주소를 가리킴, 이 때 배열의 전체 크기를 단위로 가리킨다
        
/* 
p가 가리키는 배열의 첫번째 요소를 10으로 할당
p는 배열 전체를 의미하기 때문에 *p = *&p = a 
  + 괄호 없으면 배열 indexing 우선으로 판단하기 때문에 괄호 필요
*/
(*p)[0] = 10;  
        
// 배열의 시작 주소(100) + 배열 전체 크기 주소값(20) = 120 출력
// 주소값 120 ~ 139에 할당되는 다음 배열 의미 
p+1;
(*(p+1))[0] = 33;  // 주소 120부터 시작되는 int [5] 배열 첫번째 요소에 33 할당 
```
  + 하지만 확보되지 않은 저장 공간이기에 위 코드처럼 배열 전체 주소 포인터에 연산 및 할당 과정을 사용하지 않는다 
        
### 2차원
        
```c
int a[4][5];  // a의 시작 주소 100이라 가정 

/*
2차원 배열은 2중 포인터이기에, a[0]은 5칸짜리 배열의 포인터 변수 
때문에 a+1은 5칸짜리 배열만큼의 다음 주소
*/
a+1 -> 120   
a+2 -> 140

/*
위의 예에 더해 포인터를 한번 더 써줘야 단일 메모리를 지칭한다
*/
(*(a+1))[2]  // a[1][2] 지칭 

/*
2차원 배열을 파라미터로 받는 함수
ap는 100을 가리킴
*/
input_ary(int (*ap) [5]){
...
}
```
        

## 함수, void 포인터
`함수 포인터` 함수의 명령어들이 저장되어 있는 위치
```c
int sum(int a, int b)  // 함수가 있다고 가정
    
int a = 10, b = 20;
    
// 함수 포인터 선언 및 할당 
int (*fp) (int, int);
fp = sum;  
    
// 함수 사용 2가지 방법 
res = (*fp)(a, b);  // 변수 a, b를 sum 함수로 넘겨 반환 받는 코드 
res = fp(a,b);
```
    
`void 포인터` 임의의 주소(포인터)를 다 저장할 수 있음
    
1. (+) 연산 불가, (+) 연산은 자료형 타입만큼 *를 진행해주는 것인데 void는 타입이 명확하지 않아 불가
2. 가리키는 자료형이 명확하지 않아 (*) 간접 참조도 불가
```c
int a;
void * vp

// vp에 a의 주소값 대입, 포인터 변수 입장에서 아직 데이터 타입 모름 
vp = &a;  

vp + 1 // 사용 불가, 자료형 타입 모름

(int *)vp + 1 // 가능, 원하는 데이터 타입을 변환하는 작업 필요

// 값 지칭(a에 40 할당), a의 주소값 할당해도 대입할 때 형 명시 필요 
*(int *)vp = 40;  
```
## 포인터의 구체적인 디테일
1. 조체 내에 구조체 정의되어 있을 때 상위 구조체 메모리 할당 시 내부 구조체 메모리도 함께 할당된다
2. 구조체 포인터는 `->` 간접 멤버 연산자로 접근하며 구조체 변수는 `.` 이용해 접근, 차이점 유의
3. 구조체 내 구조체 포인터가 존재하는 경우 해당 구조체 포인터에 주소 값을 할당해야되며 `->` 연산자로 접근 필요
4. 구조체 내부에 `char *` , `char 변수[]` 두 가지 유의 필요 
    1. `char *`은 외부 메모리에 데이터 저장하고 포인터 참조
    2. `char 변수[]` 은 변수 내부에 데이터 저장
5. 구조체를 함수의 인자로 사용하는 경우
    1. default는 구조체 복사해서 사용, 때문에 값의 변경이 원본 데이터에 영향 주지 않는다
    2. 원본 데이터에 영향을 주기 위해서는 포인터를 사용 필요
        1. 만약 포인터를 사용하며 원본 데이터의 영향을 주지 않고자 한다면 `const` 키워드 사용

구조체 내 일반, 포인터 변수와 구조체
  + 알다시피 단순히 함수 호출을 통해 변수에 값을 할당 할 땐 변수의 주소 값을 넘기고 포인터 형태로 값을 할당
  + 구조체를 선언하는 경우 일반적으로 구조체 내 일반, 포인터 변수, 구조체 등에 맞춰 연속적인 메모리가 할당된다
    + 때문에 구조체 내 일반 변수의 값을 할당할 때는 구조체의 주소 값을 넘기고 `->` 키워드를 이용해 값을 할당
    + 포인터 변수의 경우는 변수에 저장될 수 있는 값은 메모리 주소 값, 때문에 구조체 외부 메모리로 할당하고자 하는 값을 선언하고 포인터 변수의 외부 메모리의 주소 값을 참조하게함
    + 구조체 내 구조체는 다시 일반, 포인터 변수, 구조체 형태로 해당 시점부터 다시 고려하며 진행하면 된다
    
### char[] vs char *
`char *`의 경우 복사하고자 한다면 포인터 변수이기에 메모리를 할당하는 작업 후에 복사 가능
`char[]`은 내부 메모리에 데이터 저장 `char *`은 외부 메모리를 참조하는 형식
    
<br><br><br><br><br>

# 문자열
## buffer
완충제, 완충제 역할을 하는 것을 의미하며 CS에서는 데이터 전송을 할 때 완충 작용을 하기 위한 임시 데이터 저장 공간(char 배열)을 의미 
  + 구체적으로 데이터가 흐르는, 즉 통신하고 입력하고 등의 관련 작업을 하는 주체들의 처리 속도는 다 다르다(ex, 키보드는 초당 1회, cpu는 초당 10회 등)
  + 때문에 버퍼라는 완충 장치가 존재하지 않는 경우 효율이 떨어질 수 밖에 없다(하향 평준화, cpu가 처리 속도를 키보드에 맞춘다)
  + 개행 문자도 함께 저장 
  + fflush 키워드 이용해 버퍼 초기화 시킴 
    
## scanf
sacnf는 우리가 입력한 내용을 직접적으로 호출하는 것이 아닌 버퍼에 저장되어 있는 내용을 호출 
우리가 데이터를 입력할 때 엔터를 이용해 입력의 끝을 알리는데 입력한 데이터는 바로 scanf가 핸들링 하는 것이 아닌 버퍼에 저장 
scanf는 버퍼로부터 값을 받아오는데 만약 버퍼에 입력이 차 있는 경우 추가로 입력 받지 않고 버퍼에서 값을 가져온다 
  + 초기에 버퍼가 비어있을 땐 운영체제에게 제어를 전가하며 운영체제는 사용자의 입력을 받고 그 외 버퍼가 차 있는 경우는 버퍼에서 순차적으로 데이터를 가져온다 
  + 이 때 변환 문자 종류에 따라 버퍼로부터 데이터의 타입에 따라 데이터를 가져올지 스킵할지  다음 데이터를 판단할 판단
```c
/*
입력- tiger
출력- tig
    
1. scanf는 버퍼가 비어있는 경우 운영체제에 제어권 전달
2. 운영체제는 사용자의 입력을 받아 버퍼에 저장
3. scanf는 버퍼를 스캔하며 데이터를 확인
  -1. 데이터가 존재하는 경우 ch 공간에 가져옴
  -2. 없는 경우 다시 1번 형태로 돌아감 
  * 이 때 변환 문자마다 제어 문자를 인식하는지 무시하는지 다름 
 */
char ch;
        
for(int i = 0; i < 3; i++){
  scanf("%c", &ch);
  printf("%c", ch);
}
    
/*
입력
t
i
g
개행 문자 아스키 코드 값 까지 버퍼에 들어가기 때문에
만약 %c가 아니라 %d로 int type을 받는 경우에는 개행 문자를 무시한다
    
출력
116 t
10
15 i
*/
char ch;
    
for(int i = 0; i < 3; i++){
  scanf("%c", &ch);
  printf("%d %c\n", ch, ch);
}
```
    
## gets
scanf의 경우 sp 입력 불가
```c
char str[20];
    
/*
apple jam 입력 시 apple만 저장
*/
scanf("%s", str);  
    
gets(str);  
/*
sp 포함 줄 단위로 입력 받는 함수
    
입력받은 문자열 버퍼에 저장하고 한 글자씩 파싱하면서 배열에 넣어주는 내부 동작 
*/
```
    
### 취약점
저장 공간의 크기를 체크할 수 있는 수단이 없다는 것
개행 문자 전까지만 출력, 개행 문자가 버퍼 맨 앞에 있는 경우 이후 문자 핸들링 불가 
    
## fgets
gets와는 다르게 크기를 제어하며 버퍼로부터 개행 문자 가져옴 
저장 공간의 크기 -1 만큼만 저장한다, 마지막에 null 문자가 들어가야 되기 때문
```c
char str[20];
fgets(str, sizeof(str), stdin);
```
    

## printf
문자열 출력할 때 문자열을 특정 메모리에 따로 저장해놓고 해당 메모리의 시작 주소를 이용해 출력 
주소값이 들어가 있기에 포인터로 이용 가능 
```c
printf("%c", "apple"[2]); // p 출력됨
```
    
## puts
문자열 출력, 자동 줄바꿈
```c
char str[20];
    
puts(str);
```
    

## 포인터 변수로 문자열 핸들링
하지만 문자열을 할당하지 않고 정의만 한 경우에 재할당이 안되는 문제 발생(포인터 변수는 주소값만 저장이 가능하기 때문)
선언 시 할당을 함께하면 알아서 특정 메모리에 저장하고 메모리 시작 주소가 포인터 변수에 저장되지만 선언과 할당을 분리한다면 알아서 작업되지 않기 때문
```c
// apple이라는 문자열은 특정 메모리에 따로 저장되고 cp에 메모리 시작 주소가 저장된다 
char * cp = "apple";  

printf("%s", cp);  // apple 출력
printf("%s", cp+1);  // pple 출력 
```

<br><br><br><br><br>

# 변수
## 지역 변수
```c
auto int a = 0;  // auto는 default
int a = 0;  // auto 취급
```
지역 변수 원리를 이용해 main 함수 내부에 작업을 중괄호를 이용해 사용 가능
  + 이 때 해당 중괄호 작업 끝나면 내부에서 사용한 변수들 자동으로 정리된다 
  + 중괄호 내부에서 main 함수에서 사용되는 변수들을 사용할 수 있다
  + 중괄호 내부에 main에서 사용되는 변수 명을 같게 선언할 수 있지만 컴파일러는 가장 가까운 변수를 위주로 취급 
```c
int main(void) {
  int a = 10;
  {
    int temp = 3;
    a *= temp;
  }
}
```
    

## 전역 변수
알다시피 어디서든 사용 가능 
여기저기 다 사용하기 때문에 디버깅 힘들고 수정도 힘듬
```c
int a;  // 0으로 자동 초기화 
int main(void) {
  printf("%d", a); // 0출력
}
```
    


## 정적 지역 변수
전역 변수와 거의 같지만 사용 범위가 함수 내부에서만 사용 가능함 
```c
static int a;  // static 이용해 선언 
```
  + 함수 호출될 때마다 저장 공간의 생성, 삭제가 반복되는 것이 아닌 최초의 컴파일 시 저장 공간이 생성되고 해당 함수가 종료되었을 때 삭제되지 않음
  + 계속해서 사용된다, 함수가 끝났을 때가 아닌 프로그램이 끝날 때 까지 사용 
    

## 레지스터 변수
지역 변수에서만 사용 가능
```c
register int i;
```
딱 1개를 제외하고 지역 변수와 모두 같음
  + 지역 변수는 메모리에 할당, 레지스터 변수는 cpu에 할당
    + 주소 사용 불가, 주소는 메모리의 주소이기 때문, CPU는 주소 사용 X 
  + cpu 접근이 메모리 접근보다 효율적이기 때문에 일부 사용

<br><br><br><br><br>

# 동적 할당 함수
데이터를 저장하기 위한 메모리 저장 공간을 동적으로 할당 
변수명이 없기에 포인터 이용해서 사용할 수 밖에 없다 

프로그램이 실행 중에 입력되는 데이터들을 핸들링하기 위해서 필요한 기능
  + 우리가 프로그램이 실행되기 이전에 프로그램 내에서 사용되는 모든 데이터들의 타입, 크기, 갯수 등을 알 수 없기 때문에
    
## 프로그램에서의 메모리 사용 영역
`코드 영역`- 실행할 프로그램의 코드가 올라가는 메모리 영역
`데이터 영역`- 프로그램의 전역 변수, 정적 변수, 문자열 상수가 저장되는 영역 
`스택 영역`- 함수 호출과 관련된 지역 변수, 매개변수가 할당되는 메모리 영역
`힙 영역`- 사용자가 직접 관리할 수 있고 해야만 하는 영역, 사용자에 의해 동적으로 할당, 해제

코드가 실행 되기 전에 코드는 `코드` 영역에 올라가고 코드의 전역, 정적 변수, 문자열 상수 등은 `데이터` 영역에 올라간다. 코드의 함수와 관련된 데이터들은 `스택` 영역에 들어가고 코드가 실행이 되면서 사용되는 영역은 `힙`에 저장된다 
### 참고
`스택` - `힙` 영역은 서로 붙어 있다(스택이 할당 속도가 훨씬 빠름)
`데이터`, `스택` 영역에 할당되는 메모리의 크기는 컴파일 타임에 미리 결정됨
  + `힙` 영역의 크기는 프로그램이 실행되는 런 타임 시 사용자가 직접 결정 
#### `overflow`
스택은 위에서 아래로 메모리가 채워지며 힙은 아래에서 위로 채워지는데 이 때 두 공간의 메모리 주소가 겹치는 경우를 의미
`stackoverflow`- 스택이 힙 영역을 침범한 경우
`heapoverflow`- 힙이 스택 영역을 침범한 경우 

        
### 정적, 동적 할당 관련
컴파일 시점에 소스 코드를 읽고 메모리 공간을 확보하는 것을 정적 할당(`staticallocation`), 프로그램이 실행되는 런타임 중에 메모리 공간을 확보하는 것을 동적 할당(`dynamic allocation`)
  + 결론적으로 메모리를 보다 효율적으로 사용하기 위해 컴파일 때 고정적으로 사용되는 메모리의 크기를 줄이며 런타임 시에 유도리 있게 메모리를 사용하고자 하는 목적  
## malloc
동적 할당 함수
        
힙 영역에서 메모리 할당
        
지역 변수와 다르게 특정 함수가 마칠 경우 자동으로 반납되지 않는다 
        
메모리를 연속적으로 할당하기 때문에 빈 공간들이 존재해도 `연속적`으로 할당되지 못하는 상황이라면 할당되지 못한다  
  + 성공하면 `메모리 주소`를 반환, 실패하면 `NULL`을 반환
        
```c
int *p;  // 스택 영역에 할당
        
/*
byte 단위로 사용하고자 하는 메모리를 전달, sizeof 이용 
확보한 메모리의 첫번째 주소값 void 포인터로 형변환해서 반환
*/
        
// 결국 스택 영역에 할당된 포인터 변수 p에 힙 영역에 할당된 malloc의 반환 주소가 들어가 있다
p = (int *)malloc(byte 단위);
        
free(p);  // 동적 할당 받았던 메모리 공간 반납
```
        
## calloc
처음 생성 시 0으로 자동 초기화 시켜줌, 초기화하는데 시간 소모 
```c
calloc(5, sizeof(int));  // int 크기 5개만큼 동적 할당 
```
        
## realloc
```c
// 이미 할당되어 있는 포인터 변수, 조정하고자 하는 크기
p = (int *)realloc(p, 8); // 포인터 변수 p의 크기를 8byte로 변경 
// null pointer인 경우는 두번째 인자 크기로 새로 할당한다 
```
        
    
## 동적 할당 응용
메모리를 효율적으로 사용하고자 동적 할당을 사용  
```c
/*
임시 문자열 temp를 이용해 메모리 동적 할당 
*/
int main(void)
{
  char temp[200];
  char *sp[3];
  int i;
    
  for(i = 0; i < 3; i++){
    gets(temp);
    sp[i] = (char *)malloc(strlen(temp) + 1);
    strcpy(sp[i], temp);
  }
    
  for(i = 0; i < 3; i++){
    printf("%ds\n", sp[i]);  // 주소값이 정상적으로 출력되는지 확인 
  }
    	
  for(i = 0; i < 3; i++){
    free(sp[i]);
  }
}
```
명령행(사용자가 직접 명령을 입력하는 행) 인수, 프로그램이 실행될 때 전달되는 변수
  + main 함수 void → 인수
```c
int main(void) {}  
int main(int argc, char **argv) {}  // argc- 명령형 인자 갯수, argv- 주소값(이중 포인터)

```
<br><br><br><br><br>

# 구조체
하나 이상의 변수를 묶어 새로운 자료형을 정의하는 도구, 자료형 
1. 기본(=내장) 자료형
  + int, double 등 
2. 응용 자료형
  + 배열, 포인터 등
```c
// 사용 전 구조 선 정의 필요, 전체 멤버 변수 크기 합한만큼 메모리 할당
struct student
{
  int num,  // 변수 선언 아님, 메모리 할당 X
  double grade
};
    
int main(void){
  struct student a;  // 멤버 변수의 크기를 모두 합한 16byte 메모리 할당 
    
  a.num = 10; // 이용해 student 구조체의 a 인스턴스 num 접근, 이 상황이 int 변수와 동일하다 보면 된다
  scanf("%d", &a.num);  // 입력을 받을 수도 있다  
};
```
실질적으로는 12byte가 아니라 16byte 정도 잡히는데 이는 패딩 byte라 한다 
  + `byte alignment`, CPU가 메모리 접근 시 접근 효율을 높이기 위해 일정 byte 기준(8byte)으로 접근 
  + 하지만 메모리를 심각하게 먹는 경우도 발생할 수 있다 
  + 기준 범위(8byte) 내에서 할당이 가능하면 할당된다
    + char, short 순서라면 1234 중에 1, 34 식으로 할당 

## 구조체 별칭
구조체 변수를 추가적으로 정의할 수 있는 방법
```c
typedef struct student
{
	~
	~
} Student
```
  + Student라는 키워드로 struct student 구조체를 정의할 수 있다
## 구조체는 대입, 복사, 반환 등의 연산 가능
구조체 변수는 단순히 사용 가능
```c
struct vision
{
  double left;
  double right;
};
        
// 구조체를 매개변수로 변수에 직접 대입 가
struct vision swap(struct vision b){
  double temp;
  temp = b.left;
  b.left = b.right;
  b.right = temp;
        
  return b;
};
        
int main(void){
  struct vision a = {1.5, 2.0};
        	
  a = swap(a);
  printf("%.1f, %.1f\n", a.left, a.right);
};
```
        
         
        
    
## 비트 필드 구조체
비트 단위로 구조체 처리
  + 멤버로 배열 선언 불가 
  + 주소 연산 불가
    + 주소 연산은 byte 단위로 이루어지는데 bit 필드 구조체는 말 그대로 단위가 bit이기 때
    + 주소 연산이 불가하기 때문에 키보드로 직접 입력도 불가(scanf는 주소 값으로 입력 받기 때문)
        
```c
struct bit_field
{
  unsigned int son:2;  // 2bit
  unsigned int daughter:2;  // 2bit
  unsigned int pet:3;  // 3bit
};
        
struct bit_field
{
  unsigned int son:2;  // 2bit
  unsigned int 2;  // 2bit 패딩 비트 
  unsigned int daughter:2;  // 2bit
  unsigned int pet:3;  // 3bit
};
        
```
        
## 구조체 활용
### 구조체 포인터
`->`- 간점 멤버 접근 연산자
```c
struct score
{
  int kor;
  int eng;
  int meat;
};
        
int main(void)
{
  struct score a;
  struct score * sp = &a;  // sp는 a 전체를 가리킴 
        	
        
  // 값을 할당하는 3가지 방법
  a.kor = 90;
  a.eng = 80;
  a.mat = 70;
        
  (*sp).kor = 90;  // 괄호 안하면 (.)이 우선 순위 높아 오류 발생 
  (*sp).eng = 80;
  (*sp).mat = 70;
        
  sp -> kor = 90;  // -> 연산은 위에 (*). 연산을 간략화 시킨 것 
  sp -> eng = 80;  // 왼쪽에 구조체 포인터, 오른쪽에 구조체 멤버 변수 
  sp -> mat = 70;
};
```
        
### 구조체 포인터 연산
```c
struct score
{
  int kor;
  int eng;
  int meat;
};
        
void print_st(struct score *p);
        
int main(void)
{
  struct score a;
  struct score * sp = &a;  
        	
  a.kor = 90;
  a.eng = 80;
  a.mat = 70;
        
  print_st(&a);
};
        
void print_st(struct score *p)
{
  // 두개 같은 출력 
  printf("%d", p->kor);
  printf("%d", (*p).kor);
};
```
        
### 구조체 배열
```c
struct address
{
  char name[20];
  int age;
  char tel[20];
  char addr[80];
};
        
void print_ary(struct address *p);
        
int main(void)
{
  struct address a[5];  // 배열의 각 요소들이 address 구조체로 이루어짐
        												// 생성자 만드는 것처럼 초기화 가능 
        	
  printf("%s", a[0].name);
  printf("%d", a[0].age);
        	 
  print_ary(a);
};
        
// 구조체 포인터 배열 a 순차 출력하는 함수
void print_ary(struct address *p)
{
  int i;
        
  for(i = 0; i < 5; i++){
    printf("%s", p->name);
    printf("%d", p->age);
    p++;  // 
  }
};
```
        
### 자기 참조 구조체
```c
struct list
{
  int num;
  struct list *next;
};
        
int main(void)
{
  struct list a = {10}, b = {20}, c = {30};
        
  // a next가 b를 b next가 c를 지칭하며 single linked-list 생성된다 
  a.next = &b;
  b.next = &c;
        
  // single linked-list로 a, b, c 모든 num에 접근 가능 
  a.num
  a.next -> num
  a.next -> next -> num
};
```
위의 코드에서 포인터 변수 이용해 num에 접근하는 경우는 list가 길어질수록 코드의 가독성 반비례
  + 아래 코드 이용해 개선 가능 
```c
/*
head point, 보통 구조체 배열의 첫번째 주소를 따로 기억해둔다
첫번째 노드를 가리킨다  
*/
struct list* tp = &a;
struct list* head = &a;
        
while(tp != NULL)
{
  printf(%d", tp->num);
  tp = tp->next;
};
```

<br><br><br><br><br>

# 공용체, UNION
구조체와 많은게 유사
    
차이점은 멤버 변수 중 크기가 가장 큰 멤버의 크기만큼 메모리 공간을 확보하고 저장 공간을 멤버들끼리 공유
```c
union student
{
	int num;
	double grade;
};

int main(void)
{
	union student a;

	a.num = 365;
	printf("%d\n", a.num);

	a.grade = 3.5;
	printf("%d", a.num);  // grade가 저장 공간을 사용 중이기에 존재 X 
};
```

<br><br><br><br><br>

# 열거형
초기화, 기호화 해서 처리해준다 
  + spring- 0
  + summer- 1
  + fall- 2
  + winter- 3

열거형은 가독성은 물론 바운더리를 지정한다
  + 열거형 외 타입은 할당하지 못하기 때문

```c
enum season{spring, summer, fall, winter};

enum season a;
a = spring;
if (a == spring) {
	printf("~~~");
}
```

<br><br><br><br><br>

# typedef, 형 재정의
인위적으로 타입 관련 키워드를 추가해줄 수 있다 

```c
typedef int INT; // INT라는 이름으로 int 타입으로 정의 가능하다
typedef int* IP;  // int *를 IP로 정의해서 사용 가능

typedef struct student Student;  // struct student를 Student로 정의 가능하게 한다 
Student a;  // 구조체 정의 
```

<br><br><br><br><br>

# ref
- <a href="https://wonit.tistory.com/546#comment12685164">컴파일 1</a>
- <a href="https://wonit.tistory.com/547">컴파일 2</a>
- <a href="https://hongong.hanbit.co.kr/c언어-포인터를-사용하는-이유/">포인터 1</a>
- <a href="https://wn42.tistory.com/89">포인터 2</a>
- <a href="https://coding-factory.tistory.com/636">포인터 3</a>
- <a href="https://blog-of-gon.tistory.com/199">buffer</a>
- <a href="https://velog.io/@wonhee010/%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0-feat.-%EC%9E%AC%EA%B7%80-vs-%EB%B0%98%EB%B3%B5%EB%AC%B8">메모리 구조</a>
- <a href="https://velog.io/@saint6839/C%EC%96%B8%EC%96%B4-%EB%8F%99%EC%A0%81-%EB%A9%94%EB%AA%A8%EB%A6%AC-%ED%95%A0%EB%8B%B9-%EA%B0%9C%EB%85%90-%EC%9E%A1%EA%B8%B0">동적 메모리 할당</a>
- <a href="https://tcpschool.com/c/c_memory_malloc">동적 할당 함수 malloc</a>
- <a href="https://programfrall.tistory.com/20">헤더 파일 관련 1</a>
- <a href="https://ko.wikipedia.org/wiki/헤더_파일">헤더 파일 관련 2</a>
- <a href="https://losskatsu.github.io/programming/c-header/#헤더-파일을-사용하지-않고-프로그래밍하기">헤더 파일 관련 3</a>
- <a href="https://code4human.tistory.com/110">헤더 파일 관련 4</a>