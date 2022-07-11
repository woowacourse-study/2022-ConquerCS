# UDP
## 무엇인가?
- UDP(User Datagram Protocol): OSI 분류상 4계층(Transport Layer)으로 데이터를 데이터그램 단위로 처리하는 프로토콜이다.
- 비연결형, 신뢰성 없는 전송 프로토콜이다.
  - 비연결형: 연결을 유지하는 과정이 없다.
  - 비신뢰성: 데이터의 순서, 정확성 등 무결성을 보장하지 않는다.
 
## 왜 쓰는가?
- 데이터의 처리가 TCP보다 현저히 빠르면서도 IP 목적지를 정확하게 찾아갈 수 있다.
- 실시간 스트리밍이나 회의에서 사용한다.

## UDP Header에 담기는 내용은?
- Source Port: 시작 포트
- Destination Port: 도착지 포트
- Length: 길이
- Checksum: 오류 검출
  - 중복 검사의 한 형태로, 오류 정정을 통해 송신된 자료의 무결성을 보호한다.
  
## DNS에서 UDP를 사용하는 이유?
DNS query는 single UDP request와 server의 single UDP reply로 구성된다.
- DNS Request의 양이 작으므로 UDP Request에 담을 수 있다.
  - DNS Request는 UDP segment에 들어갈 정도로 작다.
- 3 way handshaking으로 연결을 생성, 유지할 필요가 없다.
  - Protocol overhead가 TCP에 비해 작다.
- Reliability는 Application Layer에서 timeout이나 resend 작업을 통해 보강할 수 있다.

### DNS 서버간 요청
- Zone transfer(DNS 서버간 요청)인 경우 데이터의 크기가 512bytes를 넘거나 통신의 정확성이 중요하여 TCP를 사용하는 경우가 있다.
