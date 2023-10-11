---
tags:
  - Hadoop
  - Linux
---
### 2. Linux 설치 
---------------------------

> [!info]- ifconfig 설치 방법
> yum install net-tools



### 3. 리눅스 필수 유틸 설치
-----------------------------------------------------

> [!important]- 최신 버전 패키지 설치
> 리눅스 설치 후, 가장 먼저 해야하는 작업
> 
> - yum update -y

#### SSH란?

> SSH(Secure Shell)는 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고
> 다른 시스템으로 파일을 복사할 수 있도록 해주는 응용 프로그램 또는 그 프로토콜

#### VIM 설치

>[!note]- 설치 명령어
>- yum install -y vim

	vi 편집기 대신 항상 vim 편집기로 사용 설정
	1. etc/profile 설정
	2. 가장 마지막 줄에 alias vi = 'vim' 명령어 추가
	3. source /etc/profile 수정된 내용 centOS에 적용

