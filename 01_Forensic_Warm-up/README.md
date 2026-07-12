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

> 이미징을 한 파일을 읽는 방법은 4가지가 있지만 자주 쓰는 2가지를 해볼 생각입니다.

### 1. 이미지 디스크 마운트하기
> 장점

> 직접적인 탐색 가능: 이미징된 파일을 실제 물리적인 드라이브(예: `E:\`, `F:\` 등)로 OS에 인식시켜, 윈도우 파일 탐색기를 통해 일반 디스크처럼 직관적으로 내부 구조를 확인할 수 있습니다.

> 타 분석 도구와의 연계성: OS가 드라이브로 인식하기 때문에, FTK Imager 외에 다른 포렌식 분석 도구나 백신 프로그램 등으로 해당 드라이브를 바로 스캔하고 분석하기에 용이합니다.

### 마운트 순서와 증거로 불러오기

### [Step 1] 디스크 이미지 마운트 진행
#### 1. 상단의 동전 두개가 있는 모양을 클릭한다.

<img width="278" height="33" alt="KakaoTalk_Snapshot_20260712_224016" src="https://github.com/user-attachments/assets/97b00010-1401-4555-855c-ad4c09004867" />

#### 2. 디스크 이미지 파일을 찾아 불러오고 마운트한다.

<img width="429" height="417" alt="KakaoTalk_Snapshot_20260712_224713" src="https://github.com/user-attachments/assets/2d239368-f283-4043-bacf-700d3a9647da" />

> 마운트 후 화면

<img width="431" height="416" alt="KakaoTalk_Snapshot_20260712_230343" src="https://github.com/user-attachments/assets/da94af18-8a30-4d00-ac90-4458e26ca013" />

> 파일 탐색기에 드라이브가 인식되어 있다.
<img width="143" height="144" alt="KakaoTalk_Snapshot_20260712_224836" src="https://github.com/user-attachments/assets/8f2a7ad3-d501-4713-a7ee-f4cee88534ea" />

### [Step 2] FTK Imager에 증거(Evidence)로 불러오기
#### 3. 상단의 더하기가 있는 지구 모양을 클릭한다. 혹은 파일 -> Add Evidence Item 클릭

<img width="278" height="33" alt="KakaoTalk_Snapshot_20260712_224016 - 복사본" src="https://github.com/user-attachments/assets/0eb2c47c-fb1d-43fc-8442-3c9094d6f25f" />

#### 4. Physical Drive를 선택한다.

<img width="395" height="327" alt="KakaoTalk_Snapshot_20260712_224801" src="https://github.com/user-attachments/assets/c957aaa6-643e-4a16-81f5-40151f178916" />

#### 5. 마운트되어 있는 드라이브들 중 증거로 불러올 드라이브를 찾는다.

<img width="394" height="326" alt="KakaoTalk_Snapshot_20260712_224821" src="https://github.com/user-attachments/assets/45fe7778-ba80-468e-9392-214ba3c10ffe" />

> **실습 노트:** 4GB 내외의 비교적 작은 용량임에도 로드 시 수 초에서 수 분간의 지연(Freeze) 현상이 발생할 수 있습니다. 이는 FTK Imager가 마운트된 드라이브의 파티션 구조와 파일 시스템 메타데이터(MFT 등)를 내부적으로 파싱(Parsing)하고 인덱싱하는 과정이 수반되기 때문입니다.

> 결과

<img width="469" height="225" alt="KakaoTalk_Snapshot_20260712_225032" src="https://github.com/user-attachments/assets/f9adb6b5-0bee-4d46-a5ef-9b8c7837e632" />

### 2. 디스크 이미지 읽어오기
> 장점

> 비파괴적/안전한 분석: OS에 별도의 드라이브를 할당하거나 수정하지 않고, FTK Imager 프로그램 내부의 'Evidence Tree'에 독립적인 객체로 로드하여 안전하게 분석할 수 있습니다.

> 포렌식 특화 기능 활용: 삭제된 파일 흔적 분석, 파일 시스템의 메타데이터(MFT 영역 등) 확인, 해시값 추출 등 포렌식 전용 기능을 프로그램 내에서 가장 빠르고 정확하게 수행할 수 있습니다.

### 증거로 불러오기(디스크 이미지를 읽어오는 방법은 따로 마운트 과정이 필요하지 않다)

#### 1. 상단의 더하기가 있는 지구 모양을 클릭한다. 혹은 파일 -> Add Evidence Item 클릭

<img width="278" height="33" alt="KakaoTalk_Snapshot_20260712_224016 - 복사본" src="https://github.com/user-attachments/assets/c492ff71-2111-452b-9d3d-50fb01c1956a" />

#### 2. Image File을 선택한다.

<img width="398" height="327" alt="KakaoTalk_Snapshot_20260712_225242" src="https://github.com/user-attachments/assets/388c2e9d-5c72-4642-91d6-1431714600fa" />

#### 3. 불러올 이미지 파일을 선택한다.

<img width="398" height="325" alt="KakaoTalk_Snapshot_20260712_225303" src="https://github.com/user-attachments/assets/04af5f0f-8554-42ad-a538-14cc26f9cf6f" />

> 결과

<img width="336" height="139" alt="KakaoTalk_Snapshot_20260712_225346" src="https://github.com/user-attachments/assets/7fe837ed-9c3e-46d1-ac9c-d442be65257b" />

### 💡 실습 결과 분석: 불러오기 방식에 따른 차이점

두 방식은 FTK Imager 내부의 `Evidence Tree`에 표시되는 경로와 형태가 다릅니다. 이 차이는 포렌식 데이터 접근 방식의 이해에 매우 중요합니다.

| 표시 형태 | 분석 및 의미 | 주요 특징 |
| ----- | ----- | ----- |
| **`\\.\PHYSICALDRIVE2`**<br>(Physical Drive 방식) | 윈도우 OS가 인식하는 하드웨어 장치 고유 경로 (Win32 네임스페이스)를 의미합니다. | 파일 시스템을 거치지 않고, 디스크 섹터에 직접 다이렉트(Raw)로 접근 중임을 나타냅니다. |
| **`E_Flash_Drive.E01`**<br>(Image File 방식) | 분석가가 사전에 덤프(Dump)하여 생성해 둔 정적 파일의 이름과 확장자입니다. | 하드웨어 장치 직결이 아닌, 기존에 만들어진 가상 복제본 파일을 단순 로드(Open)했음을 나타냅니다. |


