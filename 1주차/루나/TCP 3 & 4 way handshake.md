## 3 way handshake - 연결 성립

TCP/IP 통신 기법 중 하나로, TCP/IP 프로토콜을 이용하여 통신하기 전에 **정확한 전송을 보장하고자 연결이 잘 되어있는지 확인하는 것이다. 보통 데이터 송수신 시작 전에 이루어진다.**

![https://blog.kakaocdn.net/dn/dEpulC/btqNCeXP61K/wIrjJKueQOp3kNtAJKW33K/img.png](https://blog.kakaocdn.net/dn/dEpulC/btqNCeXP61K/wIrjJKueQOp3kNtAJKW33K/img.png)

1. **클라이언트가 서버에게 접속요청을 위한 SYN 패킷을 보낸다.** 클라이언트는 SYN을 보낸 후 SYN/ACK 응답을 기다리는 SYN-SENT 상태가 된다.
2. **서버가 Listen 상태일 경우에 SYN을 수신**받는다. 이후 요청수락인 **ACK와 SYN flag 패킷을 보낸다.** 이 때, 서버는 SYN-RECEIVED 상태가 된다.
3. **클라이언트는 ACK를 서버에게 보내고** 이 이후부터는 연결상태로 되어 데이터를 송수신합니다.

## 4 way handshake - 연결 해제

TCP 3-Way HandShake 와는 반대로 **데이터 송수신이 끝나고, 클라이언트와 서버 간 연결을 종료하기 위해 수행**하는 것

![https://blog.kakaocdn.net/dn/bucFJ5/btqNEeQklG0/lduxKDpt68NaJRuPU3ZwSK/img.png](https://blog.kakaocdn.net/dn/bucFJ5/btqNEeQklG0/lduxKDpt68NaJRuPU3ZwSK/img.png)

1. **클라이언트가 서버에게 FIN Flag를 전송한**다. 클라이언트가 전송하고나서 FIN-WAIT 상태가 된다.
2. 서버가 FIN Flag를 받고, **클라이언트에게 ACK를 보낸다.** 이 때, 서버는 CLOSE_WAIT 상태가 된다.
3. 클라이언트는 다음 FIN Flag를 받기 전까지 TIME-OUT 상태가 되고, 남은 데이터를 받으며 종료 준비를 한다.
4. **서버는 이제 연결종료의 의미인 FIN Flag를 클라이언트에게 전송한다**.
5. 클라이언트는 이를 받고 **ACK 메세지를 서버에 전송한다**
6. 서버는 이러한 ACK 메세지를 받고 CLOSED 한다.

### 질문

- TCP의 연결 설정 과정(3단계)과 연결 종료 과정(4단계)이 단계가 차이나는 이유?
    - Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메시지를 보내기
      때문이다.

  [관련 자료](https://ddooooki.tistory.com/21)