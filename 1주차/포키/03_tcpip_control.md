# TCP/IP 흐름제어 & 혼잡제어

### 

### TCP란?

- 전송 제어 프로토콜(Transmission Control Protocol)
- 패킷 전달 여부와 순서를 보장하지 않는 IP 위에서 동작
  - 안정적으로, 순서대로, 에러없이 교환할 수 있게
  - unreliable → reliable

### 전송 전체 과정

- sender application (data) → socket
- transport layer (data with segment) → network layer → receiving node
  - sender는 send buffer에, receiver는 receive buffer에 data 저장
- application에서 준비 되면 buffer에 있는 것 읽기 시작
- receiver buffer가 넘치지 않게 하는 것이 흐름제어의 핵심
  - RWND(Receive WiNDow): receive buffer의 남은 공간 홍보

## 

## 흐름제어

- sender - receiver 측 속도 차이 해결
- receiver가 받는 packet 양 조절 (Flow Control)
- receiver → sender 상태 feedback

### 

### 방법

- Stop and Wait: 매 패킷 전송 마다 확인 응답 받은 후에만 다음 패킷 전송
- Sliding Window: 수신 측에서 확인 응답 없이 송신할 수 있는 세그먼트 크기(윈도우 크기) 설정 → 데이터 흐름 동적 조절
  - 마지막에 보낸 byte - 마지막으로 확인한 byte = 윈도우 크기(남은 공간)
  - Window: TCP/IP를 사용하는 모든 호스트들이 2개씩 가지고 있음(송신용, 수신용)
  - 먼저 윈도우 내 패킷 전송 후 ACK받으면 받은 ACK 수 만큼 옆으로 옮기면서 다음 패킷 전송

## 

## 혼잡제어

- 데이터가 몰려들어 발생하는 네트워크 혼잡을 피하기 위해 데이터 전송 속도 조절
- 흐름제어는 sender ↔ receiver 전송 속도를 다루는 것, 혼잡제어는 호스트, 라우터 포함 보다 넓은 관점의 문제를 다룬다

### 방법

#### AIMD(Additive Increase / Multiplicative Decrease)

- 방식
  - 패킷 하나 보내고 문제 없으면 송신 window 1씩 증가시켜가며 전송
  - 전송 실패하거나 일정 시간 초과 시 패킷 보내는 속도 절반으로 줄임
- 특징
  - 여러 호스트가 한 네트워크에 진입 시, 처음에는 불공평해도 점점 평형 상태로 수렴하게 됨 (공평)
- 단점
  - 초기에 네트워크를 충분히 활용 못해 시간이 오래 걸림
  - 소 잃고 외양간 (혼잡해진 후에야 대처)

#### Slow Start

- 시작은 AIMD와 같고, 문제 없으면 ACK 패킷마다 window size 1씩 증가
  - 전송 속도 지수 함수 꼴로 증가
- 혼잡 발생 시
  - 처음에는 window size 1로 감소
  - 한 번 혼잡 발생 후 네트워크 수용량 어느정도 예상 → 혼잡 발생한 size의 절반까지는 지수 함수 꼴로 증가, 그 이후 완만하게 1씩 증가

#### Fast Retransmit

- 기존 혼잡조절에 추가된 정책
- 먼저 왔어야 할 패킷이 오지 않고 다음 패킷이 와도 ACK 패킷 전송
- 순서대로 도착한 마지막 패킷의 다음 순번을 ACK에 포함해서 전송 → 송신 측에서 손실을 감지하고 해당 패킷 재전송 해줄 수 있음
  - 중복 순번 3개 받으면 재전송 (약간 혼잡) → 혼잡 감지, window size 감소

#### Fast Recovery

- 혼잡 시 window size 1이 아닌 반으로 감소 → 선형 증가
- 혼잡 한 번 겪고 나면 순수 AIMD 방식으로 동작하게 됨

---

### 예상질문

- Q. Fast Retransmit 정책은 순번이 섞이게 되는데 어떻게 데이터 손실을 막아주나요?
  - A. 순서대로 잘 도착한 마지막 패킷의 다음 순번을 ACK에 포함해서 전송하기 때문에, 송신자 측에서 어떤 데이터가 갔어야 하는지 손실을 감지하고 재전송해줄 수 있습니다.
- Q. 흐름제어는 어느 계층에서 일어나나요?
  - A. OSI 7계층 중 4번째 계층인 전송계층에서 일어납니다.

 
