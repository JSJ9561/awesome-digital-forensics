# 📂 01. 디지털 포렌식 소개 및 Warm-up

* 과거에 학습한 포렌식 기본 개념 복습 (5대 원칙 등)
* 인프런 강의 섹션 1 (소개) & 섹션 2 (디스크 이미징, 마운트, 삭제 파일 복구) 실습 기록

## 디지털포렌식 개론  

### 디지털포렌식이란?
전자기기의 저장매체 또는 인터넷에 남아 있는 디지털 정보를 분석해 범죄 단서를 찾는 수사기법

### 디지털포렌식의 필요성
과거에는 컴퓨터 범죄(해킹 등)과 관련한 한정적 정보 수집이었으나 최근에는 일반범죄에서도 디지털포렌식을 활용하여 범죄 정보 수집을 한다. 또한 형사사건 외에 민사사건에서도 디지털포렌식을 이용하며 일반기업에서도 내부감사에서도 이용한다.

### 디지털 포렌식의 유형
#### 침해사고 대응
침해사고(예: 해킹)가 발생했을 때 피해를 최소화하기 위해 '실시간'으로 진행되며 이후 '사태 파악 및 수습'을 한다. 사태가 어느 정도 해결되면 시스템을 백업하고 포렌식 절차를 거쳐 시스템 이미지를 획득한다.

#### 증거 추출
획득한 시스템 이미지를 '사후 조사'와 '범죄 증거 수집'을 위해 '법적 절차'를 거쳐 분석한다. 

### 디지털포렌식의 종류
- 시스템 포렌식 
  - 디스크 포렌식: 컴퓨터 디스크(HDD, SSD) -> 윈도우, 리눅스, MacOS/개인, 서버, 클라우드 등의 운영체제 포렌식
  - 메모리 포렌식: 컴퓨터 메모리(RAM)
- 네트워크 포렌식: 네트워크 패킷, 네트워크 장비 로그, 네트워크 관련 설정
- 모바일 포렌식: 모바일 디바이스(저장소, 메모리), IOT 디바이스

## 디스크 이미징과 마운트, 메모리 덤프

### FTK Imager 설치
#### 1. https://www.exterro.com/digital-forensics-software/ftk-imager 공식사이트에 들어가서 Free Download를 클릭합니다.

<img width="806" height="513" alt="KakaoTalk_Snapshot_20260709_215126" src="https://github.com/user-attachments/assets/bee4bf76-5500-4794-8a0d-2de66c6f4f0a" />

#### 2. 표시된 영역의 내용을 작성합니다.(개인 정보 유출이 우려되면 아무 문자나 입력해도 문제가 없습니다. 이메일은 정상적인 이메일이 필요하나 스팸메일주소로 적어넣어도 정상적으로 다운로드됨을 확인했습니다.)

<img width="666" height="626" alt="KakaoTalk_Snapshot_20260709_215240" src="https://github.com/user-attachments/assets/173dd070-5eea-44b0-a7ff-3e25ee894478" />

#### 3. 다운로드 파일 형식은 ISO 파일입니다. 더블클릭을 하여 마운트를 하고 드라이브 내의 exe파일을 실행합니다.

<img width="562" height="25" alt="스크린샷 2026-07-09 214259" src="https://github.com/user-attachments/assets/a4019a39-3c42-4e2b-a77e-17aeb3c124f4" />

<img width="579" height="192" alt="KakaoTalk_Snapshot_20260709_215734" src="https://github.com/user-attachments/assets/ff602f00-f2ac-4193-ad03-9d04510eac9f" />

#### 4. exe 파일을 실행하고 설치경로 화면까지 다음을 누릅니다.

#### 5. 설치 경로는 본인이 편한 곳에 하고 하단의 체크박스에 'Install Bonjour', 'Install Apple mobile device support'는 Windows 이용자면 체크 해제를 합니다. 'Add Installation File Path ~'는 빠른 속도를 위해 체크합니다.

<img width="391" height="297" alt="KakaoTalk_Snapshot_20260709_214942" src="https://github.com/user-attachments/assets/731dab2d-2935-40bf-a416-7a5ede9e9e74" />

#### 6. 설치가 완료되면 마운트된 드라이브를 꺼냅니다. 해당 드라이브에 우클릭을 하고 '꺼내기'를 누릅니다.

<img width="241" height="287" alt="스크린샷 2026-07-09 220205" src="https://github.com/user-attachments/assets/c129321a-b58f-40e4-bed9-740e0677ac8c" />

#### 7. 설치된 FTK Imager를 관리자 실행합니다.

### HxD 설치








