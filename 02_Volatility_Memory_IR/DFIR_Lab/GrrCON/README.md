# GrrCON 풀이

## 분석 시나리오
```
1. imageinfo 명령어로 정보 확인
2. ps 명령어로 프로세스 확인
3. cmd 명령어로 입력 명령어 확인
4. 인터넷 연결 상태 확인
5. filescan, malfind, dlllist 확인
6. dumpfiles 하기
7. memdump 명령어로 덤프 확인
8. 분석
9. 보고서
```

## 1. imageinfo로 정보 확인

<img width="791" height="299" alt="KakaoTalk_Snapshot_20260718_173558" src="https://github.com/user-attachments/assets/fb913451-5d51-483a-9525-8642f41a9347" />

profile: Win7SP1x86_23418, Win7SP0x86, Win7SP1x86

> Windows7 이상의 운영체제 확인

## 2. ps 명령어로 프로세스 로그 저장

<img width="751" height="234" alt="KakaoTalk_Snapshot_20260718_174236" src="https://github.com/user-attachments/assets/2260922c-72c0-46dd-bcc1-ddd7545466fe" />

<img width="785" height="223" alt="KakaoTalk_Snapshot_20260718_174319" src="https://github.com/user-attachments/assets/5297d8f1-9ea8-422c-bd66-963e0114533d" />

```
wininit.exe: PC가 켜질 때 백그라운드에서 필수 시스템 초기화를 담당하는 정상적인 Windows 필수 프로세스
dllhost.exe: COM+ 기반 응용 프로그램을 관리하는 정상적인 Windows 시스템 파일
msdtc.exe: Microsoft Distributed Transaction Coordinator(마이크로소프트 분산 트랜잭션 코디네이터)의 실행 파일
dwm.exe: 윈도우의 투명 효과, 애니메이션, 고해상도 화면 렌더링 등 시각적 요소를 담당하는 필수 핵심 프로세스
TeamView_Des: 원격 제어 프로그램인 TeamViewer의 구성 요소(프로세스)
TeamViewer.exe: 다른 컴퓨터나 스마트기기에 원격으로 접속하여 화면을 보고 제어할 수 있게 해주는 원격 데스크톱 프로그램의 실행 파일
tv_w32.exe: 원격 제어 및 화면 공유 프로그램인 팀뷰어(TeamViewer)의 32비트 프로세스
mstsc.exe: 다른 컴퓨터나 서버에 원격으로 접속하여 제어할 수 있는 Windows 기본 내장 프로그램
vmtoolsd.exe: 가상 머신(VM)과 호스트 컴퓨터 간의 원활한 연결을 돕는 'VMware Tools'의 핵심 서비스 프로세스
OUTLOOK.EXE: Microsoft Outlook 클래식 데스크톱 앱을 실행하는 Windows 실행 파일, 전자메일 실행 프로세스
iexplorer.exe: Microsoft의 웹 브라우저인 Internet Explorer를 실행하는 핵심 실행 파일
taskhost.exe: DLL 파일 기반의 Windows 작업을 실행하고 제어하는 데 사용되는 정상적이고 필수적인 Windows 운영 체제 프로세스
mscorsvw.exe: 윈도우의 .NET Framework(닷넷 프레임워크) 최적화 서비스
sppsvc.exe: Windows 운영 체제의 소프트웨어 보호 플랫폼 서비스(Software Protection Platform Service) 실행 파일
wce.exe: 윈도우 시스템의 메모리에서 사용자 계정 자격 증명(로그온 세션, 비밀번호 해시, LM/NT 해시 등)을 추출하고 관리하는 보안 도구
mstsc.exe: Microsoft Windows의 원격 데스크톱 연결(Remote Desktop Connection) 프로그램
```

### pstree 확인 결과
- 필수 시스템 프로세스를 제외한 프로세스
```
TeamViewer.exe
exploler.exe
iexplore.exe
```

### psxview 확인 결과
- 필수 프로세스를 제외한 숨긴 프로레스 확인
```
vmtoolsd.exe
explole.exe
d
' '
u?US
STX
```

> 원격 제어 프로세스 확인(tv_w32.exe, mstsc.exe), 의미불명의 프로세스 확인(d, ' ', u?US, STX), cmd.exe 실행 프로세스 확인(cmd.exe, exploler.exe, iexplorer.exe)

## 3. cmd확인 명령어로 로그 저장

### cmdline 확인 결과

<img width="272" height="26" alt="KakaoTalk_Snapshot_20260718_181925" src="https://github.com/user-attachments/assets/f3a7fd17-f28b-4a16-82a7-d0a3a23d7b0b" />

<img width="855" height="24" alt="KakaoTalk_Snapshot_20260718_181937" src="https://github.com/user-attachments/assets/d2187de3-e0dd-4402-b080-6fb69fb36813" />

```
sppsvc.exe을 실행한 흔적 확인
tv_w32.exe에서 실행한 명령어 확인

"C:\Users\FRONTD~1\AppData\Local\Temp\TeamViewer\tv_w32.exe" --action hooks  --log C:\Users\frontdesk\AppData\Roaming\TeamViewer\TeamViewer10_Logfile.log
```

### cmdscan 확인 결과
```
계정 자격 증명 추출 프로세스인 wce.exe의 지속적인 실행 확인
```

### consoles 확인 결과

<img width="629" height="374" alt="KakaoTalk_Snapshot_20260718_181754" src="https://github.com/user-attachments/assets/f53fbca2-edb0-4b55-a685-1390dbb1ed8d" />

```
Temp 디렉터리에 접근한 흔적 확인
wce.exe의 지속적인 실행 확인
```

> wce.exe는 계정탈취 프로세스이다. 이 프로세스가 실행된 흔적이 나온 시점부터 악성코드로 간주하고 진행

## 4. 인터넷 연결 상태 확인

> Windows7 운영체제이므로 netscan 활용

<img width="917" height="257" alt="KakaoTalk_Snapshot_20260718_182816" src="https://github.com/user-attachments/assets/ad15b3bd-846a-4bf9-b645-aa4eb0ada4a3" />

```
iexplore.exe: 180.76.254.120:22 -> 통신 IP, SSH포트 확인
TeamViewer.exe: 192.96.201.138:5938, 107.6.97.19:5938 -> 통신 IP 확인
```

> Local Address는 루프백 IP만 확인되었다. 따라서 내부망 컴퓨터를 거점 삼아 탈취한 계정정보를 두가지 IP로 각각 수신, 송신한 것으로 추정

## 5. filesan, malfind, dlllist 로그 저장

### malfind 확인 결과

> explorer.exe, TeamViewer.exe, OUTLOOK.EXE의 PAGE_EXECUTE_READWRITE 확인

### dlllist 확인 결과

<img width="598" height="120" alt="KakaoTalk_Snapshot_20260718_185334" src="https://github.com/user-attachments/assets/9c9b115a-c79d-4f64-b826-9adbf44332a3" />

<img width="840" height="41" alt="KakaoTalk_Snapshot_20260718_185417" src="https://github.com/user-attachments/assets/c54e6197-7024-4c5e-8e8c-3e29deaa4f91" />

<img width="654" height="48" alt="KakaoTalk_Snapshot_20260718_185433" src="https://github.com/user-attachments/assets/086a41f8-877c-4f34-90c3-bda9f9302adf" />

> TeamView.exe 및 하위프로세스의 비정상적인 설치 경로 확인

```
explorer.exe PID: 2116
TeamViewer.exe PID: 2680
OUTLOOK.EXE PID: 3196
```

### filescan 확인 결과
```
explorer.exe offset: 0x000000003de1ece8
TeamViewer.exe offset: 0x000000003fd57ae8
OUTLOOK.EXE: 0x000000003de2a698
```

- 추가로 확인할 프로세스
```
sppsvc.exe offset: 0x000000003debe1b8
iexplore.exe offset: 0x000000003e7c6038
wce.exe offset: 0x000000003df31038 
```

## 6. dumfiles로 저장

> dumfiles 진행 중 wce.exe를 덤프하면 즉시 보안프로그램으로 인해 삭제되었다. 따라서 해당 프로세스는 가상머신에서 덤프를 진행

<img width="208" height="49" alt="KakaoTalk_Snapshot_20260718_193311" src="https://github.com/user-attachments/assets/deb760ca-f0a3-4927-b3e8-28290f90f966" />

<img width="833" height="445" alt="KakaoTalk_Snapshot_20260718_193135" src="https://github.com/user-attachments/assets/d178b0e2-c905-4eff-b75e-8e62619d1407" />

> 예상한 대로 악성코드임이 확인

- 이전의 consoles 결과에서 C:\Windows\Temp\w.tmp에 저장하는 흔적을 발견, PID는 탐색 불가
- psxview에서 발견한 로그 중 explorer.exe가 발견, 이 과정에서 실행했다고 추정, PID: 3932

### 조사 필요한 프로세스 PID
```
TeamViewer.exe PID: 2680
explorer.exe PID: 2116
OUTLOOK.EXE PID: 3196
iexplore.exe PID: 2996
mstsc.exe PID: 2844
sppsvc.exe PID: 3900
tv_w32.exe PID: 4064

explorer.exe PID: 3932
```
> iexplore.exe에서 cmd.exe의 실행 흔적이 있어서 추가 조사

> mstsc.exe는 원격접속 프로그램이므로 추가 조사

> sppsvc.exe는 보안 무력화 흔적 추가 조사

## 7. memdump로 저장, strings로 변환

> 숨은 explorer.exe는 memdump 실패했다.

<img width="784" height="71" alt="KakaoTalk_Snapshot_20260718_201250" src="https://github.com/user-attachments/assets/0781f470-b40f-4519-a968-aea91ce22639" />

- 활용할 단서
```
iexplore.exe: 180.76.254.120
TeamViewer.exe: 192.96.201.138

wce.exe
w.tmp
Temp
```

## 8. 분석

### 1. iexplore.exe

<img width="347" height="120" alt="KakaoTalk_Snapshot_20260718_210512" src="https://github.com/user-attachments/assets/3d73139a-bc59-4094-81f3-9d4feaf4b607" />

<img width="243" height="180" alt="KakaoTalk_Snapshot_20260718_210525" src="https://github.com/user-attachments/assets/13f79b5a-8e23-47e1-9ec3-8a319e9fb32d" />

<img width="802" height="90" alt="KakaoTalk_Snapshot_20260718_212040" src="https://github.com/user-attachments/assets/1d8d57a4-2c3e-4265-b1a8-83a564265d9c" />

- anyconnect 명령어 확인

- 수상한 도메인 확인
```
xtremerat01.dyndns.org
xtremerat02.dyndns.org
xtremerat03.dyndns.org
```

- 다운로드 링크 확인
```
http://180.76.254.120/AnyConnectInstaller.exe
```

- iexplore.exe를 통한 wce.exe 다운로드 의심 흔적
<img width="300" height="53" alt="KakaoTalk_Snapshot_20260718_222403" src="https://github.com/user-attachments/assets/0991fb8c-c978-4033-80fa-b1ec2fd71613" />

```
n\Device\HarddiskVolume2\Users\frontdesk\Downloads\wce.exe
```

- iexplore.exe의 cmd.exe실행 로그 중 일부

<img width="320" height="404" alt="KakaoTalk_Snapshot_20260718_224341" src="https://github.com/user-attachments/assets/c0f8cc11-513d-4eb7-97c0-ececc91d47bd" />

```
C:\Users\frontdesk\TeamViewerQS_en.exe
shellcommand
shellcommand
C:\Users\Whiterose\Downloads\TeamViewerQS_en.exe
ping|
ping
623677
10.1.1.21 - Remote Desktop Connectio4
10.1.1.21 - Remote Desktop Connectio|
pong|623677|10.1.1.21 - Remote Desktop Connection
pong
pong|623677|10.1.1.21 - Remote Desktop Connection
shellcommand|copy c:\windows\temp\rar.exe z:\users\gideon
copy c:\windows\temp\rar.exe z:\users\gi8
shell|shellcommand|copy c:\windows\temp\rar.exe z:\users\gideon
        1 file(s) copied.
Z:\Users\gideon>
Z:\Users\gide
shell|shellcommand|        1 file(s) copied.
Z:\Users\gideon>
Z:\Users\gideo
dir
 Volume in drive Z has no label.
 Volume Serial Number is 7491-152F
 Directory of Z:\Users\gideon
10/09/2015  08:16 AM    <DIR>          .
10/09/2015  08:16 AM    <DIR>          ..
10/09/2015  07:56 AM                58 1.bat
10/09/2015  03:59 AM    <DIR>          Contacts
10/09/2015  03:59 AM    <DIR>          Desktop
10/09/2015  03:59 AM    <DIR>          Documents
10/09/2015  03:59 AM    <DIR>          Downloads
10/09/2015  03:59 AM    <DIR>          Favorites
10/09/2015  03:59 AM    <DIR>          Links
10/09/2015  03:59 AM    <DIR>          Music
10/09/2015  03:59 AM    <DIR>          Pictures
10/09/2015  06:44 AM           503,800 Rar.exe
10/09/2015  03:59 AM    <DIR>          Saved Games
10/09/2015  03:59 AM    <DIR>          Searches
10/09/2015  03:59 AM    <DIR>          Videos
10/09/2015  08:01 AM               326 w.tmp
10/09/2015  06:45 AM           199,168 wce.exe
               4 File(s)        703,352 bytes
              13 Dir(s)  22,210,027,520 bytes free
Z:\Users\gideon>
Z:\Users\gideon>
```

- sppsvc.exe를 통한 방화벽 무력화

<img width="842" height="14" alt="KakaoTalk_Snapshot_20260718_230240" src="https://github.com/user-attachments/assets/af5af1cc-5a99-4315-a550-ce62f49ca1ea" />

```
v2.10|Action=Allow|Active=FALSE|Dir=In|Protocol=6|Profile=Private|Profile=Public|LPort=1688|RA4=LocalSubnet|RA6=LocalSubnet|App=%SystemRoot%\system32\sppsvc.exe|Svc=sppsvc|Name=@FirewallAPI.dll,-28003|Desc=@FirewallAPI.dll,-28006|EmbedCtxt=@FirewallAPI.dll,-28002|
```

> 파악 가능 정보
```
공격자 이름: Whiterose
공격자 IP: 192.96.201.138
피해자 이름: gideon(front-desk)

iexplore.exe의 cmd에서 TeamViewerQS.exe 실행
z드라이브 마운트를 통한 피해자 하드드라이브 이용
방화벽 비활성화를 통한 보안무력화
```

### 2. OUTLOOK.EXE

> iexplore.exe에서 다운로드 링크를 확인하고 피싱메일을 의심

<img width="861" height="163" alt="KakaoTalk_Snapshot_20260718_212240" src="https://github.com/user-attachments/assets/97b7d633-acff-4416-a54a-0c182195b902" />

- 피해자 컴퓨터 이름(front desk) 확인
```
front desk<CALwgF5bo54VoNzmLrOs4R500JQ-zifiDB=UxCyiEZTisogfmCQ@mail.gmail.com>
```

- 메일 내용: 성능향상을 위한 VPN 업데이트 다운로드를 하세요

### 3. explorer.exe

> wce.exe 배포 경로 파악을 위해 wce.exe를 검색

<img width="474" height="135" alt="KakaoTalk_Snapshot_20260718_221628" src="https://github.com/user-attachments/assets/f95f6694-90ae-4b27-b654-0eb8972b99e5" />

<img width="351" height="24" alt="KakaoTalk_Snapshot_20260718_222735" src="https://github.com/user-attachments/assets/1e4e30ed-5920-45cd-a721-5cc9eae5d0a5" />

- wce.exe를 통해 "gideon" 계정 탈취
```
Administrator: cmd (running as FRONT-DESK-PC\Administrator)
- wce.exe  -w 
Administrator: C:\Program Files\Internet Explorer\iexplore.exe
- dir
  c:\windows\temp\rar.exe z:\users\gideon
inistrator flagadmin@1234
OleMainThreadWndName
IME
Placeholder

cmd.exe /c wce.exe -w > c:\Users\gideon\w.tmp
```

### 4. TeamViewer.exe

<img width="444" height="26" alt="KakaoTalk_Snapshot_20260718_230957" src="https://github.com/user-attachments/assets/1863bcac-dcea-45cf-ace9-d02bcee2161f" />

- TeamViewer.exe의 cmd를 통한 iexplore.exe 실행 흔적 확인
```
Administrator: C:\Program Files\Internet Explorer\iexplore.exe
```

## 보고서

### 침해 시나리오

1. 피해자가 피싱메일을 통해 [http://180.76.254.120/AnyConnectInstaller.exe]에 접근 및 악성파일 AnyConnectInstaller를 다운로드
2. 피해자가 다운로드한 파일을 실행하면서 TeamViewer에 패치
3. 피해자가 TeamViewer를 실행하는 순간 tv_w32.exe를 통한 원격접속
4. 원격접속한 피해자의 TeamViwer cmd를 통한 iexplore 접속
5. iexplore에서 sppsvc를 활용해 방화벽을 무력화 
6. wce.exe를 다운로드
7. 원격접속한 피해자의 explorer.exe cmd를 통해 wce.exe를 실행
8. 피해자 계정(gideon) 탈취
9. mstsc.exe를 통해 탈취한 계정을 활용하여 공격범위(인트라넷 내부) 확장








