# TLS/SSL HandShake
HTTPS 통신 과정에서는 송신자와 수신자가 암호화 통신을 하기 위한 대칭키 공유가 필요하다. 이때 대칭키를 타인에게 노출시키지 않고 Client가 Server에게 전송하기 위한 방법이 존재하는데 그것이 바로 TLS/SSL HandShake이다.

![Untitled](img/tls,ssl%20handshake.png)

1. ***ClientHello(암호화 알고리즘 나열 및 전달)***: 클라이언트가 서버에 연결을 시도하며 전송하는 패킷이다. 자신이 사용가능한 Cyper Suite 목록, SessionID, SSL 프로토콜 버전, Random Byte등을 전달한다. Cipher Suite는 SSL 프로토콜 버전, 인증서 검정, 데이터 암호화 프로토콜, Hash 방식 등의 정보를 담고 있는 존재로, 선택된 Cipher Suite의 알고리즘에 따라 데이터를 암호화하게 된다.
2. ***ServerHello(암호화 알고리즘 선택)***: ******서버는 클라이언트가 보낸 ClientHello 패킷을 받아 CyperSuite 중 하나를 선택한 후 자신의 SSL 프로토콜 버전 등과 함께 다음 클라이언트에게 보낸다.

   > ClientHello에서 보낸 Cyper Suite는 여러개이지만 ServerHello에서는 서버가 한개만을 선택하여 보내기에 1개의 CyperSuite가 들어있다.
>
3. ***Server Certificate(인증서 전달)***: Server는 자신의 Server가 발행한 공개키가 들어있는 SSL인증서를 클라이언트에게 전달한다. 클라이언트는 서버가 보낸 CA의 개인키로 암호화된 SSL인증서를 CA에 등록되어있는 공개키를 사용해 복호화한다. 복호화에 성공하면 인증서는 CA가 서명한 것이 맞으니 유효성 검증이 되는 것이다.
    1. ***Server Key Exchange / ServerHello Done*: ****서버의 공개키가 SSL 인증서 내부에 없는 경우 서버가 직접 전달하겠다는 뜻으로 공개키가 SSL 인증서 내부에 있을 경우 Server KeyExchange 과정은 생략된다.

       인증서 내부에 서버의 공개키가 있다면 클라이언트가 CA의 공개키를 통해 인증서를 복호화한 후 서버의 공개키를 확보할 수 있다. 그리고 서버가 작업을 마쳤다고 ServerHelloDone을 전달한다.

4. *****Client Key Exchange(데이터를 암호화 할 대칭키 전달)*****: 클라이언트는 데이터 암호화에 사용할 대칭키를 생성한 후 SSL 인증서 내부에서 추출한 서버의 공개키를 이용하여 암호화한 후 서버에 전달한다. 전달된 대칭키가 SSL Handshaking의 목적이자, 추후 데이터를 암호화할 대칭키이다.
5. ***Client/Server Hello Done(정보 전달 완료)***
6. *****ChangeCipherSpec/ Finished***** : ChangeCiperSpec 패킷은 클라이언트와 서버 모두가 서로에게 보내는 패킷으로 교환할 정보를 모두 교환한 뒤 통신할 준비가 다 되었음을 알리는 패킷이다. 그 후 finish 패킷을 보내어 SSL handshake를 종료한다.

# 질문

- SSL Handshake란?
- Handshake과정을 설명해보세요

[[네트워크] TLS & SSL Handshake](https://steady-coding.tistory.com/512)
