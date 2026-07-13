# 설치 환경 조작이 따로 필요하지 않은 Default 설치 툴은 다운로드 사이트만 작성했습니다.

## Volatility 설치

### 용도
> 메모리 포렌식 분석을 통해 운영체제에 실행 중인 프로세스, 네트워크 연결, 악성코드 흔적 등 휘발성 데이터를 추출 및 분석하여 침해 사고를 조사합니다.

#### 1. [Volatility 공식 Github](https://github.com/volatilityfoundation/volatility/releases)에서 본인 OS에 맞는 2.6 버전을 다운로드합니다.

<img width="830" height="563" alt="KakaoTalk_Snapshot_20260713_223840" src="https://github.com/user-attachments/assets/94fd3c69-0774-4fce-a84b-f7eaeb7670b9" />

#### 2. 실행 파일(`volatility_2.6_win64_standalone.exe` 등)을 원하는 경로(예: `C:\Tools\Volatility`)에 저장합니다.

### Windows Terminal 설치
> 참고: Windows 11은 기본적으로 터미널이 포함되어 있으므로 이 과정을 건너뛰어도 됩니다.

### 시스템 환경 변수 설정
> 이유: 터미널 어디에서나 `volatility` 명령어를 어느 경로에서든 즉시 호출하여 사용할 수 있도록 실행 파일의 절대 경로를 시스템에 등록하기 위함입니다.

#### 1.  윈도우 시작 메뉴에서 '시스템 환경 변수 편집'을 검색하여 실행합니다.

<img width="628" height="502" alt="스크린샷 2026-07-13 224318" src="https://github.com/user-attachments/assets/58cad441-07a4-4612-abff-25ac37d17489" />

#### 2. [환경 변수]를 클릭합니다.

<img width="341" height="438" alt="KakaoTalk_Snapshot_20260713_224412" src="https://github.com/user-attachments/assets/fad5ece5-402b-4f6d-a996-104a0c8d35a2" />

#### 3. [시스템 변수] 항목에서 'Path'를 찾고 [편집]을 누릅니다.

<img width="444" height="485" alt="KakaoTalk_Snapshot_20260713_232744" src="https://github.com/user-attachments/assets/1ddf93ce-8845-4328-a8e7-0adcb1a18857" />

#### 4. [새로 만들기]를 클릭한 후, Volatility 실행 파일이 저장된 폴더 경로를 입력하고 확인을 누릅니다.

<img width="381" height="415" alt="KakaoTalk_Snapshot_20260713_224646" src="https://github.com/user-attachments/assets/dafbacf6-3cbb-4733-9e31-cff0edb3f04e" />

#### 5. 결과 확인

<img width="377" height="415" alt="KakaoTalk_Snapshot_20260713_224726" src="https://github.com/user-attachments/assets/11680a06-f4d8-4dcf-8100-28cc1ddff6bc" />

### Windows Terminal 실행 후 Path 설정 확인
> 터미널 창에 'volat' + tab키를 하여 자동완성이 정상적으로 작동하는지 확인합니다.

<img width="644" height="404" alt="KakaoTalk_Snapshot_20260713_225507" src="https://github.com/user-attachments/assets/f5c8fbf3-fccf-45b0-9394-f43d397e4303" />



