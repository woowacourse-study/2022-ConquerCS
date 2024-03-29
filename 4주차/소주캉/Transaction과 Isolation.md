# Transaction 격리(Isolation)
#### 격리(Isolation)이란?
데이터에 동시에 접근할 경우 비정상 상태(Anomaly)가 일어날 수 있으므로 조회/수정 중인 데이터에 접근을 막는 것

#### 격리가 필요한 이유
모든 사용자의 요청을 하나씩 처리하면(직렬화) 데이터의 일관성이 보장되어 격리를 할 이유가 없다. 그러나 실용 서비스는 성능을 위해 동시에 여러 사용자의 요청을 처리하는 병렬화가 필수이다. 따라서 여러 병렬 트랜잭션 처리와 동시에 직렬 처리의 결과와 같은 데이터 일관성을 보장하기 위해서는 격리 수준을 통해 병렬성의 정도를 지정할 필요가 있다. 

## 비정상 상태(Anormaly)
Read 측면에서의 비정상 상태를 설명한다. 각 격리 수준은 이 3가지 비정상 상태에 대응 여부가 다르다. 
### Dirty Read
어떤 트랜잭션에서 처리한 작업이 완료되지 않았는데도 다른 트랜잭션에서 볼 수 있는 현상

### Non-Repeatable Read
트랜잭션 내에서 조회의 결과가 다른 트랜잭션의 결과에 의해 달라질 수 있는 현상

### Phantom Read
트랜잭션 내에서 조회의 결과에 이전에 없었던 데이터가 등장하는 현상

## 격리 수준(Isolation Level)
### Read Uncommitted
각 트랜잭션의 변경 내용이 Commit이나 RollBack 여부에 상관 없이 다른 트랜잭션에서 보인다.

#### Anormaly
- Dirty Read: 다른 트랜잭션이 변경중인 데이터를 조회 가능하다. 
- Non-Repeatable Read: Dirty Read인 경우 Non-Repeatable Read이다.
- Phantom Read: Non-Repeatable Read인 경우 Phantom Read가 가능하다.

### Read Committed
어떤 트랜잭션에서 데이터를 변경해도 Commit이 완료된 데이터만 다른 트랜잭션에서 조회할 수 있다. 

#### Anormaly
- Non-Repeatable Read: 한 트랜잭션이 Commit전 다른 트랜잭션에서 조회한 결과와 Commit 후 조회한 결과가 달라질 수 있다.
- Phantom Read: Non-Repeatable Read인 경우 Phantom Read가 가능하다.

### Repeatable Read
어떤 트랜잭션내의 조회의 결과가 같음(Time invariant)을 보장한다. MySQL InnoDB의 기본 격리 수준이다. 

#### InnoDB
InnoDB Storage Engine은 트랜잭션이 RollBack될 가능성에 대비해 변경되기 전 레코드를 Undo log 공간에 백업해두고 실제 레코드 값을 변경한다. Repeatable Read 격리 수준에서는 Undo log에 기록된 데이터를 조회하여 Repeatable Read를 보장한다. 

#### Anormaly
- Phantom Read: 트랜잭션 도중 데이터가 추가되는 경우 Phantom Read가 가능하다(InnoDB에서는 보장한다).

### Serializable
읽기 작업도 공유 잠금을 획득하기 때문에 현재 조회/수정 중인 모든 레코드에 잠금이 걸려서 다른 트랜잭션에서 접근할 수 없다. 

# 참고
[관계형 데이터베이스 실전 입문](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158390372&orderClick=LAG&Kc=)
[Real MySQL 8.0](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=2909101309302&orderClick=LAG&Kc=)
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/Transaction.html)
