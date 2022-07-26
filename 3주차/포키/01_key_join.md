# 키(Key) & 조인(Join)

 

# 키(Key)

검색 또는 정렬 시 tuple을 구분할 수 있게 해주는 속성값

- tuple: 테이블의 한 행(속성들이 모여 이루는 한 줄의 데이터)

 

### Candidate Key(후보키)

기본키가 될 수 있는 속성들

- 유일성: 중복 없이 유일해서 Key만으로도 하나의 Tuple을 식별할 수 있음(unique)
- 최소성: 식별하는데에 꼭 필요한 속성으로만 구성
  - 어느 한 속성이 빠져도 식별 가능하다면 최소성 만족하지 못하는 것

### Primary Key(기본키)

후보키 중 main key로 선택해서 사용되는 속성

- not null, unique

### Alternate Key(대체키)

기본키를 제외한 나머지 후보키

### Super Key

유일성 O, 최소성 X

### Foreign Key

다른 테이블(릴레이션)의 기본키를 참조하는 속성

 

# 조인

둘 이상의 테이블 또는 데이터베이스를 연결해서 조회하는 것

- 적어도 하나의 컬럼을 서로 공유하고 있을 때 이 컬럼을 이용해서 조회

 

## Inner Join

두 테이블 다 중복해서 갖고 있는 값만 보여줌 (교집합)

ex) 상품과 주문을 inner join하면 상품 목록에 존재하면서 주문이 들어온 상품만 볼 수 있다

## Outer Join

어느 한 쪽 테이블에만 있는 값도 보여줌

- ex) 상품 테이블에 대해 주문 테이블을 outer join하면 주문되지 않은 상품이어도 상품 목록에 존재만 한다면 볼 수 있다

### Left Outer Join

왼쪽 테이블에 있는 값 기준

- ex) 상품 left outer join 주문

### Right Outer Join

오른쪽 테이블에 있는 값 기준

- ex) 주문 right outer join 상품

### Full Outer Join

양쪽에 존재하는 모든 데이터 검색 (합집합)

## Cross Join

모든 경우의 수 표현 (두 테이블 데이터 수의 곱 만큼 데이터가 검색됨)

## Self Join

자기 자신을 join

- 하나의 테이블을 여러 Alias를 통해 복사해서 join


