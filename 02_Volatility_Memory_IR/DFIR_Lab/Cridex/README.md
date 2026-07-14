## Volatility Cridex 풀이

> cridex를 터미널에서 이용하려면 디렉터리를 찾아가야 합니다. 기본적인 터미널 명령어를 이용하는 과정이므로 별도로 설명하지는 않습니다. 빠른 이동을 원하면 cridex파일이 있는 폴더의 빈공간에 우클릭 후 [터미널에서 열기]를 클릭하면 빠르게 cridex 디렉터리를 터미널로 접근할 수 있습니다.

> 만약 이 과정이 귀찮거나 어려우면 바탕화면이나 본인이 가장 빠르게 접근가능한 경로에 cridex 파일을 복사하거나 이동해서 실습하면 됩니다.

<img width="706" height="685" alt="KakaoTalk_Snapshot_20260713_234223" src="https://github.com/user-attachments/assets/2f6148b8-2871-4f12-a104-85e3abe606ca" />

### 1. imageinfo로 정보 확인

<img width="830" height="240" alt="KakaoTalk_Snapshot_20260714_225718" src="https://github.com/user-attachments/assets/c245b131-2ffc-4686-bddf-eab5b3692cc2" />

profile: WinXPSP2x86, WinXPSP3x86

### 2. pslist, psscan, psxview, pstree 로그 저장하기

<img width="1062" height="131" alt="KakaoTalk_Snapshot_20260714_235453" src="https://github.com/user-attachments/assets/a2b4c8ce-bb41-4b75-81b4-ab0540f62b86" />

#### 프로세스 정보 검색 결과
```
smss.exe: Windows의 세션 관리자 하위 시스템(Session Manager Subsystem)
csrss.exe: 윈도우 운영체제의 핵심 시스템 프로세스
services.exe: 시스템 부팅 시 실행되는 핵심 프로세스인 서비스 제어 관리자(SCM)
lsass.exe: 사용자의 로그인 검사, 비밀번호 변경, 엑세스 토큰 생성 등 윈도우 보안 정책을 관리하는 중요한 시스템 프로세스
svchost.exe: DLL(동적 연결 라이브러리)에서 실행되는 여러 Windows 시스템 서비스를 호스팅하고 그룹화하여 리소스 사용을 최적화하는 필수 백그라운드 프로세스
explorer.exe: 바탕화면, 시작 메뉴, 작업 표시줄 등 윈도우 그래픽 사용자 인터페이스(GUI) 전체를 담당하는 핵심 시스템 프로세스(윈도우 탐색기)
spoolsv.exe: Windows 운영체제의 인쇄 스풀러(Print Spooler) 프로세스
reader_sl.exe: Adobe Acrobat Reader의 Speed Launcher 프로세스
alg.exe: Windows의 응용 프로그램 계층 게이트웨이 서비스(Application Layer Gateway Service)
wuauclt.exe: 윈도우 업데이트 확인, 다운로드 및 설치를 관리하는 정상적인 마이크로소프트 시스템 프로세스
```

> psxview에서 확인한 결과 숨겨진 프로세스는 존재하지 않았다.

<img width="766" height="450" alt="KakaoTalk_Snapshot_20260714_230823" src="https://github.com/user-attachments/assets/d68d28bd-70c8-4eba-af03-b5be327fc58e" />

> pstree에서 확인한 결과, explorer.exe와 reader_sl.exe를 제외하고는 전부 System의 자식 프로세스이다.

<img width="702" height="404" alt="KakaoTalk_Snapshot_20260714_231121" src="https://github.com/user-attachments/assets/ea3ca6dc-dec5-43f3-9e61-d35fe9e9825d" />

### 3. cmdscan, consoles, cmdline 로그 저장하기

<img width="1071" height="103" alt="KakaoTalk_Snapshot_20260714_235719" src="https://github.com/user-attachments/assets/4b5810c7-dd2d-4d53-8072-20113b9f8e44" />

> 확인 결과 cmdscan과 consoles에서는 아무것도 나오지 않았다.

> cmdline에서도 직접적인 악성코드 명령어의 흔적은 나오지 않았다.

<img width="947" height="642" alt="KakaoTalk_Snapshot_20260714_231717" src="https://github.com/user-attachments/assets/c4dc2e61-65aa-48e7-b843-68cf870e7dd0" />

### 4. filescan, malfind 로그 저장하기

<img width="1071" height="76" alt="KakaoTalk_Snapshot_20260714_235834" src="https://github.com/user-attachments/assets/a02c2c56-374b-48a4-a428-0eb9e9560d28" />

> malfind를 사용하는 이유: 단순히 filescan으로 일일이 로그를 뒤져 문제가 되는 파일을 찾는 것은 효율이 떨어진다. 따라서 malfind를 이용하여 문제가 되는 파일을 먼저 찾고 findscan 로그를 이용하여 그 파일의 offset값을 찾는 것이 좋다.

<img width="621" height="490" alt="KakaoTalk_Snapshot_20260714_233330" src="https://github.com/user-attachments/assets/398c534b-0ade-4f75-a669-8848d8d3e044" />

<img width="532" height="501" alt="KakaoTalk_Snapshot_20260714_233343" src="https://github.com/user-attachments/assets/40071ba5-2ca5-4703-b1c5-af627300a59a" />

> malfind 확인 결과 explorer.exe와 reader_sl.exe가 탐지되었다. 또한 메모리 헤더에 'MZ'도 같이 탐지되었다.

- MZ: 파일 내부에 기록된 정보로 실행 가능한 파일의 데이터가 메모리에 숨어있다는 의미이다.

<img width="641" height="25" alt="KakaoTalk_Snapshot_20260714_234411" src="https://github.com/user-attachments/assets/7fd11805-c036-4cdc-a27a-a77bb9679592" />

<img width="736" height="16" alt="KakaoTalk_Snapshot_20260714_234427" src="https://github.com/user-attachments/assets/4efd80de-30c9-41e2-b139-fdbb3ba2416e" />

> filescan에서 offset을 찾을 때 가장 먼저 실행된 offset을 찾는 것이 좋다.

explorer.exe PID: 1484
reader_sl.exe PID: 1640

explorer.exe offset: 0x0000000002030f90 
reader_sl.exe offset: 0x00000000023ccf90

### 5. connections, netscan, sockets 로그 저장하기

<img width="914" height="331" alt="KakaoTalk_Snapshot_20260715_000224" src="https://github.com/user-attachments/assets/14810097-06bb-4433-8574-b9b8c6c1ad0d" />

> connections 확인결과 외부 네트워크로 연결된 흔적을 발견하였다.
- Local Address: 172.16.112.128:1038
- Remote Address: 41.168.5.140:8080

<img width="591" height="132" alt="KakaoTalk_Snapshot_20260715_001908" src="https://github.com/user-attachments/assets/9325d1c1-55fe-46b4-82cc-dae79e786cdc" />

> Sockets 확인결과 루프백 주소와 Local Address 통신 흔적만 나와 있다.

<img width="665" height="273" alt="KakaoTalk_Snapshot_20260715_002207" src="https://github.com/user-attachments/assets/0ab39e9c-d295-493b-9c09-147f51a27dc0" />

> 흔적에 나와 있는 PID는 1484 즉, explorer.exe이다. 

### 6. dumpfiles를 이용하여 파일 추출하기

<img width="914" height="331" alt="KakaoTalk_Snapshot_20260715_000224" src="https://github.com/user-attachments/assets/46a49b7b-2cea-4ff0-a54b-60c2477ce7e1" />

### 7. virustotal을 이용하여 바이러스 분석

- file.None.0x81ec3840.explorer.exe.dat

탐지: 0/54

<img width="845" height="479" alt="스크린샷 2026-07-15 000455" src="https://github.com/user-attachments/assets/491d84e2-d1b6-4bd7-a1df-c97512891ba4" />

- file.None.0x8224bd00.explorer.exe.img

탐지: 6/72

<img width="860" height="521" alt="스크린샷 2026-07-15 000507" src="https://github.com/user-attachments/assets/5ad65e43-f229-4f03-bf51-903a359a5ffb" />

- file.None.0x82137c08.reader_sl.exe.img

탐지: 6/61

<img width="862" height="599" alt="스크린샷 2026-07-15 000523" src="https://github.com/user-attachments/assets/4094fb22-eae5-4169-a459-523aebf45a5f" />

- file.None.0x822116f0.reader_sl.exe.dat

탐지: 2/69

<img width="850" height="421" alt="스크린샷 2026-07-15 000531" src="https://github.com/user-attachments/assets/a6e1a70d-54e1-455b-b3c8-7ad2cf58a271" />

> 악성코드가 있다고 분석한 곳이 있긴 하지만 아직 애매하다.

### 8. memdump로 메모리 덤프하기

<img width="912" height="315" alt="KakaoTalk_Snapshot_20260715_002637" src="https://github.com/user-attachments/assets/5a03ee07-06ba-4c25-b423-f081c1da8cef" />

### 9. String.exe로 텍스트 변환

> String.exe는 SysinternalsSuite를 환경변수에 등록하여 사용하면 된다.

<img width="715" height="50" alt="KakaoTalk_Snapshot_20260715_003035" src="https://github.com/user-attachments/assets/33b90e7e-6e52-4971-949b-68e3752587f5" />

### 10. 덤프 분석

1. connections에서 찾은 Remote Address(41.168.5.140)를 이용한다.

<img width="739" height="670" alt="KakaoTalk_Snapshot_20260715_003614" src="https://github.com/user-attachments/assets/3ec53a55-8af0-4a47-b578-5ea1c5c7bada" />

> [/zb/v_01_a/in/] 경로가 지속적으로 나온다.

2. [/zb/v_01_a/in/]를 이용한다.
------------------------------------------------------------
증거1번

line: 7231-7322
```
://41.168.5.140:8080/zb/v_01_a/in/
cryptnet.dll
%2.5.29.37
1.2.840.113549.1.9.16.1.1
LdapProvOpenStore
Ldap
LdapProvOpenStore
inetcomm.dll
WVTAsn1SpcMinimalCriteriaInfoDecode
EssReceiptDecodeEx
1.2.840.113549.1.9.16.2.1
EssReceiptRequestDecodeEx
1.2.840.113549.1.9.16.2.11
EssKeyExchPreferenceDecodeEx
1.2.840.113549.1.9.16.2.12
EssSignCertificateDecodeEx
1.2.840.113549.1.9.16.2.2
...
WVTAsn1SpcFinancialCriteriaInfoDecode
1.3.6.1.4.1.311.2.1.28
WVTAsn1SpcLinkDecode
1.3.6.1.4.1.311.2.1.30
WVTAsn1SpcSigInfoDecode
1.3.6.1.4.1.311.2.1.4
WVTAsn1SpcIndirectDataContentDecode
{000C10F1-0000-0000-C000-000000000046}
{06C9E010-38CE-11D4-A2A3-00104BD35090}
VerifyIndirectData
{1629F04E-2799-4DB5-8FE5-ACE10F17EBAB}
VerifyIndirectData
{1A610570-38CE-11D4-A2A3-00104BD35090}
VerifyIndirectData
{9BA61D3F-E73A-11D0-8CD2-00C04FC295EE}
CryptSIPVerifyIndirectData
{C689AAB8-8E78-11D0-8C47-00C04FC295EE}
CryptSIPVerifyIndirectData
{C689AAB9-8E78-11D0-8C47-00C04FC295EE}
CryptSIPVerifyIndirectData
{C689AABA-8E78-11D0-8C47-00C04FC295EE}
CryptSIPVerifyIndirectData
{DE351A42-8E59-11D0-8C47-00C04FC295EE}
CryptSIPVerifyIndirectData
{DE351A43-8E59-11D0-8C47-00C04FC295EE}
CryptSIPVerifyIndirectData
```
------------------------------------------------------------
- 증거2번

line: 12751-12763
```
http://41.168.5.140:8080/zb/v_01_a/in/
LUSTER_NETWORK_NAME_
erat
LUSTER_NETWORK_NAME_
z6D
TimeValidDllGetObject
7
\Documents and Settings\Robert\Local Settings\Temp
68.5.140
vPF
1.3.6.1.4.1.311.10.3.9
EGISTRY\USER\S-1-5-21-789336058-261478967-1417001333-1003
from publishers you trust. 
```
------------------------------------------------------------
- 증거3번

line: 12448-12457
```
CXTC:
: 41.168.5.140:8080
Nw<
CLSID\{0968E258-16C7-4DBA-AA86-462DD61E31A3}
6M%
6M%
6M%
http://www.download.windowsupdate.com/msdownload/update/v3/static/trustedr/en/authrootseq.txt
1.2.840.113549.1.9.16.1.1
```
------------------------------------------------------------
- 증거4번

line: 72015-72511
```
/C:\
DOCUME~1
Documents and Settings
ALLUSE~1
All Users
STARTM~1
*Start Menu
@shell32.dll,-21786
R@?
Programs
&Programs
@shell32.dll,-21782
Startup
$Startup
@shell32.dll,-21787
+00
/C:\
DOCUME~1
Documents and Settings
ALLUSE~1
All Users
...
*BusinessAppsHome*
*nab.com.au*
*us.hsbc.com*
*online.citibank.com/*
*BalanceHome*
*PassmarkChallenge*
*ktt.key.com*
*cm.netteller.com*
*/Web_Bank*
*jqueryaddonsv2.js*
http://188.40.0.138:8080/zb/v_01_a/in/cp.php
*account.authorize.net/*
```
------------------------------------------------------------
증거 5번

line: 2224-2227
```
Host: 41.168.5.140:8080
Content-Length: 229
Connection: Keep-Alive
Cache-Control: no-cache
```

### 11. procdump 하기
**악성코드가 존재할 수 있으므로 반드시 가상머신에서 실행한다.**

<img width="747" height="173" alt="KakaoTalk_Snapshot_20260715_013008" src="https://github.com/user-attachments/assets/5aafd745-6ac4-4a64-9f37-ff22d5555b69" />

<img width="699" height="323" alt="KakaoTalk_Snapshot_20260715_013305" src="https://github.com/user-attachments/assets/1466db13-bb35-4961-b0bb-373716eb74ed" />

> virustotal 분석 결과

<img width="840" height="608" alt="KakaoTalk_Snapshot_20260715_013346" src="https://github.com/user-attachments/assets/076a43b7-e9c0-4f8e-80b0-e90abef97b29" />

탐지: 34/70
유형: 트로이 목마

## 보고서

1. 발견: explorer.exe가 malfind에서 탐지되었다. 이후 외부 네트워크 연결 흔적(41.168.5.140)을 발견하였다.

2. 가설: explorer.exe가 외부 네트워크와의 통신에 이용된 악성코드일 것이란 가설을 세웠다.

3. 증거 수집: memdump를 이용하여 explorer.exe의 덤프를 확보하였다.
  - 증거5번: 41.168.5.140의 네트워크와의 'Keep-Alive' 지속적 연결 정황
  - 증거2번, 3번: OID 변조 의심 흔적
  - 증거1번: OID의 지속적 변조 흔적
  - 증거4번: 대량의 외부 은행 사이트와의 연결고리 발견

4. 시나리오:
- 악성코드가 섞인 pdf를 explorer.exe의 하위 프로세스 reader_sl.exe(Adobe Acrobat Reader)를 통해 읽는 과정에서 외부 네트워크(41.168.5.140)과 지속적 연결이 되었을 것이다. 악성코드가 활성화되면서 explorer.exe를 통해 OID가 지속적으로 변조되었을 것이고 피해자가 은행 업무를 하는 동안 휴대폰 번호, 계좌번호, OTP번호와 같은 금융정보들을 수집하고 외부 서버(188.40.0.138:8080/zb/v_01_a/in)로 보냈을 가능성이 높다. 이후 피해자는 금융 피해를 보았을 가능성이 매우 높다.
- Cridex는 정상파일처럼 생긴 pdf에 섞여 사용자가 pdf를 여는 순간 작동하는 트로이 목마 바이러스의 가능성이 매우 높다. 외부서버로 금융정보를 탈취하여 전송하는 고위험 악성프로그램이다.
