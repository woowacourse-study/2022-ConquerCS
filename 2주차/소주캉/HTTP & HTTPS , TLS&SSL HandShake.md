# HTTP
## 무엇인가?
- HTTP(Hyper Text Transfer Protocol)은 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약이다.
- OSI 7 계층의 7계층인 Application Layer에 해당하는 통신 규약이다.

## 왜 쓰는가?
- `simple` 매우 간단하여 다양한 환경에서 통신 프로토콜로 범용적으로 사용 가능하다.
- `extensible` 클라이언트 - 서버간의 동의만 있다면 새로운 기능 확장이 쉽다.

## 특징은?
- 전통적인 클라이언트 - 서버 모델을 따른다
  - 1. 클라이언트가 커넥션을 얻고 요청을 보낸다.
  - 2. 서버로부터 응답이 올 때까지 대기한다.
- 무상태성(stateless) 프로토콜이다.
  - 상태에 의존적이지 않기 때문에 이전 요청/응답과 이후의 요청/응답은 무관하다.
  
# HTTPS
## 무엇인가?
`HTTPS`는 `HTTP`에 `SSL(TLS)`를 추가한 것이다.

## 왜 쓰는가?
## HTTP의 한계
`HTTP`에는 3가지 문제점이 있다. 

1. 평문(암호화 하지 않은) 통신이기 때문에 도청이 가능하다.
2. 통신 상대를 확인하지 않기 때문에 위장이 가능하다. 
3. 완전성을 증명할 수 없기 때문에 변조가 가능하다. 

각각의 문제점을 자세히 알아보자. 

---

### 1. 평문(암호화 하지 않은) 통신이기 때문에 도청이 가능하다.
`HTTP` 를 사용한 요청과 응답은 암호화 기능이 없기 때문에 평문으로 전송된다. 어떤 해결책이 있을까?

#### 통신 암호화
`SSL(Secure Socket Layer)`나 `TLS(Transport Layer Security)`를 `HTTP`에 조합하여 통신 내용을 암호화 할 수 있다. `SSL`을 조합한 `HTTP`를 `HTTPS(HTTP Secure)`이라 부른다. `TLS`는 `SSL`이 표준화되면서 바뀐 이름이다. 동일하게 취급해도 괜찮다. 자세한 내용은 후의 `HTTPS` 에서 다룬다. 

#### 콘텐츠 암호화
콘텐츠 자체를 암호화 하여 암호회된 엔티티를 전송하는 방법이 있다. 이 방법을 위해서는 클라이언트 <-> 서버 간 암호화, 복호화 규약이 있어야한다. 평상시 브라우저와 웹 서버간 이용은 어렵고, 합의된 특정 서비스에서 사용된다. 

### 2. 통신 상대를 확인하지 않기 때문에 위장이 가능하다. 
`HTTP`는 누구든지 요청을 보내면 응답하는 심플한 구조이다. 따라서 상대를 확인하지 않는 약점이 있다. 

#### 증명서(Certificate)
`SSL`은 암호화 뿐만 아니라 상태를 확인하는 수단으로 증명서를 제공하고 있다. 

증명서는 신뢰할 수 있는 제3자 기관(CA: Certificate Authority)에 의해 발행된다. 통신 상대인 서버나 클라이언트가 가진 증명서를 확인하여 내가 통신하고자 하는 상대인지 아닌지를 판단할 수 있다. 

![인증서 1](https://velog.velcdn.com/images/sojukang/post/b491154f-c01d-46d5-b4d7-621f02f7fd43/image.png)
![인증서 2](https://velog.velcdn.com/images/sojukang/post/a10739c5-37ea-48ff-ae6b-4dd5b8853e01/image.png)

#### 증명서 발급 과정
1. 애플리케이션 서버(A)를 만드는 기업은 HTTPS를 적용하기 위해 공개키와 개인키를 만든다.
2. 신뢰할 수 있는 CA 기업을 선택하고, 그 기업에게 `내 공개키` 관리를 부탁하며 계약을 한다.
> CA란? : Certificate Authority로, 공개키를 저장해주는 신뢰성이 검증된 민간기업
3. CA 기업은 해당 기업의 이름, `A서버 공개키`, 공개키 암호화 방법을 담은 인증서를 만들고, 해당 인증서를 _CA 기업의 개인키_ 로 암호화해서 A서버에게 제공한다.
4. 클라이언트가 main.html 파일을 달라고 A서버에 요청했다고 가정하자. HTTPS 요청이 아니기 때문에 클라이언트는 CA기업이 A서버의 정보를 _CA 기업의 개인키_ 로 암호화한 인증서를 받게 된다.
> 주요 CA 기업의 공개키는 브라우저가 이미 알고있다.
5. 브라우저는 해독한 뒤 `A서버의 공개키`를 얻게 되었다. 이제 A서버와 통신할 때는 얻은 `A서버의 공개키`로 암호화해서 요청을 날리게 된다.

### 3. 완전성을 증명할 수 없기 때문에 변조가 가능하다.
완전성이란 정보의 정확성을 가리킨다. 전송한 내용이 도중에 변조되었을 수도 있다. 이를 방지하기 위해 MD5, SHA-1 등의 해시 값을 확인하는 방법이 있고, 파일의 디지털 서명을 확인하는 방법이 있다. 후자의 방법으로 `SSL`을 사용한다. 

---

위 세 가지 문제점을 각각 `도청, 위장, 변조` 문제점이라 한다.
이상 `HTTP`의 한계를 해결하기 위해 `HTTPS`가 등장한다. `HTTPS`는 `HTTP`의 `도청, 위장, 변조` 문제를 어떻게 해결했을까? 

## HTTP + 암호화 + 인증 + 완전성 보호 = HTTPS
`HTTPS`는 `HTTP`에 `SSL(TLS)`를 추가한 것이다. 이를 통해 앞서 말한 3가지 문제, `도청, 위장, 변조` 문제를 해결한다. `HTTPS`를 사용하면 `HTTP`와 `TCP/IP`간의 새로운 계층인 `SSL`이 추가되어 보다 안전한 통신이 가능하다.

<div align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/1258X489_How-SSL-Certificates-Work.jpg/800px-1258X489_How-SSL-Certificates-Work.jpg" width="100%" height="60%">
  
<a href="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/1258X489_How-SSL-Certificates-Work.jpg/800px-1258X489_How-SSL-Certificates-Work.jpg">SSL</a>
</div>

`SSL(TLS)`의 과정은 다음과 같다. 

---

1. Browser connects to a web server (website) secured with SSL (https). Browser requests that the server identify itself. 
브라우저는 웹 서버와 SSL 연결을 시도한다. 브라우저는 서버에게 서버의 식별을 요청한다.

2. Server sends a copy of its SSL Certificate, including the server’s public key.
서버는 공개키와 함께 가지고 있는 SSL 인증의 복사본을 전송한다.

3. Browser checks the certificate root against a list of trusted CAs and that the certificate is unexpired, unrevoked, and that its common name is valid for the website that it is connecting to. If the browser trusts the certificate, it creates, encrypts, and sends back a symmetric session key using the server’s public key.
브라우저는 받은 인증서를 브라우저가 저장한 인증기관에서 받은 리스트에서 유효성을 검증한다. 인증서가 검증에 통과한 경우 서버의 공개키를 이용해서 암호화한 대칭 세션 키를 만들어 서버로 전송한다. 
4. Server decrypts the symmetric session key using its private key and sends back an acknowledgement encrypted with the session key to start the encrypted session.
서버는 받은 대칭 세션 키를 비밀키를 이용하여 복호화한다. 그리고 암호화된 세션 키를 응답하며 암호화된 세션을 시작한다. 

5. Server and Browser now encrypt all transmitted data with the session key.
서버와 브라우저는 암호화된 세션 키를 이용해 통신한다.

---

#### SSL의 특징
1. 기본 포트는 `443`이다.
2. 통신 데이터가 암호화되어, 패킷이 탈취되는 사고가 발생해도 데이터를 지킬 수 있다. 
3. SSL 인증서를 통해 도메인의 신뢰성을 검증할 수 있다. 
4. 데이터 송/수신 과정에서 암/복호화가 발생하므로 속도가 느리다. 


### 정리
정리하면, `SSL`이 제공하는 암호화, 인증서를 통해 `도청, 위장, 변조` 문제를 해결한다.

# 참고
[MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/network/HTTP%20&%20HTTPS.html)
[What is SSL?](https://www.digicert.com/what-is-an-ssl-certificate)