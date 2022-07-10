# UDP



## TCP와 UDP

### 

### reference

- [사용자 데이터그램 프로토콜 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
- [[프로토콜] UDP Header / UDP 동작 (tistory.com)](https://joycecoder.tistory.com/20)
- [도메인 네임 시스템 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)



### 등장 배경

- IP는 장치 ↔ 장치만 해결, 하나의 장치에서 다수의 통신을 할 경우에는 한계가 있음 → Port로 해결
- 오류 발생 시 IP 상위에서 대처해주어야 함 → 상위 프로토콜인 TCP와 UDP 등장

### 

### UDP?

- User Datagram Protocol
  - 데이터를 데이터그램(단문) 단위로 처리
  - Transport Layer에서 사용하는 프로토콜 중 하나
    
    

### TCP vs UDP

- TCP
  - 양단 간 연결 먼저 설정 후 양방향 전송
  - 메세지 수신 여부, 순서 보장
- UDP
  - 연결 설정 X, 수신자 준비 여부 확인 X, 단방향 전송
  - 수신자가 메시지 수신 했는지 확인할 수 X
    - 메시지 도착 순서 역시 예측할 수 X
    - 오류가 생긴 경우 Application에서 처리해야 함
  - TCP에 비해 속도가 빠르고 오버헤드 적음
    - 실시간 방송, 온라인 게임 등 끊기지 않아야 할 때 주로 사용
    - 🧠: 속도가 최우선되어야 할 때는 UDP를 사용하나보다



## UDP Header

- Source Port: 송신자가 사용하는 Port 번호
- Destination Port: 수신자가 사용하는 Port 번호
- Length: 헤더 + 데이터 합한 사용자 데이터그램의 전체 길이
- Checksum: 헤더 + 데이터 합한 사용자 데이터그램 전체에 대한 오류 검출

## 

## DNS의 UDP 프로토콜 사용

### DNS?

- Domian Name System
- 도메인 이름 ↔ 네트워크 주소 변환 수행
- 53번 port에서 UDP 사용

### 왜 unreliable한 UDP를 사용하는가?

- 연결 유지할 필요 X
  - 연결 유지를 보장하기 위해 거치는 handshaking 과정은 overhead가 크다
- DNS request는 양이 작아 UDP Request에 담김
  - 메세지 크기가 512byte(UDP 제한)를 넘을 경우엔 TCP 사용 (DNS 서버 간 Zone transfer 사용 시)
- Request 손실을 Application Layer에서 처리해줄 수 있음
  - Timeout 추가, resend 작업 등
- 🧠: DNS는 데이터가 간단해서 불안정하지만 빠른 UDP를 사용해도 괜찮나보다




