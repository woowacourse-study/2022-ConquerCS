# Index
#### 그게 뭔데?
- Table의 column을 색인화 하여 따로 파일로 저장한다.

#### 왜 쓰는데?
- index를 통해 빠르게 조회를 하기 위한 목적으로 만든다.
- 색인화 된(B+ Tree in MySql innoDB) index를 통해 table의 모든 record를 탐색하지 않는다.

### 과정은?
- Table 생성시 MYD, MYI, FRM 3개의 파일 생성
#### FRM
- Table 구조가 저장된 파일

#### MYD
- 실제 데이터가 있는 파일

#### MYI
- index 정보가 기록된 파일
- index를 사용하지 않을 경우 비워져있다.
- 사용자가 index를 사용하는 column 탐색시 MYI 파일 내용 검색

#### 언제 쓰는데?
- CUD에 비하여 R의 비중이 높은 경우
- 관계로 인해 조회 빈도가 높은 경우
  - Where 절에서 자주 사용되는 culumn
  - 외래키가 사용되는 column
  - Join에 자주 사용되는 column
  
### 단점은?
- index 생성시 .mdb 파일 크기 증가
- 한 페이지 동시 수정 병행성 감소
- CUD 성능 감소

#### 언제 쓰지 않아야 하는데?
- CUD에 의해 자주 변경되는 column
  - Data 중복도가 높은 column
  - DML이 자주 일어나는 column
  
## DML 발생시
### Insert(Create)
- 기존 Block에 여유가 없을 때 새로운 Data 입력
- 새 Block 할당 받은 후 Key를 옮기는 작업 수행
  - 대량의 Redo 발생
- Index split 작업 동안 해당 Block의 Key 값 DML 블로킹되어 대기 발생

### Delete
#### Table
- Data 삭제되어 다른 Data가 공간 사용

#### Index
- Data가 지워지지 않고 사용 불가 상태로 변경
- Table의 Data 수와 Index의 Data 수 다를 수 있음

### Update
- Table에서 update가 발생하면 index는 Update 할 수 없음.

#### Index
# Redis
#### 그게 뭔데?
- HDD나 SSD에 저장하는 일반 DB와 달리 RAM에 저장하여 빠른 엑세스 강점을 갖는 스토어

#### 왜 쓰는데?
- 특정 데이터에 잦은 빈도로 조회 요청이 몰리는 경우 이를 메모리에 캐싱하여 DB와 통신하는 것에 비해 매우 빠르게 처리할 수 있기 때문이다.

#### 언제 쓰는데?
- CUD에 비해 R의 비중이 높고 특정 데이터에 잦은 빈도로 요청이 와서 캐싱의 효용이 높을 때
- 실시간 채팅 등 빠른 읽기 성능을 요구할 때

#### 단점은?
- 영속으로 보관할 데이터가 포함될 경우 휘발성 메모리에 두는 것은 바람직하지 않다.
- 데이터의 만료 기간, 원본과 사본의 일관성 등 적절한 설정의 어려움이 있다.
- 캐싱 서버의 장애에 의해 전체 시스템 동작이 중단될 수 있다.

#### 특징은?
- 데이터 구조는 Key - value 값으로 되어 있다.
- 휘발성 메모리의 한계를 극복하기 위해 백업 과정이 존재한다.

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/Redis.html)
[가상 면접 사례로 배우는 대규모 시스템 설계 기초](http://www.kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788966263158)