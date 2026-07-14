# Volatility 명령어 분석 가이드

## 분석가 가이드 

> [!WARNING] 분석 시 주의사항: 추출된 파일은 실제 동작하는 악성코드일 가능성이 매우 높습니다.
  1. 반드시 네트워크가 차단된 격리된 가상머신 환경에서만 분석하십시오.
  2. 원본 데이터의 무결성을 위해 원본 파일은 읽기 전용으로 보관하고, 분석은 복사본을 활용하십시오.

**각 명령어의 목적과 출력 결과를 명확히 이해하십시오. 특히, 나열된 프로세스 목록 중 생소한 항목은 반드시 개별적인 검색과 분석을 통해 프로세스의 정상/비정상 여부를 스스로 검증하는 습관을 갖추는 것이 실무 역량 향상의 핵심입니다.**

## Volatility 명령어

- 옵션
  - -f [메모리 파일 경로]: 메모리 덤프 파일의 경로를 지정하는 필수 옵션

> 'volatility_2.6_win64_standalone.exe'가 너무 길면 'Volatility'처럼 이름을 축소하여 실습하는 것도 좋습니다.

### 1. imageinfo: 분석할 메모리 이미지의 프로파일(OS 정보) 확인 명령어
> 메모리 덤프 파일의 정보를 분석하여 적절한 프로파일을 식별합니다. 분석의 첫 단계로 반드시 수행해야 합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] imageinfo

<img width="844" height="461" alt="KakaoTalk_Snapshot_20260714_183506" src="https://github.com/user-attachments/assets/df2253cb-a9e4-4bb9-a0db-7a6265eb0284" />

### 2. pslist: EPROCESS 구조체를 기반으로 프로세스 리스트 출력 명령어
> 액티브(Active) 프로세스 리스트를 따라가며 생성된 순서대로 프로세스들을 보여줍니다. 기본적으로 가장 먼저 확인하는 명령어입니다.

> imageinfo에서 찾은 profile(s)에서 하나를 골라 복사하고 --profile=[profile] 옵션을 추가합니다.

> EPROCESS 구조체: 운영체제가 프로세스를 관리하기 위해 사용하는 '신분증 양식'입니다. PID, 실행 시간, 부모 프로세스 정보 등이 담겨 있습니다. 악성코드는 이 신분증의 명단 연결 고리를 끊어(Unlinking) 시스템에서 자신을 숨기려 하지만, 메모리 구조를 직접 스캔(psscan)하면 숨겨진 신분증까지 찾아낼 수 있습니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] pslist

<img width="982" height="420" alt="KakaoTalk_Snapshot_20260714_184057" src="https://github.com/user-attachments/assets/3a292bfb-f7b5-465c-ae3f-6c79573000f9" />

> 명령어를 실행하고 결과출력이 너무 많으면 가독성이 떨어집니다. '.log' 형식으로 리다이렉션하여 새로 만들고 'Notepad++'로 열어줍니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] pslist > pslist.log

<img width="577" height="201" alt="KakaoTalk_Snapshot_20260714_184444" src="https://github.com/user-attachments/assets/82a790a5-ad22-4b1b-aa31-9438573dbfe2" />

<img width="728" height="500" alt="KakaoTalk_Snapshot_20260714_184653" src="https://github.com/user-attachments/assets/e4202b73-700a-4670-8c9c-1d7d8441946f" />

### 3. psscan: 숨은 프로세스 확인 명령어
> 메모리 구조를 직접 스캔하여 프로세스 객체(EPROCESS)를 찾습니다. 악성코드가 시스템 리스트에서 자신을 제거(Unlinking)하여 숨더라도, 메모리에 남아 있는 신분증 패턴을 직접 찾아내기 때문에 탐지가 가능합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] psscan > psscan.log

### 4. pstree: 프로세스 계층 구조 확인 명령어
> 부모-자식 관계(PPID)를 통해 악성코드의 감염 경로를 추적할 때 유용합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] pstree > pstree.log

### 5. psxview: 프로세스 은닉 탐지 명령어
> 여러 기법을 교차 분석하여 정상 리스트에서 제외된 비정상 프로세스를 식별합니다.(출력 결과의 False 값을 유심히 확인하세요.)

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] psxview > psxview.log

### 6. cmdscan: 터미널을 명령어 기록 탐색 명령어
> 메모리 내의 _COMMAND_HISTORY구조체를 스캔하여, 사용자가 'cmd.exe' 터미널에서 입력했던 명령어 기록을 복구합니다. 악성코드가 실행한 쉘 명령어나 파워쉘 스크립트를 찾아낼 때 매우 유용합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] cmdscan > cmdscan.log

### 7. consoles: 윈도우 콘솔 히스토리 복구 명령어
> 'cmdscan'보다 더 상세하게 콘솔 창에 출력되었던 텍스트와 명령어 히스토리를 가져옵니다. 악성코드의 동작으로 인해 터미널에 어떤 로그가 남았는지 확인할 때 사용합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] consoles > consoles.log

### 8. cmdline: 프로세스 실행 인자(Argument) 확인 명령어
> 프로세스가 실행될 때 함께 입력된 인자값들을 확인합니다. 예를 들어, 'powershell.exe'가 실행될 때 뒤에 붙은 '-EncodedCommand' 같은 악성 스크립트 본문을 발견할 수 있습니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] cmdline > cmdline.log

### 9. filescan: 메모리 상의 파일 객체 스캔 명령어
> 시스템 메모리에 존재하는 모든 파일 객체를 스캔합니다. 악성코드가 생성한 파일의 이름과 메모리 상의 위치(Offset)를 파악할 때 사용합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] filescan > filescan.log

### 10. dumpfiles: 파일 추출(증거 확보) 명령어
> 'filescan'으로 찾은 오프셋(offset) 주소를 기반으로 실제 파일을 추출합니다.

- 옵션: -Q, -D, -n
  - -Q [offset]: 특정 주소의 파일을 지정
  - -D [저장할 디렉터리]: 파일을 저장할 경로 지정
  - -n: 원래 파일 이름을 유지하여 저장하는 옵션

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] dumpfiles -Q [offset] -D [저장할 디렉터리] -n

### 11. connections: 연결된 TCP/IP 네트워크 정보 추출 명령어
> 프로세스가 네트워크를 통해 외부와 통신한 이력을 확인합니다. 악성코드가 C&C 서버와 통신하거나 데이터를 외부로 유출할 때 사용한 연결 정보를 추적할 수 있습니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] connections > connections.log

### 12. netscan: 메모리 상의 네트워크 연결 정보 스캔 명령어 
> connections 명령어보다 더 정교하게, 현재 및 과거의 TCP/UDP 네트워크 연결 상태를 스캔합니다. 특히 종료된 연결이나 리스닝(Listening) 중인 소켓까지 포괄적으로 찾아내므로, 악성코드의 통신 흔적을 분석할 때 반드시 병행해야 합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] netscan > netscan.log

### 13. sockets: 활성화된 네트워크 소켓 탐지 명령어
> 시스템에서 열려 있는 모든 네트워크 소켓(Socket) 정보를 나열합니다. 악성코드가 특정 포트를 열어 백도어로 활용하거나 외부와 통신하기 위해 생성한 소켓을 확인할 때 유용합니다.

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] sockets > sockets.log

### 14. memdump: 프로세스 메모리 전체 덤프 명령어
> 특정 프로세스가 사용 중인 전체 메모리 영역을 파일로 저장합니다. 프로세스가 메모리 상에서 어떻게 동작하는지, 어떤 데이터를 처리 중인지 상세히 분석할 때 사용합니다.

- 옵션: -p, -D
  - -p [PID]: 추출할 프로세스의 PID 지정

\> volatility_2.6_win64_standalone.exe -f [메모리 파일 경로] --profile=[profile] memdump -p [PID] -D [저장할 디렉터리]

### 15. procdump: 프로세스 실행 파일 추출 명령어
> 특정 프로세스의 실행 파일(exe)을 추출합니다. 이 도구는 실제 실행 파일 형태를 확보하기 때문에, 악성코드의 기능을 분석(정적 분석)하는 데 핵심적인 명령어입니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] procdump -p [PID] -D [저장할 디렉터리]
