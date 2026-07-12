# 📂 01. 디지털 포렌식 소개 및 Warm-up

* 과거에 학습한 포렌식 기본 개념 복습 (5대 원칙 등)
* 인프런 강의 섹션 1 (소개) & 섹션 2 (디스크 이미징, 마운트, 삭제 파일 복구) 실습 기록

## 디지털포렌식 개론  

### 디지털포렌식이란?
전자기기의 저장매체 또는 인터넷에 남아 있는 디지털 정보를 분석해 범죄 단서를 찾는 수사기법

### 디지털포렌식의 필요성
과거에는 컴퓨터 범죄(해킹 등)과 관련한 한정적 정보 수집이었으나 최근에는 일반범죄에서도 디지털포렌식을 활용하여 범죄 정보 수집을 한다. 또한 형사사건 외에 민사사건에서도 디지털포렌식을 이용하며 일반기업에서도 내부감사에서도 수집한다.

### 5대 원칙(기본개념)
- 1. 정당성의 원칙: 모든 증거는 적법한 절차를 거쳐 획득되어야 한다.
- 2. 재현의 원칙: 같은 조건에서 분석을 진행했을 때 항상 같은 결과가 나와야 한다.
- 3. 신뢰성의 원칙: 분석에 사용된 도구와 절차는 신뢰할 수 있어야 한다. (FTK Imager 등의 검증된 도구 사용)
- 4. 연속성의 원칙(Chain of Custody): 증거가 수집된 후 법정에 제출되기까지의 이동 및 보관 과정이 명확히 기록되어야 한다.
- 5. 무결성의 원칙: 수집된 디지털 증거는 최초 수집 시점부터 법정 제출 시점까지 위·변조되지 않아야 한다. (디스크 이미징 시 쓰기 방지 조치 및 해시 값 검증이 필수적인 이유)

### 디지털 포렌식의 유형
#### 침해사고 대응
침해사고(예: 해킹)가 발생했을 때 피해를 최소화하기 위해 '실시간'으로 진행되며 이후 '사태 파악 및 수습'을 한다. 사태가 어느 정도 해결되면 시스템을 백업하고 포렌식 절차를 거쳐 시스템 이미지를 획득한다.

#### 증거 추출
획득한 시스템 이미지를 '사후 조사'와 '범죄 증거 수집'을 위해 '법적 절차'를 거쳐 분석한다. 

### 디지털포렌식의 종류
- 시스템 포렌식/디스크 포렌식: 컴퓨터 디스크(HDD, SSD) -> 윈도우, 리눅스, MacOS/개인, 서버, 클라우드 등의 운영체제 포렌식, 비휘발성 저장매체에 저장된 데이터 분석
- 메모리 포렌식: 컴퓨터 메모리(RAM) 분석
- 네트워크 포렌식: 네트워크 패킷, 네트워크 장비 로그, 네트워크 관련 설정 분석
- 모바일 포렌식: 모바일 디바이스(저장소, 메모리), IOT 디바이스 데이터 분석

## 디스크 이미징과 마운트, 메모리 덤프

> ⚠️ 중요 (포렌식 주의사항): 원본 매체를 PC에 연결하여 디스크 이미징을 수행하기 전, 원본 데이터가 위·변조되는 것을 방지하기 위해 반드시 하드웨어적 또는 소프트웨어적 '쓰기 방지(Write-Protection)' 조치를 취해야 합니다. (무결성의 원칙 준수)

### 디스크 이미징하는 순서

#### 1. 상단의 표시된 모양을 클릭한다.

<img width="272" height="52" alt="KakaoTalk_Snapshot_20260709_220908" src="https://github.com/user-attachments/assets/696bc427-4665-4ef4-b0dc-6f0ed7e80bce" />

#### 2. 이미징할 매체를 선택한다.
  - Physical Drive: 실제 하드디스크나 USB에 담겨 있는 전체데이터를 가져오고 싶을 때 선택
  - Logical Drive: OS가 인식하고 있는 특정 드라이브에 담겨 있는 데이터를 가져오고 싶을 때 선택(예: C, D드라이브)
  - Image File: 사전에 이미징 해놓은 디지털파일들을 불러올때 사용
  - Contents of a Folder: 특정 폴더에 담겨 있는 데이터를 가져오고 싶을 때 선택
  - IOS Advanved Logical Collection/Fernico Device: IOS/CD/DVD와 같은 컴퓨터 장비 이외에 있는 데이터를 가져오고 싶을 때 선택

<img width="394" height="326" alt="KakaoTalk_Snapshot_20260712_211407" src="https://github.com/user-attachments/assets/2d91e477-ef2b-4f4d-ab97-dec827f4d21c" />

#### 3. 추출할 드라이브/메모리를 선택한다.(개인 정보 보호를 위해 장치 시리얼 넘버는 마스킹처리 후 진행)

<img width="397" height="324" alt="KakaoTalk_Snapshot_20260709_220935" src="https://github.com/user-attachments/assets/f28a9f33-b90b-43fa-99bd-c47a1f79c02a" />

#### 4. Add를 클릭하여 이미지 저장 세부설정을 한다.

<img width="326" height="320" alt="KakaoTalk_Snapshot_20260709_221031" src="https://github.com/user-attachments/assets/a1a48903-f36c-4c9a-ac12-d4cfee980413" />

#### 5. 이미징 형식(포맷)을 선택한다.
  - RAW(dd): 디스크 원본을 가공없이 복사하는 형식(쉽게 말하면 날것 그대로)
  - SMART: 리눅스를 위한 포렌식 형식
  - E01: 포렌식 소프트웨어 'EnCase'에서 사용하는 압축과 무결성 검증이 통합된 형식
  - AFF: 특정 기업 기술에 종속되지 않은 오픈소스 조립식 포맷

<img width="365" height="309" alt="KakaoTalk_Snapshot_20260709_221102" src="https://github.com/user-attachments/assets/4e74092a-2455-4b54-8fa3-24b95ec3ddf6" />

#### 6. 증거의 기본 정보를 입력한다(사건번호, 증거번호, 분석가 이름 등을 입력한다. 이는 증거의 **연속성(Chain of Custody)과 신뢰성**을 확보하여, 향후 법정에서 증거 능력을 인정받기 위한 필수적인 기록 절차이다.)

<img width="364" height="308" alt="KakaoTalk_Snapshot_20260712_211449" src="https://github.com/user-attachments/assets/a3dd0cc1-96c1-423f-aac2-a8c180ecf434" />

#### 7. 이미지 저장 경로를 지정하고 파일 이름을 작성한다. 분할할 개수도 함께 설정한다.(첫 연습이라 분할하지 않고 이미징하였습니다.)
  - 분할을 하는 이유: 디스크의 거대한 용량으로 인해 발생할 수 있는 보관 및 네트워크 전송 문제를 해결하기 위해 사용한다.

<img width="366" height="310" alt="KakaoTalk_Snapshot_20260712_211542" src="https://github.com/user-attachments/assets/b5c07c16-1058-4581-9656-6256a7ee6cb5" />

### 실제 컴퓨터 드라이브를 이미징하고 싶었으나 현실적인 용량의 문제로 USB드라이브로 대체하였습니다.

> 실제 이미징 화면

<img width="303" height="216" alt="KakaoTalk_Snapshot_20260712_220341" src="https://github.com/user-attachments/assets/4ceec224-fa7c-44b1-9651-1e2b34dcf26b" />

> 이미징 완료 후 무결성 검증 확인 화면

<img width="511" height="389" alt="KakaoTalk_Snapshot_20260712_220719" src="https://github.com/user-attachments/assets/99e9a40a-05cf-4071-8403-8e1c7c81fbeb" />

<img width="553" height="307" alt="KakaoTalk_Snapshot_20260712_220902" src="https://github.com/user-attachments/assets/98a3a65a-b7fb-4fe9-b8cd-1d9220db230f" />

<img width="551" height="307" alt="KakaoTalk_Snapshot_20260712_220929" src="https://github.com/user-attachments/assets/5c0de12b-498a-472e-a11a-e124e388fe5e" />

## 디스크 이미지 마운트







