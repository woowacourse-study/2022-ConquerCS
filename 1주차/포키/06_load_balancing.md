# 로드밸런싱

### 

### reference

- [라운드 로빈 스케줄링 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/%EB%9D%BC%EC%9A%B4%EB%93%9C_%EB%A1%9C%EB%B9%88_%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81)
- [L4의 부하 분산 방법 (tistory.com)](https://ktdsoss.tistory.com/440)
- [로드 밸런싱에 대해 알아보자! (techcourse.co.kr)](https://tecoble.techcourse.co.kr/post/2021-11-07-load-balancing/)

### 등장 배경

- 웹사이트 접속 인원의 증가로 1대의 서버가 트래픽을 감당할 수 없음
- 하드웨어 업그레이드(Scale-up) → 비쌈, 한 대 다운되면 타격이 크다
- 여러대의 서버(Scale-out) → 무중단 서비스 제공 환경 구성이 용이(효과적)
  - 여러 서버에게 트래픽 분산시키는 것이 `로드 밸런싱`

## 

## 로드 밸런싱?

- 분산식 웹 서비스
- 여러 서버에 부하(Load)를 나누어줌(Balancing)
  - 클라이언트 - Load Balancer - 서버
- 사이트 규모에 따라 서버 증설하면서 부하 해결

### 

### 서버를 선택하는 방식

- Round Robin: CPU 스케줄링의 Round Robin 방식 차용
  - 요청을 순서대로 돌아가며 배정
  - 모든 서버의 연결 세션 갯수가 거의 비슷
  - 서버들의 스펙이 비슷하고 세션 지속이 짧을 때 적합
- Least Connections: 연결 개수(Active Connection)를 기준으로 가장 적은 서버 선택
  - 모든 서버의 Active 연결 세션 갯수가 거의 비슷
  - 세션 지속이 길거나 트래픽 분배가 일정하지 않을 때 적합
- Source(Hashing, IP Hash): 사용자 IP 기준 분배 → 한 사용자는 같은 서버로 연결되도록
  - 세션 유지가 가능하나 서버간 연결 갯수에 불균형 발생

### 장애 대비

- Load Balancer 역시 문제가 생길 수 있음 → Load Balancer도 이중화
  - Active / Passive

---

### 예상질문

- Q. 서버 트래픽 과부화에 대처하는 방법에는 어떤 것이 있을까요?
  - A. 하드웨어 성능을 업그레이드 하는 Scale-up 방식과, 서버를 증설하는 Scale-out 방식이 있습니다. Scale-up은 비용이 많이 들며 한 대의 서버가 다운되면 서비스 자체가 중단된다는 위험성이 있지만, Scale-out 방식은 한 대가 다운되어도 서비스가 중단되지 않아 효과적입니다.
- Q. Load Balancing 방법 중 Round Robin 방식은 어떨 때 적합할까요?
  - A. Round Robin 방식은 요청 순서대로 돌아가며 서버에 배정하기 때문에 모든 서버의 스펙이 동일하거나 비슷한 경우에 적합합니다.

 
