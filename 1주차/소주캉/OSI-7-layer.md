# OSI 7 Layer
# 무엇인가?
![OSI 7 layer](https://velog.velcdn.com/images/sojukang/post/7764cb43-5935-4c9b-b295-01fc47c7ce63/image.png)

OSI(Open Systems Interconnection): 네트워크 통신을 7개의 계층으로 나눈 모델.

# 왜 쓰는가?
네트워크 통신의 각 관심사를 나누어 파악하기 위해. 각 계층을 추상화하여 개념을 파악하기 쉽게 한다.

# 각 계층 상세 
Application ~ Session 계층까지를 Application Layer(상위 계층),
Transport ~ Physical 계층까지를 Data flow Layer(하위 계층)으로 나누기도 한다.
계층의 구분은 데이터를 만드는 어플리케이션 부분과 이 데이터를 전달하는 하부 계층으로 구분하는 게 목적이다.
## Application Layer
### Application(7)
#### 특징
- 사용자 입, 출력 부분을 정의

#### 프로토콜
- HTTP, SMP, SMTP

### Presentation(6)
#### 특징
- 다른 어플리케이션이나 시스템간의 통신을 돕기 위해 통일된 형식으로 변환

#### 프로토콜
- TLS, SSH

### Session(5)
#### 특징
- 양 끝단의 응용 프로세스 연결, 유지, 종료

#### 프로토콜
- L2TP, PPTP, NFS

## Data Flow Layer
### Transport(4)
#### 목적
- 실제로 데이터들이 정상적으로 잘 보내지도록 확인

#### 특징
- 패킷이 유실되면 재전송을 요청할 수 있다.
  - `패킷이란?` 하나의 통신이 회선 전체를 점유하지 않고 동시에 여러 단말이 통신하도록 데이터를 쪼갠 단위.
- 순서가 바뀌었을 때 바로잡아준다.
- port 번호를 통해 상위 어플리케이션을 구분한다.

#### 프로토콜
- TCP: 신뢰성, 연결지향적
- UDP: 비신뢰성, 비연결성, 실시간

#### 주요 장비 
port 번호와 sequence number, ACK number 를 이용해 부하를 분산하거나 보안 정책을 수립해 패킷을 통과, 차단하는 기능 수행

- Load Blancer
- Fire Wall

### Network(3)
#### 목적
- 논리적인 주소 정보를 정의하고 통신이 되도록 하는데 초점

#### 특징
- IP 주소는 네트워크 주소와 호스트 주소 부분으로 나뉨

#### 프로토콜
- ARP, IPv4, IPv6, NAT

#### 주요 장비
- Router: IP 주소를 사용해 최적 경로를 찾아 패킷 전송

### Datalink(2)
#### 목적
- 실제 물리적 주소 정보를 정의하고 정확한 주소로 통신이 되도록 하는데 초점

#### 특징
- 전기 신호를 모아 특정 데이터 형태로 처리 
- 데이터에 관한 에러 탐지, 고침
- 이더넷 기반 네트워크에서는 에러 탐지 역할 수행
- MAC 주소를 기반으로 통신

#### 주요 장비
- NIC(Network Interface Card, Lan Card)
- Switch

### Phisical(1)
#### 목적
- 들어온 전기 신호를 잘 전달

#### 특징
- 물리적 연결과 관련된 정보 정의
- 주로 전기 신호 전달

#### 주요 장비
- Hub, Repeater: 네트워크 통신을 중재
- Cable, Connector: 케이블 본체를 구성
- Tranceiver: 랜 카드와 케이블 연결
- TAP: Network monitoring과 Packet 분석을 위해 전기 신호를 다른 장비로 복제


# TCP/IP와 차이는?
다소 개념적인 OSI 7 계층에 비하여 실제 쓰이는 프로토콜별로 나누어 현실에 쉽게 대응된다.
OSI 7 계층은 참조형 모델이고 실제로 사용하는 프로토콜은 TCP/IP 프로토콜 스택으로 구현된다.