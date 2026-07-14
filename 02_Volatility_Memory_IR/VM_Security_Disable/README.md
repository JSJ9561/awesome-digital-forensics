# 가상머신(Windows10 기준) Windows Defender, 방화벽, 자동 업데이트 비활성화 방법
## 간단한 사진과 경로만 개시할 것이며 Geminai의 답변을 참고했습니다.

> 악성코드가 자동으로 삭제되지 않도록 하고 각종 도구 최적화를 위함입니다.

## Winows Defender, 방화벽 비활성화
### 1. Windows Defender 및 실시간 감시 영구 중지
Windows 10의 '실시간 보호'를 레지스트리로 제어합니다.
1. Win + R 키를 누르고 regedit을 입력하여 레지스트리 편집기를 엽니다.
2. 다음 경로로 이동합니다.
   HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender
3. Windows Defender 폴더 우클릭 -> 새로 만들기(N) -> DWORD(32비트) 값(D) 선택.
4. 이름을 DisableAntiSpyware로 지정하고, 값을 1로 설정합니다.
5. Windows Defender 폴더 안에 Real-Time Protection이라는 하위 키(폴더)가 없다면 생성합니다.
6. Real-Time Protection 폴더 안에서 우클릭 -> 새로 만들기(N) -> DWORD(32비트) 값(D) 선택.  
7. 이름을 DisableRealtimeMonitoring으로 지정하고, 값을 1로 설정합니다.
   
### 2. 바이러스 및 위협 방지 설정
Windows 보안 센터에서 관련 기능을 비활성화합니다.
1. 동일한 레지스트리 경로(Windows Defender)에서 새로 만들기 -> DWORD(32비트) 값을 생성합니다.
2. 다음 항목들을 각각 생성하고 값을 1로 설정합니다.
  - DisableAntiVirus: 1
  - DisableIOAVProtection: 1 (파일 스캔 방지)
  - DisableScriptScanning: 1 (스크립트 스캔 방지)

<img width="571" height="386" alt="KakaoTalk_Snapshot_20260714_215409" src="https://github.com/user-attachments/assets/c70fde0c-d652-4b3b-9189-95833fd17193" />

### 3. 방화벽 및 네트워크 보호 중지
방화벽은 레지스트리보다는 명령어를 사용하는 것이 더 확실하고 간편합니다.
1. Win + S를 누르고 cmd를 검색하여 관리자 권한으로 실행합니다.
2. 다음 명령어를 입력하여 실행합니다.
  **netsh advfirewall set allprofiles state off**
   - 이 명령어를 실행하면 모든 네트워크 프로필(도메인, 개인, 공용)의 방화벽이 즉시 중지됩니다.

<img width="551" height="314" alt="KakaoTalk_Snapshot_20260714_215626" src="https://github.com/user-attachments/assets/149612fa-87cc-4a29-b104-530323c2fc4a" />

## 자동업데이트 비활성화
### 1. 서비스에서 Windows Update 중지 (필수)  
가장 기본적으로 업데이트 서비스 자체를 비활성화해야 합니다.  
1. Win + R을 누르고 services.msc를 입력하여 실행합니다.
2. 목록에서 Windows Update 항목을 찾아 더블 클릭합니다.
3. 일반 탭: 시작 유형을 '사용 안 함'으로 변경하고, 서비스 상태를 '중지' 버튼을 눌러 종료합니다.
4. 복구 탭: 첫째 실패, 둘째 실패, 후속 실패를 모두 '동작하지 않음'으로 설정합니다. (이렇게 해야 서비스가 자동으로 다시 살아나는 것을 방지할 수 있습니다.)

### 2. 로컬 그룹 정책 편집기 설정 (Pro 버전 이상)  
Windows 10 Pro 이상을 사용 중이라면 이 방법이 가장 강력합니다.
1. Win + R을 누르고 gpedit.msc를 입력하여 실행합니다.
2. 다음 경로로 이동합니다:컴퓨터 구성 > 관리 템플릿 > Windows 구성 요소 >   Windows 업데이트
3. 오른쪽 목록에서 '자동 업데이트 구성'을 더블 클릭합니다.
4. '사용 안 함'을 선택하고 확인을 누릅니다.

<img width="516" height="481" alt="KakaoTalk_Snapshot_20260714_221131" src="https://github.com/user-attachments/assets/ccad7406-6441-4867-8769-9ac713b4fa70" />

## **위 작업을 완료하면 반드시 재부팅을 합니다**
## **스냅샷을 반드시 찍습니다. 실습 과정 중 가상머신에 문제가 생기면 초기 상태로 되돌리기 위함입니다.**
# **스냅샷을 습관화합시다.**












