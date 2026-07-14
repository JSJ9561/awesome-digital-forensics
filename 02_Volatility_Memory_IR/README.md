# 📂 02. 침해사고 대응기법 및 메모리 분석

* 인프런 강의 섹션 3 (Volatility 도구 활용 및 실습)
* Cridex, GrrCon 2015, OlympicDestroyer 기출 및 실습 풀이 기록
* 메모리 덤프 분석 및 악성코드 흔적 추적 과정 요약

## 해당 실습을 위해 사전에 문제 파일을 다운로드 받아야 합니다.

| 항목 | 공식 경로 | 상태 | 확보 방법 |
| :--- | :--- | :--- | :--- |
| **Malware-Cridex** | [GitHub](https://github.com/volatilityfoundation/volatility/wiki) | 다운로드 불가 | 강의 첨부파일 활용 |
| **GrrCON** | [ctf-d.com](http://ctf-d.com) | 접근 불가 | 강의 배포파일 활용 |

> ※ 본 실습 파일은 저작권 문제로 인해 직접 게시하지 않으니, 각 공식 경로 혹은 수강 중인 학습 플랫폼을 통해 확보하시기 바랍니다.

## Volatility 명령어

> cridex를 터미널에서 이용하려면 디렉터리를 찾아가야 합니다. 기본적인 터미널 명령어를 이용하는 과정이므로 별도로 설명하지는 않습니다. 빠른 이동을 원하면 cridex파일이 있는 폴더의 빈공간에 우클릭 후 [터미널에서 열기]를 클릭하면 빠르게 cridex 디렉터리를 터미널로 접근할 수 있습니다.

> 만약 이 과정이 귀찮거나 어려우면 바탕화면이나 본인이 가장 빠르게 접근가능한 경로에 cridex 파일을 복사하거나 이동해서 실습하면 됩니다.

<img width="706" height="685" alt="KakaoTalk_Snapshot_20260713_234223" src="https://github.com/user-attachments/assets/2f6148b8-2871-4f12-a104-85e3abe606ca" />

> 'volatility_2.6_win64_standalone.exe'가 너무 길면 'Volatility'처럼 이름을 축소하여 실습하는 것도 좋습니다.

### 옵션: -f

### 1. imageinfo: 분석할 메모리 이미지의 프로파일(OS 정보) 확인 명령어
> 메모리 덤프 파일의 정보를 분석하여 적절한 프로파일을 식별합니다. 분석의 첫 단계로 반드시 수행해야 합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem imageinfo

<img width="844" height="461" alt="KakaoTalk_Snapshot_20260714_183506" src="https://github.com/user-attachments/assets/df2253cb-a9e4-4bb9-a0db-7a6265eb0284" />

### 2. pslist: EPROCESS 구조체를 기반으로 프로세스 리스트 출력 명령어
> 액티브(Active) 프로세스 리스트를 따라가며 생성된 순서대로 프로세스들을 보여줍니다. 기본적으로 가장 먼저 확인하는 명령어입니다.

> imageinfo에서 찾은 profile(s)에서 하나를 골라 복사하고 --profile=[복사한 profile] 옵션을 추가합니다.

> EPROCESS 구조체: 운영체제가 프로세스를 관리하기 위해 사용하는 '신분증 양식'입니다. PID, 실행 시간, 부모 프로세스 정보 등이 담겨 있습니다. 악성코드는 이 신분증의 명단 연결 고리를 끊어(Unlinking) 시스템에서 자신을 숨기려 하지만, 메모리 구조를 직접 스캔(psscan)하면 숨겨진 신분증까지 찾아낼 수 있습니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] pslist

<img width="982" height="420" alt="KakaoTalk_Snapshot_20260714_184057" src="https://github.com/user-attachments/assets/3a292bfb-f7b5-465c-ae3f-6c79573000f9" />

> 명령어를 실행하고 결과출력이 너무 많으면 가독성이 떨어집니다. '.log' 형식으로 리다이렉션하여 새로 만들고 'Notepad++'로 열어줍니.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=WinXPSP2x86 pslist > pslist.log

<img width="577" height="201" alt="KakaoTalk_Snapshot_20260714_184444" src="https://github.com/user-attachments/assets/82a790a5-ad22-4b1b-aa31-9438573dbfe2" />

<img width="728" height="500" alt="KakaoTalk_Snapshot_20260714_184653" src="https://github.com/user-attachments/assets/e4202b73-700a-4670-8c9c-1d7d8441946f" />

### 3. psscan: 숨은 프로세스 확인 명령어
> 메모리 구조를 직접 스캔하여 프로세스 객체(EPROCESS)를 찾습니다. 악성코드가 시스템 리스트에서 자신을 제거(Unlinking)하여 숨더라도, 메모리에 남아 있는 신분증 패턴을 직접 찾아내기 때문에 탐지가 가능합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] psscan > psscan.log

### 4. pstree: 프로세스 계층 구조 확인 명령어
> 부모-자식 관계(PPID)를 통해 악성코드의 감염 경로를 추적할 때 유용합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] pstree > pstree.log

### 5. psxview: 프로세스 은닉 탐지 명령어
> 여러 기법을 교차 분석하여 정상 리스트에서 제외된 비정상 프로세스를 식별합니다.(출력 결과의 False 값을 유심히 확인하세요.)

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] psxview > psxview.log

### 6. cmdscan: 터미널을 명령어 기록 탐색 명령어
> 메모리 내의 _COMMAND_HISTORY구조체를 스캔하여, 사용자가 'cmd.exe' 터미널에서 입력했던 명령어 기록을 복구합니다. 악성코드가 실행한 쉘 명령어나 파워쉘 스크립트를 찾아낼 때 매우 유용합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] cmdscan > cmdscan.log

### 7. consoles: 윈도우 콘솔 히스토리 복구 명령어
> 'cmdscan'보다 더 상세하게 콘솔 창에 출력되었던 텍스트와 명령어 히스토리를 가져옵니다. 악성코드의 동작으로 인해 터미널에 어떤 로그가 남았는지 확인할 때 사용합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] consoles > consoles.log

### 8. cmdline: 프로세스 실행 인자(Argument) 확인 명령어
> 프로세스가 실행될 때 함께 입력된 인자값들을 확인합니다. 예를 들어, 'powershell.exe'가 실행될 때 뒤에 붙은 '-EncodedCommand' 같은 악성 스크립트 본문을 발견할 수 있습니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] cmdline > cmdline.log

### 9. filescan: 메모리 상의 파일 객체 스캔 명령어
> 시스템 메모리에 존재하는 모든 파일 객체를 스캔합니다. 악성코드가 생성한 파일의 이름과 메모리 상의 위치(Offset)를 파악할 때 사용합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] filescan > filescan.log

### 10. dumpfiles: 파일 추출(증거 확보) 명령어
> 'filescan'으로 찾은 오프셋(offset) 주소를 기반으로 실제 파일을 추출합니다.

- 옵션: -Q, -D, -n
  - -Q [offset]: 특정 주소의 파일을 지정
  - -D [디렉터리]: 파일을 저장할 경로 지정
  - -n: 원래 파일 이름을 유지하여 저장하는 옵션

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] dumpfiles -Q [offset] -D [저장할 디렉터리] -n

> cridex 디렉터리 안에 files 디렉터리를 생성하고 추출했습니다.

### 11. connections: 연결된 TCP/IP 네트워크 정보 추출 명령어
> 프로세스가 네트워크를 통해 외부와 통신한 이력을 확인합니다. 악성코드가 C&C 서버와 통신하거나 데이터를 외부로 유출할 때 사용한 연결 정보를 추적할 수 있습니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] connections > connections.log

### 12. netscan: 메모리 상의 네트워크 연결 정보 스캔 명령어 
> connections 명령어보다 더 정교하게, 현재 및 과거의 TCP/UDP 네트워크 연결 상태를 스캔합니다. 특히 종료된 연결이나 리스닝(Listening) 중인 소켓까지 포괄적으로 찾아내므로, 악성코드의 통신 흔적을 분석할 때 반드시 병행해야 합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] netscan > netscan.log

### 13. sockets: 활성화된 네트워크 소켓 탐지 명령어
> 시스템에서 열려 있는 모든 네트워크 소켓(Socket) 정보를 나열합니다. 악성코드가 특정 포트를 열어 백도어로 활용하거나 외부와 통신하기 위해 생성한 소켓을 확인할 때 유용합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] sockets > sockets.log

### 14. memdump: 프로세스 메모리 전체 덤프 명령어
- 옵션: -p, -D
  - -p [PID]: 추출할 프로세스의 PID 지정

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] memdump -p [PID] -D [저장할 디렉터리]

> cridex 디렉터리 안에 dumps 디렉터리를 생성하고 저장했습니다.

### 15. procdump: 프로세스 실행 파일 추출 명령어
> 특정 프로세스의 실행 파일(exe)을 추출합니다. 이 도구는 실제 실행 파일 형태를 확보하기 때문에, 악성코드의 기능을 분석(정적 분석)하는 데 핵심적인 명령어입니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=[profile] procdump -p [PID] -D .\dumps\

> [!WARNING] 분석 시 주의사항: 추출된 파일은 실제 동작하는 악성코드일 가능성이 매우 높습니다.
  1. 반드시 네트워크가 차단된 격리된 가상머신 환경에서만 분석하십시오.
  2. 원본 데이터의 무결성을 위해 원본 파일은 읽기 전용으로 보관하고, 분석은 복사본을 활용하십시오.

## Volatility Cridex 풀이
