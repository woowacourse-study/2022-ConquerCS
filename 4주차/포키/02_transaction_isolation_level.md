# Transaction Isolation Level

> 트랜잭션에서 일관성 없는 데이터를 얼마나 허용할 지

## 격리수준을 왜 조정해야 할까?

트랜잭션 보장을 위해 무조건 Locking → 수 많은 트랜잭션을 순서대로만 처리하게 되어 성능 저하

성능을 위해 Locking 범위 축소 → 잘못된 값이 처리될 수 있음

> 결론: “적당히” 격리시켜야 한다

---



## Isolation Level 종류

### Read Uncommitted

- 아직 commit되지 않은 데이터도 읽을 수 있다
  - → `Dirty Read` 부정합 발생
- `Dirty Read`: 아직 완료되지 않은 transaction에 의한 변경 사항이 조회되는 것

### Read Committed

- 오라클 default, 온라인 서비스에서 가장 많이 선택
- commit된 데이터만 읽을 수 있다
  - → `NON-REPEATABLE READ` 부정합 발생
- `NON-REPEATABLE READ`: A라는 transaction을 실행하는 동안 B라는 transcation에서 데이터를 변경해서 commit을 했다면, 같은 A transaction 내에서 같은 select query를 두 번 날렸을 때 다른 결과가 조회된다

### Repeatable Read

- MySQL InnoDB의 default
- 같은 트랜잭션 내에서는 조회 결과가 항상 동일하다
  - commit이 일어났을 때, 변경되기 전의 record를 Undo 영역에 백업한 후 실제 record를 변경 (`MVCC`)
  - 모든 트랜잭션은 순차적으로 증가하는 고유번호를 가지며, Undo 영역의 백업 데이터는 변경을 발생시킨 트랜잭션의 번호 포함
  - 이를 이용해 데이터 조회 시 자신보다 후에 일어난 데이터 변경은 반영하지 않음 → 항상 같은 조회 결과 보장
- `PHANTOM READ` 발생할 수 있으나, InnoDB에서는 발생하지 않음 → 굳이 Serializable 선택하지 않는 이유
  - `PHANTOM READ`: 트랜잭션 도중 다른 트랜잭션에서 새로운 row를 추가했을 때, 같은 select query를 두 번 날렸을 때 그 전에 없던 row가 함께 조회되는 것

### Serializable

- 다른 트랜잭션에서 읽거나 쓰는 record는 절대 접근 불가
- 가장 엄격하지만, 그만큼 동시성이 떨어져 성능이 현저히 떨어짐


