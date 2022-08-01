# Transaction
### 그게 뭔가?
특성상 하나의 성공/실패로 취급되어야 하는 여러 동작을 하나의 단위로 묶은 개념

### 왜 쓰는가?
데이터를 올바르게 보장하기 위해서이다. 데이터를 올바르게 보장하기 위해서는 `동시 실행 제어`와 `크래시 복구`가 필수이다.

#### 동시 실행 제어가 뭔가?
> 트랜잭션에 포함된 개별 조작에 주목하고 어떻게 스케줄을 짜면 데이터를 정확하게 보장하여 동시에 수정할 수 있을까?

실용 서비스는 동시 접속으로 인한 병렬화가 필수이다. 따라서 얼마나 직렬화 되어 데이터를 안전하게 수정할 것인지, 얼마나 병렬화를 하여 성능을 높일 것인지 두 사이에서 적절한 스케줄링을 통해 최적점을 찾아야 한다. RDB에서는 주로 잠금 스케줄러 로직을 사용하여 테이블 혹은 Row(tuple) 단위로 데이터를 locking 하여 동시 실행을 제어한다. 

- 데이터의 정확성이란?
  - 병렬 트랜잭션이 개별 트랜잭션을 한 개씩 차례로 실행할 때(직렬 트랜잭션)와 같은 결과가 될 때 병렬화의 데이터 정확성이 보장되었다고 한다. 
  
#### 크래시 복구가 뭔가?
데이터를 올바르게 보장하기 위해서는 의도하지 않은 데이터 수정이나 과정 중 오류가 발생했을 경우(크래시 발생) 데이터를 원상태로 복구해야 한다. DB는 이를 트랜잭션 RollBack을 통해 구현한다. 

### 특징은?
트랜잭션의 특징을 말할 때 주로 `ACID`를 많이 거론한다. 핵심은 `A(Atomicity)`이다. 
#### A(Atomicity, 원자성)
- 트랜잭션에 포함된 모든 작업이 성공(Commit) 또는 실패(Abort, SQL에서는 Rollback)하는 성질
#### C(Consistency, 일관성)
- 트랜잭션 실시 전후 데이터 일관성이 손상되지 않아야 한다. 
  - 주로 `데이터의 중복`, `테이블간 관계 업데이트 오류`로 인해 일관성이 훼손된다.
#### I(Isolation, 격리성)
- 동시에 실행하는 여러 개의 트랜잭션이 서로 영향을 주지 않는 성질
- 개별 트랜잭션의 동시 실행 결과는 트랜잭션을 직렬로 실행했을 떄와 결과가 같아야 한다.

#### D(Durability, 영속성)
- 커밋이 완료된 트랜잭션이 손상되지 않는 성질
- 확정된(Commit) 트랜잭션이 취소 불가하다.
- 시스템이 크래시 나도 복원 가능해야 한다.

## DB Transaction
DBMS의 구조(Architecture)는 어떠하며 어떻게 Transaction을 구현하는가? 여기서는 주로 MySQL의 InnoDB를 중심으로 정리한다. 

### DB Architecture
DBMS는 크게 Query Engine, Storage Engine으로 구성된다. 
Query Engine은 요청된 쿼리를 파싱하여 파서 트리를 만들고, 이를 최적화하여 Storage Engine에 그 처리를 요청한다. 
Storage Engine은 Query Engine의 요청에 따라 데이터를 디스크로 저장하고 디스크로부터 읽어온다.

### Buffer Pool
Storage Engine의 핵심 부분으로, 디스크의 데이터 파일이나 인덱스 정보를 메모리에 캐시해준다. 쓰기 작업을 지연시켜 일괄 작업으로 처리할 수 있게 해주는 버퍼 역할도 한다. 

### MVCC(Multi Version Concurrency Control)
일반적으로 레코드 레벨의 트랜잭션을 지원하는 DBMS가 제공하는 기능이다. MVCC의 가장 큰 목적은 잠금을 사용하지 않는 일관된 읽기를 제공하는 데 있다(낙관적 락). Multi Version의 의미는 하나의 레코드에 대해 여러 개의 버전이 동시에 관리된다는 의미이다. Undo log를 이용해 이 기능을 구현한다. 

### Undo log
Storage Engine은 트랜잭션과 격리 수준을 보장하기 위해 DML로 변경되기 이전 데이터를 Undo log로 백업한다. 

#### 왜 쓰는가?
- 트랜잭션 보장
  - Undo log에 백업해둔 이전 버전의 데이터를 이용하여 복구한다.
- 격리 수준 보장
  - 특정 커넥션에서 데이터를 변경하는 도중에 다른 커넥션에서 데이터를 조회하면 트랜잭션 격리 수준에 맞게 변경중인 레코드를 읽지 않고 Undo log에 백업해둔 데이터를 읽어서 반환할 수 있다.
  
### Redo log
Redo log는 ACID 중 D(Durability)에 해당하는 영속성과 가장 밀접하게 연관한다. Redo log는 서버가 비정상적으로 종료됐을 때 기록되지 못한 데이터를 잃지 않게 해주는 안전창지다. 

# 참고
[관계형 데이터베이스 실전 입문](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791158390372&orderClick=LAG&Kc=)
[Real MySQL 8.0](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=2909101309302&orderClick=LAG&Kc=)
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/data-base/Transaction.html)