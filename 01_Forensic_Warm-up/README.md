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

## 디스크 이미징

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

> 마운트된 이미지 디스크를 제거 하고 싶으면 상단의 동전모양을 누르고 나오는 창에 다시 들어가서 Unmount할 드라이브를 선택하고 Unmount를 클릭하면 된다.

<img width="429" height="417" alt="KakaoTalk_Snapshot_20260712_224713 - 복사본" src="https://github.com/user-attachments/assets/bae1d149-b231-4c3f-a222-048d2fa5dff6" />

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

## 메모리 덤프

> ⚠️ 실습 과정 중 덤프가 제대로 되지 않는 문제가 있었습니다. 이에 대해 찾아본 내용도 함께 올립니다.

#### 1. 상단에 램 모양 아이콘을 클릭한다.

<img width="278" height="33" alt="KakaoTalk_Snapshot_20260712_224016 - 복사본 (3)" src="https://github.com/user-attachments/assets/2113a787-a8a9-4dd9-9cb7-c1ce6900c596" />

#### 2. 덤프한 메모리를 저장할 경로를 설정한다.

<img width="257" height="212" alt="KakaoTalk_Snapshot_20260712_225115" src="https://github.com/user-attachments/assets/a736d784-defe-441a-a499-f7d10c102ac7" />

#### 3. Capture Memory를 실행하여 결과 확인

<img width="324" height="161" alt="KakaoTalk_Snapshot_20260712_225127" src="https://github.com/user-attachments/assets/70448382-ab9f-4307-8452-e5007e47bbe0" />

> 실행 결과, 위 스크린샷과 같이 메모리 덤프 실패 오류가 발생하였습니다.

#### 🕵️‍♂️ 에러 원인 추정 및 자체 검증
1. **관리자 권한 미부여**
   * *검증:* FTK Imager를 '관리자 권한으로 실행'한 뒤 재시도하였으나 동일한 오류 발생 (원인 아님).
2. **저장 공간 부족**
   * *검증:* 약 300GB의 여유 공간이 있는 D드라이브를 경로로 지정함 (원인 아님).
3. **Windows 보안 프로그램(백신) 차단**
   * *검증:* 초기 설치 시 Windows Defender 예외 설정을 완료한 상태임 (원인 아님).

### 💡 해결 방안 및 대체 실습

해당 시스템 환경 특성상 FTK Imager의 메모리 덤프 모듈이 정상 동작하지 않는 것으로 판단되어, 아래와 같은 대체 방안을 수립하였습니다.

1. **대체 도구 활용**: FTK Imager 대신 `WinPmem` 또는 `DumpIt`과 같은 메모리 포렌식 전용 덤프 도구를 활용하여 추출을 시도할 수 있습니다.
2. **공인된 샘플 활용**: 덤프 파일 생성 연습 대신, [CyberDefenders DumpMe 챌린지](https://cyberdefenders.org/blueteam-ctf-challenges/dumpme/)에서 제공하는 공개 메모리 덤프 샘플(.raw)을 다운로드하여 분석 실습을 대체 진행하였습니다. 
   * *참고:* 해당 샘플은 악성코드 감염 흔적을 포함하고 있어, 향후 침해사고 분석 및 메모리 포렌식 학습에 더욱 유용합니다.
  
## 삭제 파일 복구

### FTK Imager를 이용하여 복구하기

### 이미지 파일을 읽어와서 진행

<img width="725" height="182" alt="KakaoTalk_Snapshot_20260713_001223" src="https://github.com/user-attachments/assets/02f6e170-3e7d-44e1-8406-797486023d88" />

> 예시 사진

<img width="976" height="546" alt="deletedfile_ftkrecover" src="https://github.com/user-attachments/assets/1578c0c0-2c8f-46b2-9c53-bad88b6fdeb1" />

- 출처: [https://mattcasmith.net/2021/04/02/file-carving-recovering-deleted-file-disk-image]

> 이미지 파일을 불러오면 evidence tree(초록색 상자)가 보인다. evidence tree를 열어보면 'root' 파일이 존재한다. 'root'파일을 살펴보면 'x'표시된 아이콘(빨간색 상자)이 존재하는데 이 파일들이 삭제된 파일들이다. 만약 시스템 드라이브 즉, 컴퓨터 하드디스크나 ssd를 열어보면 예시 사진과 같이 'RECYCLE.BIN' 혹은 '$' 표시된 파일이 존재하는데 그 곳에 삭제된 파일들이 존재한다. 

### 복구 방법

#### 1. 복구할 파일을 선택하고 우클릭 후 Export File 클릭

<img width="684" height="198" alt="스크린샷 2026-07-13 002111" src="https://github.com/user-attachments/assets/a2d51959-690b-4e5e-9d35-627ba9b62a89" />

#### 2. 저장 경로 선택

<img width="276" height="307" alt="KakaoTalk_Snapshot_20260713_002243" src="https://github.com/user-attachments/assets/d139099e-3ef5-4d55-941b-d74d82df05a6" />

#### 결과 확인

<img width="844" height="552" alt="KakaoTalk_Snapshot_20260713_002351" src="https://github.com/user-attachments/assets/a9385b5c-3b17-4587-a46c-a75e34264162" />

> 실습 노트:
실습에 사용된 USB 드라이브의 경우, 파일 삭제 시 휴지통을 거치지 않고 파일 시스템(FAT32/NTFS) 상에서 메타데이터의 연결 고리가 즉시 끊어지는 영구 삭제 구조를 가집니다. 이로 인해 일반적인 내보내기(Export) 방식으로는 데이터 영역까지 온전히 복구되지 않아 파일 손상이 발생합니다.

이러한 한계를 극복하기 위해, 과거 학습했던 **HxD 헥스 에디터(Hex Editor)**를 활용한 시그니처 분석 및 헥사값 수동 조작 기법이 대안이 될 수 있으며, 해당 세부 기법은 추후 실습을 통해 깊이 있게 다룰 예정입니다.

### Autopsy를 이용하여 복구하기

### 분석파일 불러오기

#### 1. Autopsy 실행 후 New Case 클릭

<img width="391" height="271" alt="KakaoTalk_Snapshot_20260713_003407" src="https://github.com/user-attachments/assets/f6a15aa6-5c90-40a2-bb0c-15cd29d0b8c9" />

#### 2. 케이스 이름과 테이블을 생성할 디렉터리 설정

<img width="605" height="368" alt="KakaoTalk_Snapshot_20260713_003545" src="https://github.com/user-attachments/assets/85f1d088-0c6d-44ec-8933-c07fefd57e41" />

#### 3. 사건의 세부정보를 입력한다.

<img width="601" height="367" alt="KakaoTalk_Snapshot_20260713_003604" src="https://github.com/user-attachments/assets/6f766571-19f5-437d-b488-0b3d4199fbba" />

#### 4. Default 선택을 한다.

<img width="660" height="419" alt="KakaoTalk_Snapshot_20260713_003638" src="https://github.com/user-attachments/assets/611a0bf3-b7bc-4005-a7b1-cc5b074da014" />

#### 5. 불러올 사건 파일의 형식을 선택한다. 이전에 생성한 usb 이미지 파일을 이용할 것이니 Disk Image 선택

<img width="657" height="419" alt="KakaoTalk_Snapshot_20260713_003656" src="https://github.com/user-attachments/assets/f8341361-d723-4a35-a948-b1b3d93ad0b8" />

#### 6. 불러올 파일을 선택하고 시간을 설정한다. 한국에서 실행할 것이므로 Seoul 선택

<img width="656" height="420" alt="KakaoTalk_Snapshot_20260713_003759" src="https://github.com/user-attachments/assets/b304d8e7-6bf8-4ec1-999d-eed912f1e800" />

#### 7. 분석에 이용할 도구 선택하기

<img width="652" height="411" alt="KakaoTalk_Snapshot_20260713_003846" src="https://github.com/user-attachments/assets/968baffd-f25f-43e5-81a0-f20dbde01d09" />

#### 8. 결과 확인

<img width="656" height="416" alt="KakaoTalk_Snapshot_20260713_004036" src="https://github.com/user-attachments/assets/8ce6bc37-459e-480e-b9e5-cacb0effbcf9" />

<img width="943" height="685" alt="KakaoTalk_Snapshot_20260713_004057" src="https://github.com/user-attachments/assets/28c941cf-01d7-4aba-bec6-f9fbb9e67e77" />

### 파일 복구하기

<img width="941" height="690" alt="KakaoTalk_Snapshot_20260713_004307" src="https://github.com/user-attachments/assets/185b3cb8-b713-45b4-88a3-8441d8d98dc3" />

Data Source Tree 하위의 Deleted File 항목이 존재한다. FTK Imager에서와 비슷하게 복구할 파일을 우클릭하고 Extract를 하면 파일이 복구된다.

> 실행 결과

<img width="915" height="648" alt="KakaoTalk_Snapshot_20260713_004358" src="https://github.com/user-attachments/assets/ec3bc9e7-665b-400d-a8af-92e1a064b0b2" />

> FTK Imager에서와 마찬가지로 손상된 파일로 나온다.

### 💡 실습 결과 분석 및 향후 계획

#### [현상 및 문제점]
FTK Imager와 Autopsy 두 도구 모두에서 삭제 표시된 파일의 복구(Export/Extract) 자체는 성공하였으나, 복구된 이미지 파일(`Grogu.jpg`)을 실행하면 **"지원되지 않는 형식이거나 파일이 손상되어 사진을 열 수 없다"**는 오류가 발생합니다.

#### [원인 분석]
이는 파일의 메타데이터(이름, 경로 등) 정보는 파일 시스템에 남아있어 도구상에 노출되었지만, 실제 파일 데이터가 저장되어 있던 클러스터(Cluster) 영역의 링크가 끊어졌거나 이미 다른 데이터가 덮어씌워진(**Overwrite**) 상태이기 때문입니다. 즉, 파일의 껍데기만 복구되고 알맹이(데이터 영역)가 파괴된 포렌식적 전형적인 파일 손상 현상입니다.

#### [향후 계획: 파일 카빙(File Carving) 도입]
위와 같이 파일 시스템의 메타데이터가 손상되었거나 제 기능을 하지 못할 때는, 파일 시스템을 거치지 않고 디스크의 비할당 영역(Unallocated Space)을 직접 스캔하여 파일 고유의 특징적인 바이너리 패턴(헤더 및 푸터 시그니처)을 기준으로 파일을 통째로 이어 붙여 복구하는 **'파일 카빙(File Carving)'** 기법이 필요합니다. 

현재 복구 실패한 파일은 일반적인 내보내기 기능으로는 정상화가 불가능하므로, **추후 별도의 실습을 통해 파일 카빙(시그니처 기반 복구)을 적용하여 원본 이미지 복원을 시도하고 그 결과를 추가로 기록할 예정입니다.**
