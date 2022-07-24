# Key
#### 그게 뭐야?
Relation에서 tuple을 구분할 수 있는 기준이 되는 attribute

## Candidate Key(후보 키)
#### 그게 뭐야?
- Tuple을 유일하게 식별하기 위해 사용하는 attribute들의 부분 집합
- PK로 사용할 수 있는 attribute

#### 어떤 키가 후보키가 돼?
2가지 조건을 만족한다.
- 유일성: key로 하나의 tuple을 유일하게 식별할 수 있다.
- 최소성: tuple을 유일하게 식별할 수 있는 최소한의 속성으로만 구성된다.

#### 특징은?
- Null이 될 수 없다. Null은 어떤 것도 특정할 수 없다. 
- 동일한 값이 중복될 수 없다. Relation은 집합이며 집합의 원소(의 식별값)는 중복될 수 없다. 

### Primary Key(기본 키)
#### 그게 뭐야?
- 후보 키중 선택한 Main key

### Altenatate Key(대체 키)
#### 그게 뭐야?
- 후보 키 중 PK를 제외한 나머지 키(보조 키)

## Super Key(슈퍼 키)
#### 그게 뭐야?
- 유일성은 만족하지만 최소성은 만족하지 못하는 키 
- 하나의 attribute으로는 tuple을 특정하지 못하나 다수의 attribute으로 tuple을 특정하는 key로 기능할 때

## Foreign Key(외래 키)
#### 그게 뭐야?
- 다른 Relation의 PK를 참조하는 attribute의 집합

#### 왜 쓰는데?
- 데이터를 각 Relation이 가져야 할 속성들을 만족하도록 여러 Relation에 나누어 저장하고, 이 Relation들에 관계를 부여하여 데이터를 나타내기 위해

#### Relation의 성질
- 어떤 요소가 Relation에 포함돼 있는지 명확하게 판정할 수 있어야 한다(Null로는 어떤 것도 판정할 수 없다).
- Relation의 요소는 중복일 수 없다.

# Join
#### 그게 뭐야?
- 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법
- 테이블을 연결하기 위해 테이블이 공통으로 가지는 column이 필요하다.

#### 왜 쓰는데?
- RDB에 저장되는 데이터는 하나의 Relation으로 전부 저장되는 게 아니라 Relation이 지켜야 할 속성들을 만족하는 여러 개의 Relation으로 저장된다. 따라서 여러 Relation 사이의 데이터를 조합하여 하나의 총체적인 데이터를 구성할 필요가 생긴다. 이 때 필요한 게 Relation의 교집합에 대응하는 table의 Join이다. 

## Inner Join
- Relation의 교집합에 해당하는 연산으로, 기준 테이블과 Join 하는 테이블의 중복된 column 값이 존재하는 tuple을 반환한다.

## Outer Join 
- Join 과정에서 어느 한쪽에만 존재하는 column의 값을 다루기 위해 존재한다.

### Left Outer Join
- 기준 테이블과 Join 테이블의 중복된 column 값이 존재하는 기준 테이블의 tuple을 반환한다.

### Right Outer Join
- 기준 테이블과 Join 테이블의 중복된 column 값이 존재하는 Join 테이블의 tuple을 반환한다.

### Full Outer Join
- Relation의 합집합에 해당하는 연산으로, 기준 테이블과 Join 테이블의 중복되는 column 값이 존재하는 tuple을 반환하며, 두 테이블에 존재하는 모든 column 값을 반환한다.

## Cross Join
- 곱집합(Cartesian Product)에 해당하는 연산으로, 두 테이블의 모든 경우의 수(Combination)를 반환한다.

## Self Join
- 하나의 물리적인 테이블을 2개의 가상 테이블 처럼 다루어 Cross Join한다.
- 테이블의 속성을 여러 조합으로 활용할 경우 사용한다.

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/Join.html)
[[MYSQL] SELF JOIN 예제](https://link2me.tistory.com/958)
[SQL 첫걸음](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9788968482311)
[관계형 데이터베이스 실전 입문](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158390372&orderClick=LAG&Kc=)