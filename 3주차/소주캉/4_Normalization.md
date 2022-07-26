# 정규화(Normalization)
#### 그게 뭔데?
- 데이터의 중복을 줄이고, 무결성을 향상시키는 테이블 설계 전략

#### 왜 필요해?
- 데이터의 중복을 없앤다.
- 무결성을 지키고, 이상(Anomaly) 현상을 방지한다.
- 테이블 구성을 논리적이고 직관적으로 할 수 있다.
- DB 구조 확장에 용이해진다.

## 이상(Anomaly)
#### 그게 뭔데?
- 잘못된 테이블 설계로 인해 Relation의 논리적 정합성에 문제가 생기는 경우
- 중복, Null값 존재 등 

### 삽입 이상(Insertion Anomaly)
#### 그게 뭔데?
- 불필요한 데이터를 추가해야지 삽입할 수 있는 상황
- 두 개 이상의 키를 PK로 지정할 경우 오직 하나의 키 값만 존재할 경우 나머지 키를 Null로 둘 수 없으므로(PK이므로) 불필요한 데이터를 추가해야 PK의 조건을 만족한다. 

### 갱신 이상(Update Anomaly)
#### 그게 뭔데?
- 관련된 데이터의 일부만 변경하여 데이터가 논리적으로 불일치하는 문제
- A 테이블의 값을 변경했을 때 같은 Column을 가지는 B테이블의 정보도 변경되어야하나 되지 않았을 때

### 삭제 이상(Deletion Anomaly)
#### 그게 뭔데?
- Row 삭제로 인해 삭제되면 안되는 다른 데이터까지 삭제되는 문제

## 제1 정규화(1NF: 1st Normal Form)
#### 그게 뭔데?
- 테이블의 column이 하나의 값을 갖도록 테이블을 분리한다.

#### 조건이 뭐야?
- 어떤 Relation에 속한 모든 도메인(attribute)이 하나의 값(원자값)만으로 되어 있어야 한다.
- 모든 attribute에 반복이 나타나지 않는다.
- PK를 사용하여 tuple을 고유하게 식별할 수 있어야 한다.


## 제2 정규화(2NF)
#### 그게 뭔데?
- 테이블의 모든 culumn이 완전 함수적 종속을 만족하는 정규화
- PK의 부분 집합 키가 결정자가 되어선 안된다(테이블의 PK가 복합키로 묶여있을 때, 두 키중 하나의 키만으로 다른 column을 결정지을 수 있으면(부분 함수 종속인 경우) 안된다)

### 함수 종속(Functional Dependency)
- 어떤 Relation R이 있고, 부분집합 두 개를 A, B라 하자. R에 속한 임의의 원소에 대하여 A에 속하면서 B의 값도 같은 경우가 있을 수 있다. 이 경우에 한해서 B는 A에 함수 종속한다고 하고, 이러한 관계성을 A -> B라고 기술한다. 즉, A의 값을 알면 B의 값을 알 수 있는 경우이다. 

#### 부분 함수 종속(Partial Functional Dependency)
- 위의 A의 부분집합 A'에 대하여 A' -> B로 함수 종속할 경우 A -> B의 관계는 부분 함수 종속이라고 한다. 

## 제3 정규화(3NF)
#### 그게 뭔데?
- 2NF를 만족하는 테이블에서 이행적 종속을 없애기 위해 테이블을 분리하는 것
- PK가 아닌 Key에 종속하는 attribute을 PK에 의존하도록 변경한다. 

#### 이행적 함수 종속(Transitive Functional Dependency)
- A -> B 관계를 만족하는 A, B에 관하여 B -> C 일때 A -> C를 만족하는 경우 이행적 함수 종속이라고 한다. 

### 조건이 뭐야?
- Relation이 2NF를 만족한다.
- PK가 아닌 attribute들은 PK에 의존한다.

# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/Normalization.html)
[함수 종속성(완전 함수 종속, 부분함수 종속, 이행함수 종속)의 개념](https://developer111.tistory.com/80)
[Differentiate between Partial Dependency and Fully Functional Dependency](https://www.geeksforgeeks.org/differentiate-between-partial-dependency-and-fully-functional-dependency/#:~:text=Partial%20Functional%20Dependency%20%3A,%2C%20and%20D%2D%3EB.)
[Transitive Dependency in DBMS](https://byjus.com/gate/transitive-dependency-in-dbms-notes/#:~:text=FAQs-,What%20is%20Transitive%20Dependency%20in%20DBMS%3F,must%20eliminate%20the%20Transitive%20Dependency.)
[관계형 데이터베이스 실전 입문](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158390372&orderClick=LAG&Kc=)