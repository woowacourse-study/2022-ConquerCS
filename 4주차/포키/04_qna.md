# 예상 질문

### Q. 트랜잭션 격리 수준을 Read Committed로 두었을 때 발생할 수 있는 부정합에 대해 설명해주세요.

- NON-REPEATABLE READ가 발생할 수 있습니다. NON-REPEATABLE READ란 한 트랜잭션이 실행되는 동안 다른 트랜잭션이 해당 트랜잭션에서 조회해야 하는 데이터에 대해 수정하고 commit했다면, 한 트랜잭션 내에서 같은 select 쿼리에 대해 다른 조회 결과가 나오는 현상입니다.

### Q. Spring Transaction의 read-only 속성은 어떨 때 사용하나요?

- 조회만 하는 트랜잭션에 대해 성능 최적화를 해주거나, 해당 트랜잭션에서 데이터에 대한 쓰기 작업이 일어나는 것을 막을 떄 사용합니다. read-only로 설정된 트랜잭션 범위 내에서 쓰기 작업이 일어날 경우 exception이 발생하기 때문에 이를 이용할 수 있습니다.


