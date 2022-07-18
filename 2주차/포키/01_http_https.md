# HTTP & HTTPS



# HTTPS(****HyperText Transfer Protocol Secure****)

> HTTP의 암호화된 버전



### reference

- [https에 대해서 | Kyun2da.dev](https://kyun2da.dev/CS/https%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C/)

- HTTP는 데이터를 평문 텍스트로 주고받음 → 조작, 탈취 위험성 → 암호화로 해결

- SSL 또는 TLS 등의 암호화 프로토콜을 통해 텍스트 암호화



## CA(Certificate Authority)

> 공개키 저장, 신뢰도 검증을 해주는 민간 기업

HTTP: HTTP ↔ TCP (직접 통신)

HTTPS: HTTPS ↔ SSL ↔ TCP (SSL 거쳐 통신)

- SSL은 공개키 방식 사용
- 수신한 공개키가 정말 본래의 서버가 발행한 공개키인지 알 수 없다 → 인증기관(CA)을 두어 보완
1. 서버 운영자 → CA에 공개키 등록
2. CA → 서버의 공개키가 담긴 인증서 만들고, CA의 비밀키로 암호화하여 서버에 제공
3. 서버 → HTTPS가 아닌 요청을 보낸 클라이언트에 CA가 작성해준 공개키 인증서 전송
4. 브라우저는 이를 해독 → 얻은 서버의 공개키 암호로 통신
   - 세계적으로 신뢰할 수 있는 CA기업의 공개키는 등록되어있기 때문에 브라우저가 알 수 있음
5. 클라이언트는 CA의 공개키를 통해 서버의 공개키가 인증되었으며 신뢰할 수 있음을 알 수 있다



---

### 

### 예상 질문

- Q. HTTPS는 왜 등장했나요?
  - A. HTTP는 데이터를 암호화 되지 않은 텍스트로 주고받아 탈취의 위험이 있습니다. 이를 방지하기 위해 HTTP에 SSL 또는 TLS와 같은 보안 프로토콜을 더해서 데이터를 암호화하는 프로토콜이 바로 HTTPS입니다.


