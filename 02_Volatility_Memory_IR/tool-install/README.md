# 설치 환경 조작이 따로 필요하지 않은 Default 설치 툴은 다운로드 사이트만 작성했습니다.

## Volatility 설치

### 용도
> 메모리 포렌식 분석을 통해 운영체제에 실행 중인 프로세스, 네트워크 연결, 악성코드 흔적 등 휘발성 데이터를 추출 및 분석하여 침해 사고를 조사합니다.

#### 1. [https://github.com/volatilityfoundation/volatility/releases] 공식 Github 레포지토리에서 본인 OS에 맞는 2.6버전을 다운받는다.

<img width="830" height="563" alt="KakaoTalk_Snapshot_20260713_223840" src="https://github.com/user-attachments/assets/94fd3c69-0774-4fce-a84b-f7eaeb7670b9" />

#### 2. 원하는 디렉터리에 압축을 해제한다.

### Windows Terminal 설치
> 해당 과정은 설치가 안되어 있는 OS의 경우 따로 설치를 해야 한다. Windows11에서는 기본으로 설치되어 나오기 때문에 해당 과정은 건너뛴다.

### 시스템 환경 변수 설정
> 이유: 터미널 어디에서나 `volatility` 명령어를 어느 경로에서든 즉시 호출하여 사용할 수 있도록 실행 파일의 절대 경로를 시스템에 등록하기 위함이다.

#### 1.  윈도우 시작 메뉴에서 '시스템 환경 변수 편집 검색 후 실행한다.

<img width="628" height="502" alt="스크린샷 2026-07-13 224318" src="https://github.com/user-attachments/assets/58cad441-07a4-4612-abff-25ac37d17489" />

#### 2. 환경 변수를 클릭한다.

<img width="341" height="438" alt="KakaoTalk_Snapshot_20260713_224412" src="https://github.com/user-attachments/assets/fad5ece5-402b-4f6d-a996-104a0c8d35a2" />

#### 3. 시스템 변수 창에서 'path'를 찾고 '새로 만들기'를 클릭한다.

<img width="443" height="486" alt="KakaoTalk_Snapshot_20260713_224625" src="https://github.com/user-attachments/assets/4d7b008c-5db0-4832-b050-cc1041133954" />

#### 4. 'Volatility'폴더의 경로를 복사하고 '새로 만들기'를 클릭한 후 붙여넣기 한다.

<img width="381" height="415" alt="KakaoTalk_Snapshot_20260713_224646" src="https://github.com/user-attachments/assets/dafbacf6-3cbb-4733-9e31-cff0edb3f04e" />

#### 5. 결과 확인

<img width="377" height="415" alt="KakaoTalk_Snapshot_20260713_224726" src="https://github.com/user-attachments/assets/11680a06-f4d8-4dcf-8100-28cc1ddff6bc" />

### Windows Terminal 실행 후 path 설정 확인
> 터미널 창에 volatitlity + tab키를 하여 자동완성되는지 확인한다.

<img width="644" height="404" alt="KakaoTalk_Snapshot_20260713_225507" src="https://github.com/user-attachments/assets/f5c8fbf3-fccf-45b0-9394-f43d397e4303" />



