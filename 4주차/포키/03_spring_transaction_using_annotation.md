# Spring Transaction Using Annotation

> Spring의 `@Transactional` 설정 시 사용할 수 있는 attributes

References

- 토비의 스프링 3.1

## propagation(트랜잭션 전파)

> Spring의 선언적 트랜잭션에서는 각각의 모듈로 분리된 로직들, 그리고 그 각각의 트랜잭션 적용 범위를 묶어서 커다란 트랜잭션 경계를 만들 수 있다

`propagation={Propagation Enum}`

- `REQUIRED`(default)
  - 먼저 시작된 transaction이 있으면 참여, 없으면 새로 시작
  - transactional이 설정된 method A에서 또 다른 transactional 메소드 B를 호출했을 때, A의 트랜잭션 범위 내에 B의 로직이 포함되어 같은 트랜잭션으로 묶임
- `SUPPORTS`
  - 먼저 시작된 transaction이 있으면 참여, 없으면 transaction 없이 실행
- `MANDATORY`
  - 먼저 시작된 transaction이 있으면 참여, 없으면 예외 발생
  - 독립적으로 transaction 범위를 가질 수 없는 경우 사용
- `REQUIRES_NEW`
  - 항상 새로운 transaction 시작
  - 먼저 시작된 transaction 있다면 보류시킴
- `NOT_SUPPORTED`
  - transaction 사용 X
  - 먼저 시작된 transaction 있다면 보류시킴
- `NEVER`
  - transaction 사용 X
  - 먼저 시작된 transaction 있다면 예외 발생
- `NESTED`
  - 먼저 시작된 transaction 있으면 그 안에 또 다른 transaction 생성 (`중첩 트랜잭션`)
  - 부모 transaction의 commit과 rollback에는 영향 받지만 자신의 commit과 rollback은 부모에게 영향 X
  - ex) 로깅 작업을 중첩 트랜잭션으로 설정 → 메인 로직에 문제 발생 시 로그 삭제, 로그 작성 로직에 문제 발생 시 메인 로직은 문제없이 마무리

## isolation(격리 레벨)

`isolation={Isolation Enum}`

- `DEFAULT`
  - 사용중인 DB의 default 격리 레벨을 따름
- `READ_UNCOMMITTED`
- `READ_COMMITTED`
- `REPETABLE_READ`
- `SERIALIZABLE`

## timeout(제한 시간)

> transaction 제한 시간 지정(초 단위)

`timeout={int}`

- 기본값: transaction 시스템 따름

## readOnly(읽기 전용)

> 성능 최적화 및 해당 transaction 내부의 데이터 수정 방지 위해 설정

`readOnly={boolean}`

- 기본값: false
- true일 떄 해당 transaction 안에서 쓰기 작업 일어나면 예외 발생

## rollbackFor, rollbackForClassName(롤백 예외)

> 원래는 unchecked exception에 대해 rollback하지만, 특정 checked exception에 대해서도 rollback하고 싶을 때

`rollbackFor={Class<? extends Throwable>}`

`rollbackForClassName={String(예외 class 이름)}`

- 배열 형태로 여러개 설정할 수 있음

## noRollbackFor, noRollbackForClassName(커밋 예외)

> 원래는 rollback 대상인 unchecked exception중 특정 exception은 제외하고 싶을 때

`noRollbackFor={Class<? extends Throwable>}`

`noRollbackForClassName={String(예외 class 이름)}`

- 배열 형태로 여러개 설정할 수 있음


