---
tags:
  - Hadoop
  - Linux
---
### 2. Linux 설치 
---------------------------

> [!info]- ifconfig 설치 방법
> yum install net-tools


>[!note]+ 제목
>ㅁㄴㅇㄻㄴ
>ㄴㅁㅇㄹㄴㅁ






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



### 4. 하둡설치
-------------------------------------------------
#### 호스트 네임 설정

	- ip로 접속하는 것보단 호스트네임으로 설정하는것이 직관적으로 서버를 찾기 편하고,
	    DHCP 특성상 IP가 변경되어도 호스트 네임은 변경되지 않기 때문에 사용함

> [!note]- 호스트명 변경 명령어
> - hostnamectl set-hostname "변경할 호스트명"
> - eg : hostnamectl set -hostname master

#### 호스트 설정



#### 리눅스 계정 생성



#### hadoop 계정 sudo 권한 추가



#### hadoop SSH 접속



#### 마스터 서버 SSH 키 생성하기



#### 마스터 서버 SSH Key 파일 전달



#### 마스터 서버 > 슬레이브 서버1 SSH 접속
