특수 권한

- UNIX 시스템은 파일에 대한 접근 권한 및 파일 종류흫 나타내기 위해 16bit를 사용

- 각 3bit씩 총 9bit, 소유자 접근 권한, 그룹 접근권한, 기타 사용자 접근권한을 기술하는데 사용

- 4bit는 파일의 종류 표현에 사용

- 3bit는 특수권한에 사용

Set-UID

- set-uid 비트 : 8진수 4000

- 비트를 실행 파일에 적용하면 실사용자에서 프로그램 소유자의 ID로 유효 사용자(EUID)가 변경

  1. 비트를 설정하는 경우

     - root 만 접근할 수 있는 파일이나 명령에 대해, 일반 사용자로 접근하는 것이 기능상 필요한 경우
     - 실행하는 순간에만 그 파일의 소유자 권한으로 실행
     - 매번 root의 권한으로 실행 하지않아도 되기 때문에 효율적

  2. 보안에 취약함

  3. 비트 설정 방법

     - 8진수(4000)이나 u+s를 이용하여 설정 가능(비트 제거시 u-s)

- 설정된 파일을 실행할 떄 파일의 소유자의 권한을 얻어 실행할 수 있도록 하는것

- root 권한없이 일반 사용자도 접근이 가능한 것

- 대표적으로 /usr/bun/passwd 파일



Sticky-Bit
- 외부 권한 변경 (공유 디렉토리)
- chmod o+t or 1***
- 공용으로 사용 가능한 디렉터리 생성을 요청 받아서 같은 그룹으로 묶은 후에 공유 디렉터리로 설정
- 파일을 삭제할 때는 파일 생성자(소유자)만 삭제할 수 있다.
- stick-bit가 부여된 디렉터리 : /tmp


chmod

- 파일, 디렉토리의 권한을 수정하는 명령어

umask

- 파일이나 디렉터리 생성 시 부여되는 기본 허가권 값을 지정하는 명령어
- -S : 심볼릭 값을 보는 명령어

chown

- 파일 소유자, 소유그룹을 수정할때 사용하는 명령어
- -R : 경로와 그 하위 파일들을 모두 변경한다.
- -c : 변경된 파일만 자세하게 보여준다.
- -f : 변경되지 않은 파일에 대해서 오류 메시지를 보여주지 않는다.
- -v : 작업 상태를 자세히 보여준다.

chgrp

- 사용자그룹 변경
- -R : 지정한 디렉토리 아래에 있는 모든 파일도 함께 지정한 그룹으로 변경한다.
- -c : 작업상태를 자세히 보여주거나, 실제로 변경되는 것만 보여준다.
- -f : 그룹이 변경되지 않은 파일들에 대한 오류 메시지를 보여주지 않는다.
- -h : 심볼릭 링크가 지정하는 것 대신에 심볼릭 링크 자체의 그룹을 변경한다.

저널링

- 리눅스 커널 2.4 버전부터 파일 시스템 기능이 있는 ext3을 사용하였고, 시스템에서 충돌이 발생하거나 전운 문제가 발생한 경우에 데이터 복구 확률을 높여준다.

저널링 파일 시스템

- 파일 시스템에 대한 변경사항을 반영하기전에 저널이라 부르는 로그에 변경사항을 저장하여 추적이 가능하게 만든 파일 시스템
- 시스템에 충돌현상이 발생하거나 전원 문제가 발생된 경우에 데이터 복구 확률을 높여준다.
- ext3 부터 저널링 파일 시스템 기능이 있다.

mkfs

- 새로운 파일 시스템을 만드는 명령으로 root만 사용 가능하다. 파일 시스템 유형을 지정하지 않으면 ext2으로 생성된다.

mke2fs

- ext2, ext3, ext4 파일 시스템을 만드는 명령으로 최근 리눅스 배포한에서 mkfs 명령 실행 시 실제 사용되는 멸령어이다. 파일 시스템의 유형을 지정하지 않으면 ext2로 생성된다.

eject

- 보조 기억장치의 미디어를 꺼낼때 사용하는 명령어

fdisk 

- -q --> 변경된 파티션의 정보를 저장하지 않고 종료
- -t --> 파티션 속성 변경
- -d --> 파티션 삭제
- -s --> 파티션 크기 출력

blkid

- 현재의 하드디스크의 파티션에 부여된 UUID의 값을 볼 수 있는 명령어
- /etc/blkid/blkid.tab 에 캐싱된 정보 데이터가 저장되어있음

UUID(Universally Unique Identifier)

- 범용 고유 식별자
- 16byte로 이루러진 규격화돤 숫자
- 보통 여러 개체들이 존재하는 환경에서 식별하고 구별하기 위해서 사용되는 고유한 이름을 통칭한다.
- 최근 리눅스에서 파티션을 생성하면 고유한 이 값이 부여된다.

df

- 시스템에 마운트된 하드디스크의 남은 용량을 확인할 때 사용하는 명령어
- 경로 —> /bin/df
- 옵션
  1. -T, —print-type —> 파일 시스템의 형태를 추가하여 각각의 파티션 정보를 출력
  2. -t, —exclude-type=TYPE —> 지정한 형태(TYPE)을 제외하고 나머지 모든 파일 시스템 정보를 출력
  3. -h, —human-readable —> 사람이 읽을 수 있는 형태의 크기로 출력
  4. -a, —all —> 0 블록의 파일 시스템을 포함하여, 모든 파일 시스템을 출력
  5. -i, --inodde —> 파티션별 블록 사용 정보 대신 inode 정보를 표시함

bash

- 본 셸을 기반으로 하여 GNU 프로젝에 의해서 개발
- 브라이언 폭스가 만듬
- GNU 운영체제, 리눅스, 맥 OSX 등 다양한 운영체제에서 사용 중
- 현재 리눅스의 표준 셸

ksh

- AT&T 사의 데이비드 콘(David Korn)이 개발하고, 명령어 완성 기능, 히스토리 기능 등을 제공

export

- 명령어를 통해서 쉘 변수를 환경변수로 저장

env

- 현재 셀에서 설정된 환경 변수의 값을 확인 하는 명령어
- 글로벌 환경변수 조회 명령어

set

- 셸 변수 확인 명령어

환경변수

1. PATH —> 실행할 명령어를 탐색하는 경로
2. SHELL —> 로그인 셀에 대한 경로
3. TMOUT —> 입력이 일정시간 없으면 연결 종료
4. HOME —> 홈 디렉터리에 대한 경로

exec

- 원래의 프로세스를 새로운 프로세스로 대체하는 형태로 호출한 프로세스의 메모리에 새로운 프로세스의 코드를 덮어씌워 버림

chown
- 소유권 변경
- -R 옵션을 주면 해당 디렉토리 + 하위 디렉토리까지 변경

디스크

du
- 특정 디렉토리를 기준으로 디스크 사용량을 확인
- -h 옵션을 사용하여 디스크 사용량을 K, M, G 단위로 확인
- 디렉토리 이름을 지정하지 않으면 현재 디렉토리를 기준으로 디스크 사용량을 출력
- 디렉토리 안에 있는 서브 디렉토리의 디스크 사용량도 표시
- 옵션
  - -s : 지정한 파일이나 디렉터리의 총 사용량 출력
  - -h : 알아보기 쉽게 적당한 단위별로 출력

df
- 리눅스 시스템 전체의 (마운트 된) 디스크 사용량을 확인
- 파일시스템, 디스크 크기, 사용량, 여유공간, 사용률, 마운트지점 순
- USB메모리나 SD카드의 저장공간도 여기서 확인이 가능
- 옵션
  - -h : 옵션을 사용하면 사람이 보기 좋게 메가(M), 기가(G) 단위로 디스크 공간을 확인
  - -T : 파일시스템의 종류를 확인할 때 입력하는 옵션
  - -t : 보여주는 목록을 파일 시스템의 타입으로 제한
  - -a : 0 블록파일의 시스템을 포함하여, 모든 파일시스템을 출력

fstab
- 파일시스템 정보를 저장하고 있으며, 리눅스 부팅시 마운트 정보를 저장하고 있음
- 옵션
  - usrquota —> 사용자 쿼터 설정
  - grpquota —> 그룹 사용자 쿼터 설정
  - qutaon —> 쿼터 활성화

디스크 쿼터(DIsk Quota)

- 파일 시스템마다 사용자나 그룹이 생성할 수 있는 파일의 용량 및 개수를 제한한다.
- 보통 블럭 단위의 용향 제한과 inode의 수, 사용자나 그룹에게 할당된 디스크 블록 수를 제한한다.

shell

- 사용자로 부터 명령을 받아 해석하고 프로그램을 실행하는 역할
- 프로그램할 수 있는 여러가지 기능을 가지고 있음
- 운영체제와 사용자간의 대화식 인터페이스 제공
- 입력된 내용을 파악해서 명령 줄을 분석
- 파이프, 리다이렉션, 백그라운드 프로세스 실행
- 셀 확인 명령어 : ps
- 처리 과정 : Shell <—> Kernel <—> Hardware
- bash
  - 1989년 브라이언 폭스가 GNU 프로젝트를 위해 개발한 셀
  - 명령 히스토리, 명령어 완성 기능, 히스토리 치환, 명령행 편집 등을 지원
  - 본 셀을 기반으로 하여 제작
- csh
  - 1978년 버클리대학의 빌 조이가 개발
  - C언어를 기반으로 만들어짐
  - 강력한 작성기능, 히스토리 기능, 별명(Alias)기능, 작업제어 등의 기능을 포함
- tcsh
  - 켄 그리어가 테넥스라는 운영체제에서 명령행 완성기능을 반영
  - 1981년 C셸과 통합하여 만듬
  - C셸의 기능을 강화시킨 셸로 명령어 완성기능, 명령행 편집기능 등을 추가로 지원한다.
- nano
  - pico 가 자유 소프트웨어 라이선스가 아니었디 때문에 GNU 프로젝트에 의해서 pico의 복제버전으로 개발 되었다.
- pico
  - University of Washington에서 개발되었으며 현재 Apache 라이센스이다.
  - 기본 인터페이스는 noteped와 유사하여 매우 단순
  - 쉽고 사용하기 편리하지만 기능이 부족하고 업데이트가 잘 되지않고 있다.
  - Ctrl + X : 프로그램 종료
  - Ctrl + n : 커서를 아랫줄로 이동
  - Ctrl + b : 커서를 뒤(왼쪽)로 이동
  - Ctrl + f : 커서를 앞(오른쪽)으로 이동
  - Ctrl + p : 커서를 윗줄로 이동
- vim
  - 브람 무레나르가 만든 편집기
  - 편집시 다양한 생상을 이용하여 가시서을 높임
  - ex 모드에서 히스토리 기능 제공
  - 확장된 정규 표현식 문법, 강력한 문법 강조 기능
  - 다중 되돌리기 기능 및 유니코드를 비롯한 다국어 지원, 문법 검사 등의 기능도 지원
  - vi 편집기와 호환되면서 독자적으로 다양한 기능을 추가하여 만든 편집기
- emacs
  - LISP 언어를 기반으로 만듬
  - 리처드 스톨만이 만든 편집기
  - Alt + d : 커서가 위치한 부분부터 단어를 삭제
  - Alt + k : 커서가 위치한 부분부터 문장 전체를 삭제
  - Ctrl + n : 현재 커서가 위치한 줄의 화면 아래로 이동
  - Ctrl + a : 현재 커서가 위치한 줄의 처음르로 커서를 이동

alias

- 특정 명령어 실행 시에 자주 사용하는 옵션을 등록하여 사용하거나 나만의 새로운 명령어 조합을 만들 때 유용하다.
- 별칭, 가칭이라는 뜻을 가지고 있다.

kernel

- 컴퓨터가 부팅도리 때 주기억 장치에 적재된 후 상주하면서 실행
- 하드웨어를 보호하고, 프로그램과 하드웨어 간의 인터페이스 역할을 담당
- CPU 스케줄링 관리, 기억 장치 관리, 파일 관리, 입출력 관리, 프로세스간 통신, 데이터 전송 및 변환 등 여러가지 기능을 수행

ps

- 총 CPU 사용시간
- 부모 프로세스의 PID
- 현재 프로세스의 상태 코드

top

- 시스템의 상태를 전반적으로 가장 빠르게 파악 가능
- 옵션 없이 입력하면 interval 간격으로 화면을 갱신하여 보여줌
- ps와 차이점
  - ps는 ps한 시점에 proc에서 검색한 cpu 사용량
  - top은 proc에서 일정 주기로 합산해 cpu 사용율 출력
- 옵션
  - 실행 상태에서 [t] : 프로세스와 CPU항목을 on/off 한다.
  - 실행 상태에서 [c] : Command line의 옵션을 on/off 한다.

exec

- 원래의 프로세스를 새로운 프로세스로 대체하는 형태로 호출한 프로세스의 메모리에 새로운 프로세스의 코드로 덮어씌워 버린다.
- fork 처럼 새로운 프로세스를 위한 메모리를 할당하지 않고, exec 에 의해 호출된 프로세스만 메모리에 남겨둔다.

fork

- 하나의 프로세스가 다른 프로세스를 실행하기 위한 시스템 호출방법
- 새로운 프로세스를 위해 메모리를 할당받아 복사본 형태의 프로세스를 실행
- 프로세스 생성의 한 방법으로 새로운 프로세스를 원래의 프로세스의 자식 프로세스로 관리하는 방식

bg

- stop 상태인 것을 백드라운드로 실행

fg

- stop 상태인 것을 포그라운드로 실행

nohup

- 프로세스가 중단되지 않는 백그라운드 작업으로 실행
- 표준 출력을 nohup.out으로 돌리는 작업을 실행

nice

- 우선순위 조절

synaptic

- APT 패키지 관리 시스템으로 GTK+ 기반의 GUI 도구

fsck

- 운영 중인 리눅스 서버의 파일시스템에 손상된 디렉터리나 파일을 수정할 때 사용하는 명령어
- /lost+found : fsck 명령 실행 시에 발생한 오류 파일들이 위치하는 디렉토리

mount

- 파일 시스템 구조내에 있는 일련을 파일들을 사용자나 사용자 그룹들이 이용할 수 있도록 만드는 것
  - 옵션
    - -a : /ect/fstab에 기술되어 있는 모든 파일 시스템을 마운트한다.
    - -t : 파일시스템의 형식을 저장한다.
    - -n : /etc/mtab 파일에 정보를 넘기지 않고 마운트한다.
    - -o : 마운트 옵션을 사용한다.
      - ro : 읽기 전용으로 마운트
        - loop : Loop 디바이스나 CD-ROM 이미지 파일 ios 마운트

| **변수**     | **내용**                                                     | **변수**     | **내용**                                   |
| ------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------ |
| HOME         | 현재 사용자의 홈 디렉터리                                    | PATH         | 실행 파일을 찾는 디렉터리 경로             |
| LANG         | 기본 지원되는 언어                                           | PWD          | 사용자의 현재 작업 디렉터리                |
| TERM         | 로그인 터미널 타입                                           | SHELL        | 사용자의 로그인 셸                         |
| USER         | 사용자의 이름                                                | DISPLAY      | X윈도에서 프로그램 실행 시 출력되는 창     |
| COLUMNS      | 현재 터미널의 컬럼 수                                        | LINES        | 현재 터미널 라인 수                        |
| PS1          | 1차 명령 프롬프트 변수                                       | PS2          | 2차 프롬프트 변수, 기호와 관련된 환경변수  |
| BASH         | bash 셸의 경로                                               | BASH_VERSION | bash 버전                                  |
| HISTFILE     | 히스토리 파일의 절대 경로                                    | HISTSIZE     | 히스토리 파일에 저장되는 명령어(줄)의 개수 |
| HISTFILESIZE | 히스토리 파일의 크기                                         | HOSTNAME     | 시스템의 호스트명                          |
| MAIL         | 도착한 메일이 저장되는 경로                                  | LOGNAME      | 로그인 이름                                |
| TMOUT        | 사용자가 로그인 한 후 일정 시간 동안 작업을 하지 않을 경우에 로그아웃시키는 시간으로 단위는 초 |              |                                            |
| UID          | 사용자의 UID                                                 | OSTYPE       | 운영체제 타입                              |

">" : 덮어씌움

">>" : 추가함

PID

- 프로세스 각각을 구별할 수 있는 유일한 데이터

PPID

- 프로세스를 만든 부모 프로세스의 PID를 나타내는 값
- 쉘 프롬프트에서 명령어를 입력하여 프로그램을 실행했다면 쉘이 부모 프로세스가 되어 쉘의 PID가 프로세스의 PPID로 할당된다.

시그널 번호

1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL
 5) SIGTRAP      6) SIGABRT      7) SIGBUS       8) SIGFPE
 9) SIGKILL     10) SIGUSR1     11) SIGSEGV     12) SIGUSR2
13) SIGPIPE     14) SIGALRM     15) SIGTERM     16) SIGSTKFLT
17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU
25) SIGXFSZ     26) SIGVTALRM   27) SIGPROF     28) SIGWINCH
29) SIGIO       30) SIGPWR      31) SIGSYS      34) SIGRTMIN
35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3  38) SIGRTMIN+4
39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12
47) SIGRTMIN+13 48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14
51) SIGRTMAX-13 52) SIGRTMAX-12 53) SIGRTMAX-11 54) SIGRTMAX-10
55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7  58) SIGRTMAX-6
59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX

SIGHUP

- 프로세스를 재시작할 때 사용

SIGINT

- 프로세스를 인터럽트, 키(DELETE, Ctrl + C)를 눌렀을때 처럼 종료

SIGKILL

- 프로세스를 강제 종료할 때 사용

SIGTERM

- 프로세스를 가능한 정상 종료시킬때 사용

cron

- 주기적인 예약작업을 설정하는 명령

crontab [-u user] file

- -e : edit user's crontab (예약 작업 수정)
- -l : list user's crontab (예약 작업 리스트)
- -r : delete user's crontab (예약 작업 remove~)
- -i : prompt before deleting user's crontab

vi

- 유닉스 환경에서 가장 많이 쓰는 문서 편집기이며, 다른 편집기들과 다르게 모드(mode)형 편집기
- 옵션
  - -r : 파일이 비정상적으로 종료된 후 파일 되살리기
  - -R : 읽기전용으로 불러오기

**1. vi 실행하기**(https://hyeonstorage.tistory.com/274)

| **명령어**     | **동작**                                             |
| -------------- | ---------------------------------------------------- |
| vi file        | file을 연다                                          |
| vi file1 file2 | file1 과 file2 를 차례로 연다                        |
| view file      | file을 읽기 모드로 연다                              |
| vi -R file     | file을 읽기 모드로 연다                              |
| vi + file      | file을 열때 커서가 file 본문의 마지막 행에 위치한다. |
| vi +n file     | file을 열어 n행에 위치한다.                          |
| vi -r file     | 손상된 파일 회복                                     |

**2. 입력모드 전환 명령어**

| **명령어** | **동작**                          |
| ---------- | --------------------------------- |
| i          | 커서 있는데서 입력모드 전환       |
| I          | 커서 왼쪽, 행의 처음에 몬자 삽입  |
| a          | 커서 있는 줄 끝에서 입력모드 전환 |
| A          | 커서 오른쪽, 행의 끝에 문자 삽입  |
| o          | 커서 있는 줄 아래에 빈 줄 삽입    |
| O          | 커서 있는 줄 위에 빈 줄을 삽입    |
| R          | 덮어쓰기 모드로 전환              |

**3. 커서의 이동**

| **명령어** | **동작**                                  |
| ---------- | ----------------------------------------- |
| ^, 0       | 줄의 처음으로 이동                        |
| $          | 줄의 끝으로 이동                          |
| H          | 화면 맨 위로 이동                         |
| M          | 화면의 중간으로 이동                      |
| L          | 화면 맨 아래로 이동                       |
| w          | 다음 단어 끝으로 커서 이동                |
| e          | 다음 단어 앞으로 커서 이동                |
| b          | 이전 단어로 이동                          |
| shift + ↑  | 한 페이지 앞으로 이동                     |
| shift + ↓  | 한 페이지 뒤로 이동                       |
| 3l , 3G    | 현재 커서 위치한 행에서 3번째 행으로 이동 |
| Ctrl + i   | 한 화면 위로 이동                         |
| Ctrl + b   | 한 화면 아래로 이동                       |
| Ctrl + d   | 반 화면 위로 이동                         |
| Ctrl + u   | 반 화면 아래로 이동                       |
| Ctrl + e   | 한 줄씩 위로 이동                         |
| Ctrl + y   | 한 줄씩 아래로 이동                       |

**4. 삭제**

| **명령어** | **동작**                               |
| ---------- | -------------------------------------- |
| x          | 한 문자 삭제                           |
| 5x         | 커서가 있는 위치부터 5개의 문자를 삭제 |
| d + ↑      | 커서있는 줄, 윗줄 2줄 삭제             |
| d + ↓      | 커서잇는 줄, 아래줄 2줄 삭제           |
| dw         | 한 단어 삭제                           |
| dd         | 한 줄 삭제                             |
| 5dd        | 커서가 있는 라인부터 5개의 라인 삭제   |
| db         | 커서의 위치에서 거꾸로 한 단어 삭제    |
| D          | 한줄 내에서 커서있는 뒤 모두 삭제      |
| u          | 바로 전에 수행한 명령을 취소           |
| :5,10ㅇ    | 5~10번째 행 삭제                       |

**5. 복사와 붙여넣기**

| **명령어** | **동작**                                 |
| ---------- | ---------------------------------------- |
| yy         | 현재 줄을 버퍼로 복사                    |
| p          | 버퍼에 있는 내용을 커서 뒤에 삽입        |
| P          | 버퍼에 있는 내용을 커서 앞에 삽입        |
| 3y         | 현재 줄에서부터 아래로 3줄 복사          |
| :5, 10y    | 5~10줄을 버퍼로 복사                     |
| :30pu      | 30행에 버퍼 내용을 삽입                  |
| d          | 현재 커서가 위치해 있는 단어 복사        |
| 3yy        | 현재 행을 기준으로 3번째 행까지 n행 복사 |

**6. 문자열 찾기**

| **명령어** | **동작**                   |
| ---------- | -------------------------- |
| /name      | name 문자열 찾기           |
| n          | 다음 name으로 이동         |
| N          | n과 같으며 역방향으로 이동 |

**7. 문자열 대체**

| **명령어**     | **동작**                                                   |
| -------------- | ---------------------------------------------------------- |
| :s/str/rep     | 현재 행의 str을 rep로 대체                                 |
| :l,.s/str/rep/ | 1부터 현재 행의 str을 rep로 대체                           |
| :%s/str/rep/g  | 파일 전체 str을 rep로 전부 대체                            |
| :.$/aaa/bbb    | 커서의 위치로부터 파일의 끝까지 있는 모든 aaa를 bbb로 대체 |

**8. 파일 저장 및 불러오기**

| **명령어**      | **동작**                                             |
| --------------- | ---------------------------------------------------- |
| :w              | 지정된 파일에 저장                                   |
| :wq, :x, ZZ     | 지정된 파일에 저장하고 vi를 종료                     |
| :w php.ini      | php.ini 파일에 저장                                  |
| :q              | 저장하지 않고 종료                                   |
| :q!             | 저장하지 않고 강제 종료                              |
| :wq php.ini     | php.ini에 저장하고 vi를 종료                         |
| :r php.ini      | php.ini의 내용을 현재 커서가 있는데로 불러온다.      |
| :e php.ini      | 현재의 화면을 지우고 새로운 파일 php.ini를 불러온다. |
| :5,10 w php.ini | 5~10 줄까지의 내용을 php.ini에 저장                  |

**9. 기타**

| **명령어** | **동작**                        |
| ---------- | ------------------------------- |
| :set nu    | 행 번호 보여주기                |
| :set nonu  | 행 번호 보여주기 취소           |
| .          | 바로 전에 실행한 명령어 재 실행 |
| Ctrl + l   | 불필요한 화면 정리후 다시 표시  |

gedit

- 그놈 데스크톱 환경용으로 개발된 자유 소프트웨어인 텍스트 편집기
- 윈도우, OSX에서도 사용 가능
- UTF-8과 호환 가능하며 프로그램 코드, 마크업 언어와 같은 구조화된 텍스트 문서를 편집하는 용도에 중점
- X 윈도 시스템에 맞춰 개발했으며, GTK+와  그놈 라이브러리를 이용하여 개발
- 그놈 파일 관리자인 노틸러스와의 사이에서 드래그 앤 드롭이 가능

CUPS

- 애플에서 개발한 모듈 방식을 프린팅 시스템
- 인쇄작업과 대기열을 취급하는 기반으로 HTTP 기반의 IPP를 이용
- System V 형식과 BSD 형식의 커멘드라인 인터페이스도 지원
  - System V 계열 명령어 : lp, lpstat, cancel
  - BSD 계열 명령어 : lpr(작업요청), lpq(큐에 있는 작업 목록), lprm, lpc(컨트롤)
- SMB 프로토콜도 부분적으로 지원
- 어도비의 PRD 형식의 텍스트 파일을 이용하여 설정이 가능
- lpadmin 이라는 명령을 이용하여 웹상에서도 제어 가능

LPRng

- 버클리 프린팅 시스템
- 라인 프린터 데몬 프로토콜을 사용하여 프린터 스풀링 및 네트워크 프린터 서버를 지원한다.

SANE

- 평판 스캐너, 핸드 스캐너 등 이미지 관련 하드웨어를 사용할 수 있도록 해주는 API
- GPL 라이선스로 리눅스 및 유닉스와 windows도 지원
- 스캐너 관련 드라이버가 있는 sane-backends와 사용자 관련 명령이 있는 sane-frontends 등 2개의 패키지로 배포

회선 교환 방식

- 송수신 호스트가 데이터를 전송하기 전에 연결 경로를 미리 설정하는 방식
- 고정된 대역폭을 할당 받아 전송
- 안정적인 데이터 전송률을 지원

패킷 교환 방식

- 회선 교환 방식에 비해 더 많은 지연이 발생
- 패킷마다 오버헤드 비트가 존재
- 이론상 호스트의 무제한 수용이 가능

rsync

- 파일과 디렉토리를 복사하고 동기화 하기위해서 사용

stty

- 터미널 통신 포트나 가상 터미널 포트에 대한 특성 세팅
- 셸 환경에서 터미널 설정을 변경하기 위한 명령어

/etc/profile.d

-  몇몇 응용프로그램들이 시작할때 필요한 스크립트가 위치하는 디렉도리로 보통 /etc/profile에서 호출된다. 일반 사용자의 alias 설정 등과 관련된 스크립트가 존재한다.

/etc/sysconfig/etwork

- 게이트웨이 주소 설정

/etc/hosts

- IP와 호스트 이름 또는 도메인 이름을 매핑

/etc/hosts.conf

- 도메인 요청시 검색 순서

/etc/resolv.conf

- DNS서버 주소 설정

/etc/profile

- 환경 변수와 bash가 수행될 때 실행되는 프로그램을 제어하는 전역적인 시스템 설정과 관련된 파일

/etc/bashrc

- alias와 bash가 수행될 때 실행되는 함수를 제어하는 전역적인 시스템 설정과 관련된 파일

$HOME/.bashrc

- 배쉬셸의 환경파일
- 개인 사용자가 정의한 alias와 함수들이 있는 파일
- 개인 사용자의 환경변수 설정도 가능

~/.bash_profile

- 환경변수와 bash가 수행될 때 실행프로그램을 제어하는 지역적인 시스템 설정과 관련된 파일
- 이들 환경변수들은 오직 그 사용자에게만 한정되며 그 이외의 다른 사람에게는 영향을 미치지 않는다.
- 전역적인 실행 파일인 /etc/profile이 실행된 다음 바로 수행된다.

~/.bash_logout

- 사용자가 로그아웃하기 직전에 실행 프로그램에 관한 bash의 지역시스템 설정과 관련된 파일
- 프로그램은 오직 그 프로그램을 실행하는 사용자에게만 영향

/etc/passwd

- 사용자별 로그인 셸의 정보

unset

- 쉘의 변수를 효과적으로 NULL로 세트를 해서 그 변수를 지우는 효과가 있다.

tar

- -f : 테이프 대신 파일을 묶는다.
- -c : 지정한 파일을 tar로 묶는다.
- -x : tar를 압축 해제한다.
- -r : 묶인 tar에 새 파일을 추가한다.
- -t : 안에 들어 있는 파일을 목록으로 표시한다.
- -v : 압축 및 해체 과정을 상세한 메시지로 출력한다.
- -z : 묶은 tar를 gzip으로 압축한다.
- -j : 묶은 tar를 bzip2로 압축한다.
- -J : 묶은 tar를 xz로 압축한다.
- -C : 디렉터리를 변경할 때 사용

gzip

- 전통적으로 유닉스에서 사용해왔던 압축프로그램
- LZ77 알고리즘을 이용
- 허브만 부조화 를 이용하며 현재에도 업데이트되고 있으며 자주쓰인다.

compress

- 유닉스에서 사용하는 프로그램
- LZW 압축 알고리즘을 이용

bzip2

- 블록정렬 알고리즘과 허브만 부조화 를사용하여 압출률이 좋다

xz

- LZMA2 알고리즘을 사용
- 리눅스 계열 운영체제에서 자주 사용

lspci

- 시스템의 모든 PCI BUS와 장치에 대한 목록을 각개 하드웨어 설정 정보를 확인할 수 있는 명령어
- 트리형태로 옵션을 주어 장치 번호를 트리형태로 보여주고 내용내역까지 출력

SANE

- 평판 스캐너, 핸드 스캐너, 비디오 캠 등 이미지 관련 하드웨어를 사용할 수 있도록 해주는 API

UTP 케이블

- 주황 + 흰-주 : 송신(TX)
- 녹생 + 흰-녹 : 수신(RX)
- 파랑 + 흰-파 : 전화선(예비)
- 갈색 + 흰-갈 : 전원선
- 실제  랜통신에서는 주황과 녹색선만 사용

NFS

- NIS 와 더불어 RPC 프로토콜 기반으로 작동하므로, 해당 서비스를 해주는 portmap 데몬의 실행이 필수이다.
- NetWork File System의 약자로 네트워크 상의 서로 다은 기계가 일관성있게 디렉토리와 파일을 생성, 사용 가능하돌고 하는 기술
- 윈도우와 리눅스, 유닉스에 모두 존재하는 시스템

CIFS

- common internet file system

ntfs

- new technology file system

udf

- unviersal disk format

IRC

- 실시간 채팅 프로토콜로 여러 사용자가 모여 대화를 할 수 있는 서비스
- 사용자 간의 대화와 파일 전송 기능도 제공

netstat

- 물리적 네트워크 확인 가능, 네트워크 연결 상태 출력
- 라우팅 테이블 정보, 네트워크 인터페이스 상태, 매스커레이드 연결 상태, 멀티캐스트 멤버 정보
- -a : 모든 소켓 보기
- -n : 도메인 주소를 읽어들이지 않고 숫자로 출력
- -p : PID와 사용중인 프로그램명이 표시됨
- -u  : UDP 프로토콜 보기

rmp

- -q : 패키지 정보를 검색
- -qa : 전체 패키지 목록을 출력
- -qi : 자세한 정보를 출력
- -ql : 패키지 내의 파일을 출력
- -qs : 패키지 안에 들어있는 설정 파일을 보여준다.
- -qap : 옵션 p는 패키지명으로 상세 정보를 출력한다.

프로세스

- 특정 프로그램이 메모리에 상주해서 실행되고 있으면 이는 프로세스라고 한다.
- 리눅스에서 프로세스는 실행시 PID가 할당되오 관리된다.
- 리눅스 부팅시 최초의 프로세스의 PID는 1번리고, 쵀대 65536까지 할당된다.
- 셸에서 명령을 실행하고 해당 프로세스가 종료될 때까지 기다리는 프로세스를 포어그라운드 프로세스라 한다.

데몬

- 지속적인 서비스 요청을 처리하기 위해 계속 실행되는 프로세스
- 이를 실행하는 방법에는 standalone 방식과 inetd 방식이 있다.
- 보통 이름 뒤에 d를 붙인다
- 주기적이기 지속적인 서비스 요창을 처리하기 위해 백그라운드 상태에서 계속 실행되는 프로세스
- 보통 서버 역할을 하는 프로그램들이 이에 해당
- service 명령어로 실행, 중지, 재시작 등을 할 수 있다.

intend

- 지속적인 서비스 요청을 처리하기 위해 관련 데몬이 메모리에 계속 상주하면서 처리하는 것이 아니라, 특정 데몬이 여러 데몬을 관리하면서 서비스 요청이 들어왔을때 관련 프로세스를 메모리에 상주시키는 방식

프로세스 우선순위

- 프로세스 우선순위를 변경하는 명령으로는 nice, renice가 있다
- 일반 사용자는 NI값을 증가만 가능
- root 사용자는 NI값을 증감 가능
- nice 명령어 사용시 값을 지정하지 않으면 기본적을 NI 값이 10으로 지정
- nice 명령은 프로세스 명으로 우선순위를 조정하고, renice 명령은 주로 PID로 조정
- 기존의 NI값에 상관없이 지정한 NI 값으로 바로 적용하려면 renice 명령어를 사용해야한다.

xhost

- X서버에서 접근 가능한 IP주소 및 호스트명을 확인할 때 사용
- '+' 옵션으로 클라이언트를 X서버에 접근 가능하도록 설정할 수 있다.

xauth

- X서버에서 X클라이언트 허가를 위해 생성한 키 값을 확인할 때 사용

RPM

- 설치 및 갱신, 제거, 질의, 검증 모드 등이 있다.
- 시스템에 설치된 모든 패키지 정보를 출력할 때 사용하는 명령은 rpm -qa
- 질의 모드에서 해당 패키지가 설치 또는 동작시 필요한 패키지 목혹을 보여주는 옵션은 -R
- 검증모드에서 사용하는 기본 옵션은 -V
- -F : 현재 시스템에 설치된 패키지만 찾아서 업데이트

mput

- 파일을 업로드할 때

mget

- 파일을 다운로드할 때

chsh

- shell 변경 명령어
- 옵션
  - -s : 지정하는 셸을 앞으로 사용할 로그인 셀로 변경
  - -ㅣ : /etc/shells 파일안에 지정된 셀을 나열

cmake

- 기존 MAKE를 수행하지 않고 운영체제에 맞는 make만을 수행
- 프로그램 설치 순서
  - make —> make install
- KDE와 MYSQL

소스파일 설치 단계

	1. 환경설정(configure) : 프로그램 설치 과정에서 필요로하는 환경파일 makefile 생성
 	2. 컴파일(make) : makefile을 기반으로 소스 파일을 컴파일
 	3. 파일설치(make install) : 컴파일된 실행 파일을 지정된 디렉터리에 설치

ALSA

- 사운드 카드용 자치 드라이버를 제공하기 위한 리눅스 커널의 요소
- 1998년 Jaroslav Kysela에 의해 시작됨
- GPL 및 LGPL 라이선스 기반으로 배포

네트워크 프린트 설정 환경

- AppSocket/HP jecDirect
- LPD/LPR 호스트 또는 프린터
- Windows Printer vis SAMBA
- 인터넷 프린터 프로토콜(http)
- 인터넷 프린터 프로토콜(ipp)

X-Windows 환경에서 프린터 설정

- 주메뉴 —> 시스템 설정 —> 인쇄 선택
- system —> config —> printer

GNOME

- 응용 프로그램 : nautilus, totem, evolution
- 윈도우 매니저
  - GNOME 2 : mutter
  - GNOME 3 : metacity

KDE

- 응용 프로그램 : konqueror
- 윈도우 매니저
  - KWin
  - KWM