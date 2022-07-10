# OSI 7계층

### 

### reference

- [OSI 7 계층 - 해시넷 (hash.kr)](http://wiki.hash.kr/index.php/OSI_7_%EA%B3%84%EC%B8%B5)
- [OSI 모형 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95)

### 7계층을 나누는 이유

네트워킹 시스템에서 문제가 생겼을 때, 계층 개념을 통해 시각적으로 쉽게 설명 → 빠르게 문제 범위를 좁혀서 찾고 대응

실제로 계층이 구분되어 있는것이 아니라 개념 모델

- 🧠: 오 이게 약간 java web app에서 layered architecture를 만드는 그런 느낌인갑다..

## 7계층 구조

- 🧠: 1~7까지 네트워크에 필요한 최소 장비부터 차근차근 준비물을 세팅한다는 느낌

### 

### **1. 물리(Physical)**

> 리피터, 케이블, 허브, 네트워크 어댑터 등

- 단위: Bit
- 프로토콜: 10BASE-T, 100BASE-TX, ISDN, wired, wireless, RS-232, DSL, Twinax
- 디지털 ↔ 아날로그 신호 변환
- 🧠: 데이터를 디지털 신호로 전송하는데 필요한 최소한의 물리적 환경

### 

### **2. 데이터 링크(Data Link)**

> MAC 주소, 브릿지, 스위치 등

- 단위: Frame
- 프로토콜: Ethernet, Token Ring, AppleTalk, PPP, ATM, MAC, HDLC, FDDI, LLC, ALOHA
- 1홉 통신 담당
  - 홉(hop): 네트워크에서 노드에서 다음 노드로 가는 경로
  - 1홉: 라우터 → 라우터 딱 한 번
- 물리 전송에 대한 관리
  - 각 장치끼리 식별할 수 있는 주소 체계 제공
  - Point To Point 간 신뢰도 보장 위해 에러 검출, 흐름 제어

### 

### **3. 네트워크(Network)**

> 라우터, IP

- 단위: Packet
- 프로토콜: IP, IPX, IPsec, ICMP, ARP, NetBEUI, RIP, BGP, DDP, PLP
- 2홉 이상의 통신 (멀티 홉 통신)
- 실제 네트워크 간 데이터 라우팅 담당 (주소 부여 + 경로 설정)
  - 라우팅: 데이터를 최대한 빠르게 보낼 최적의 경로를 선택하는 것
- 최적 경로 선택 → 논리 주소(IP) 지정 → Packet 전달
- 라우팅, 흐름 제어, 세그멘테이션, 오류 제어 등
- 🧠: 이거 약간 Dispatcher Servlet…? Controller…?

### 

### **4. 전송(Transport)**

> TCP, UDP, 특정 방화벽 및 프록시 서버

- 단위: TCP-Segment, UDP-datagram
  - TCP : 신뢰성, 연결지향적
  - UDP : 비신뢰성, 비연결성, 실시간
- 프로토콜: TCP, UDP, SPX, SCTP, NetBEUI, RTP, ATP, NBP, AEP, OSPF
- 송신자 → 수신자 연결하는 통신 서비스 제공
  - 하위 계층에 신뢰할 수 있는 데이터 전송 서비스 제공
  - End-to-End를 다루는 최하위 계층
- 시퀀스 넘버 기반의 오류 제어
- 🧠: 네트워크 계층이 길을 찾아 주면 전송 계층이 데이터 배달

### 

### **5. 세션(Session)**

> API, Socket

- 단위: Data
- 프로토콜: NetBIOS, SAP, SDP, PIPO, SSL, TLS, NWLink, ASP, ADSP, ZIP, DLC
- TCP/IP 세션 관리
  - 만들고 없애는 책임
- 호스트가 갑자기 중지되지 않도록 정상 연결 관리
  - 통신하는 사용자들 동기화
  - 오류 복구 명령 일괄적 처리
- 🧠: 하위 계층에서 만들어진 통신에 대한 논리적 관리

### 

### **6. 표현(Presentation)**

> 인코딩, 디코딩, 암호화, 복호화

- 단위: Data
- 프로토콜: ASCII, MPEG, JPEG, MIDI, EBCDIC, XDR, AFP, PAP
- 응용 계층과 주고받는 데이터의 인코딩, 디코딩
- 안전한 데이터 사용을 위한 암호화, 복호화
- 🧠: MVC로 치면 데이터를 view로 전달하기 위한 전처리 과정

### 

### **7. 응용(Application)**

> 텔넷(Telnet), 구글 크롬, 이메일, 데이터베이스 관리 등

- 단위: Data
- 프로토콜: HTTP, SMTP, SSH, FTP, Telnet, DNS, modbus, SIP, AFP, APPC, MAP
- 사용자에게 자원 접근 제공
  - 사용자가 볼 수 있는 유일한 계층
  - 네트워크 활동의 기반 인터페이스 제공
- 사용자가 실행하는 응용 프로그램들

---

### 예상질문

- Q. 브라우저가 속하는 OSI 계층과 그 계층의 특징을 설명해주세요.
  - A. 브라우저는 최상단 계층인 응용계층에 속합니다. 응용계층은 사용자가 볼 수 있는 유일한 계층으로, 인터페이스를 통해 사용자가 네트워크 자원에 접근할 수 있도록 하는 계층입니다.
- Q. 네트워크 계층은 어떤 책임이 있나요?
  - A. 데이터를 보낼 가장 빠른 경로를 설정하는 라우팅을 담당하며, 논리 주소인 IP를 부여합니다.

 
