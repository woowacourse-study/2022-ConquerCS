# 로드 밸런싱
# 무엇인가?
둘 이상의 서버(자원)에 요청(작업)을 나누는 것

# 왜 쓰는가?
## 문제
- 하나의 자원만 존재할 경우 문제 발생하면 전체 시스템에 장애가 생긴다
- 자원의 성능을 높이는 scale-up의 경우 성능에 따라 증가의 효과가 감소하는 수확체감이 발생한다.

# 해결
- Load Balancer를 클라이언트와 서버 사이에 두고 여러 서버에 부하를 나눈다. 
  - scale-out: 서버의 성능이 아니라 개수를 늘려 더 많은 트래픽을 처리할 수 있는 확장.
- 주로 OSI 7 Layer의 7 계층의 Load Balancer, 4 계층의 Load Balancer가 쓰인다.

## 알고리즘 
- 라운드 로빈(Round Robin, RR): 일정 시간마다 부하를 처리할 서버를 바꿔가며 분산한다.
- Least Connections: 커넥션 개수가 가장 작은 서버를 우선 선택한다. 트래픽으로 인해 세션이 길어지는 경우 권장한다.
- Hashing: 사용자 IP를 해싱하여 분배한다. 특정 사용자가 항상 같은 서버로 연결되는 것을 보장한다.

## Load Balancer 장애 대비
- Load Balancer 자체에도 장애가 발생할 수 있기 때문에 이중화 혹은 여러 계층에 도입하여 대비한다. 

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/network/OSI%207%EA%B3%84%EC%B8%B5.html)
[IT 엔지니어를 위한 네트워크 입문](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791165213183)
