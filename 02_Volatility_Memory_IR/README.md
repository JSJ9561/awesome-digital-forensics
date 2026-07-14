# 📂 02. 침해사고 대응기법 및 메모리 분석

* 인프런 강의 섹션 3 (Volatility 도구 활용 및 실습)
* Cridex, GrrCon 2015, OlympicDestroyer 기출 및 실습 풀이 기록
* 메모리 덤프 분석 및 악성코드 흔적 추적 과정 요약

## 해당 실습을 위해 사전에 문제 파일을 다운로드 받아야 한다.

| 항목 | 공식 경로 | 상태 | 확보 방법 |
| :--- | :--- | :--- | :--- |
| **Malware-Cridex** | [GitHub](https://github.com/volatilityfoundation/volatility/wiki) | 다운로드 불가 | 강의 첨부파일 활용 |
| **GrrCON** | [ctf-d.com](http://ctf-d.com) | 접근 불가 | 강의 배포파일 활용 |

> ※ 본 실습 파일은 저작권 문제로 인해 직접 게시하지 않으니, 각 공식 경로 혹은 수강 중인 학습 플랫폼을 통해 확보하시기 바랍니다.

## Volatility Cridex 풀이

> cridex를 터미널에서 이용하려면 디렉터리를 찾아가야 합니다. 기본적인 터미널 명령어를 이용하는 과정이므로 별도로 설명하지는 않습니다. 빠른 이동을 원하면 cridex파일이 있는 폴더의 빈공간에 우클릭 후 [터미널에서 열기]를 클릭하면 빠르게 cridex 디렉터리를 터미널로 접근할 수 있습니다.

> 만약 이 과정이 귀찮거나 어려우면 바탕화면이나 본인이 가장 빠르게 접근가능한 경로에 cridex 파일을 복사하거나 이동해서 실습하면 됩니다.

<img width="706" height="685" alt="KakaoTalk_Snapshot_20260713_234223" src="https://github.com/user-attachments/assets/2f6148b8-2871-4f12-a104-85e3abe606ca" />

### Volatility 명령어

> 'volatility_2.6_win64_standalone.exe'가 너무 길면 'Volatility'처럼 이름을 축소하여 실습하는 것도 좋습니다.

#### 옵션: -f

#### 1. imageinfo: 분석할 메모리 이미지의 프로파일(OS 정보) 확인하는 명령어
> 메모리 덤프 파일의 정보를 분석하여 적절한 프로파일을 식별합니다. 분석의 첫 단계로 반드시 수행해야 합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem imageinfo

<img width="844" height="461" alt="KakaoTalk_Snapshot_20260714_183506" src="https://github.com/user-attachments/assets/df2253cb-a9e4-4bb9-a0db-7a6265eb0284" />

#### 2. pslist: EPROCESS 구조체를 기반으로 프로세스 리스트 출력하는 명령어
> 액티브(Active) 프로세스 리스트를 따라가며 생성된 순서대로 프로세스들을 보여줍니다. 기본적으로 가장 먼저 확인하는 명령어입니다.

> imageinfo에서 찾은 profile(s)에서 하나를 골라 복사하고 --profile=[복사한 profile] 옵션을 추가합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=WinXPSP2x86 pslist

<img width="982" height="420" alt="KakaoTalk_Snapshot_20260714_184057" src="https://github.com/user-attachments/assets/3a292bfb-f7b5-465c-ae3f-6c79573000f9" />

> 리스트가 너무 길어서 가독성이 떨어지면 .txt나 .log 등의 형식으로 리다이렉션하여 새로 만들고 'Notepad++'로 열면 됩니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=WinXPSP2x86 pslist > pslist.log

<img width="577" height="201" alt="KakaoTalk_Snapshot_20260714_184444" src="https://github.com/user-attachments/assets/82a790a5-ad22-4b1b-aa31-9438573dbfe2" />

<img width="728" height="500" alt="KakaoTalk_Snapshot_20260714_184653" src="https://github.com/user-attachments/assets/e4202b73-700a-4670-8c9c-1d7d8441946f" />

#### 3. psscan: 숨은 프로세스들을 볼 수 있는 명령어
> 메모리 구조를 직접 스캔하여 프로세스 객체를 찾으므로, OS 리스트에서 은닉된 프로세스까지 탐지 가능합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=WinXPSP2x86 psscan > psscan.log

#### 4. pstree: 프로세스 계층 구조 확인하는 명령어
> 부모-자식 관계(PPID)를 통해 악성코드의 감염 경로를 추적할 때 유용합니다.

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=WinXPSP2x86 pstree > pstree.log

#### 5. psxview: 프로세스 은닉 탐지 명령어
> 여러 기법을 교차 분석하여 정상 리스트에서 제외된 비정상 프로세스를 식별합니다.(출력 결과의 False 값을 유심히 확인하세요.)

\> volatility_2.6_win64_standalone.exe -f .\cridex.vmem --profile=WinXPSP2x86 psxview > psxview.log


