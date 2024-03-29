# 이상(Anomaly) & 정규화(Normalization)

 

# 이상(Anomaly)

> 만약 상품, 주문, 회원 정보가 모두 한 테이블로 관리된다면?

### 삽입 이상(Insertion Anomaly)

불필요한 데이터를 추가해야 삽입할 수 있는 상황

- 기본키가 회원ID + 주문ID인 경우, 주문 한 적 없는 회원은 주문ID가 없음
- 기본키는 null일 수 없으므로 Table에 추가하려면 ‘주문없음’과 같은 불필요한 데이터로 ID를 채워야 한다

### 갱신 이상(Update Anomaly)

일부만 변경되어 데이터가 불일치하는 모순의 문제

- 만약 어떤 회원의 회원 등급을 변경해야 한다면, 해당 회원과 관련있는 모든 row의 등급 column 값을 수정해야 한다
- 혹시나 일부를 깜빡하여 바꾸지 않는다면 데이터에 모순이 발생

### 삭제 이상(Deletion Anomaly)

튜플 삭제로 인해 꼭 필요한 데이터까지 함께 삭제되는 문제

- 만약 한 회원이 주문을 모조리 취소한다면, 꼭 필요한 해당 회원의 회원정보까지 삭제해야 한다

 

# 정규화(Normalization)

> 중복된 데이터를 없애서 무결성 유지하며 용량을 효율적으로 관리

## 제 1정규화(1NF)

column이 원자값(분해할 수 없는 하나의 값)을 갖도록 테이블 분리

- 릴레이션에 속한 모든 도메인이 원자값만으로 이루어져야 함
- 모든 속성에 반복되는 그룹이 나타나지 않음
- 기본키로 각 데이터 집합을 고유하게 식별할 수 있어야

## 제 2정규화(2NF)

모든 column이 완전 함수적 종속 만족

- 상품ID와 주문ID의 복합키를 기본키로 갖고 있을 때, 상품명은 상품ID만으로 결정할 수 있음 → 부분 함수적 종속
- 이럴 경우 상품 테이블과 주문 테이블을 분리하여 완전 함수적 종속(2NF)을 만족시켜줄 수 있음

## 제 3정규화

2NF까지 진행된 테이블에서 이행적 종속을 없애는 것

- 기본키가 아닌 속성들은 기본키에 의해 결정되어야 함
  - 기본키 → 속성 → 또 다른 속성 과 같은 형태로 결정된다면 이행적 종속 (A→B, B→C, A→C)
- 주문ID를 기본키로 가지고 있고 고객ID와 고객명을 속성으로 가질 때, 고객ID는 주문ID를 보고 알 수 있지만 고객명은 고객ID만으로 결정되는 정보 → 이행적 종속
- 주문 테이블과 고객 테이블 분리해야 함

 
