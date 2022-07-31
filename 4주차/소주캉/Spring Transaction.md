# Spring Transaction
#### Declarative Transaction
Spring은 광범위하게 Annotation을 적용하여 Declarative(선언적) 프로그래밍을 가능하게 한다. 이는 Transaction에도 마찬가지이다. 스프링을 사용하는 우리는 객체 내부에 Transaction과 관련된 부가 기능 코드를 더할 필요 없이 Annotation만을 달아주면 Transaction을 사용할 수 있다. 이렇게 공통되지만 객체의 핵심 관심사가 아닌 코드(횡단 관심사, Aspect)를 분리하여 적용할 수 있게 한 것이 AOP(Aspect Oriented Programming)이다. Spring의 Transaction은 AOP를 활용한 기술로 볼 수 있다. 

### AOP
위와 같이 AOP는 여러 객체에 필요하지만 핵심 관심사가 아닌 코드를 횡단 관심사(Aspect)로 간주하여 이를 객체에서 분리하여 다른 차원에서 관리하도록 하는 패턴이다. Sprng에서 사용할 수 있는 AOP 구현 방법은 두 가지가 있다. 

#### Spring Transaction 
Proxy Pattern과 Decorator Pattern을 이용해서 구현한다. 즉 부가 기능을 더할 목적 클래스(Target)을 직접 호출하는 것이 아니라, Proxy를 호출하고 Proxy에 의해 Target을 호출하게 한다. 이 과정에서 Proxy가 부가 기능을 Target의 메서드를 호출하며 부가 기능을 더해준다. 
![](https://velog.velcdn.com/images/sojukang/post/4fb5b2ac-1356-49b0-9112-a800560bf207/image.png)


#### AspectJ
Proxy를 사용하는 것이 아니라, 부가 기능을 더할 목적 클래스의 코드에 직접 코드를 집어 넣어(Weaving) 구현한다. Compile 과정에서 수행할 경우 Compile Time Weaving, Compile 후 생성된 Bytecode를 대상으로 Loading 과정에서 수행할 경우 Load time Weaving이라고 한다. 

## Spring @Transactional Option
### Propagation
트랜잭션의 전파 속성을 정의한다. 
#### REQUIRED
![](https://velog.velcdn.com/images/sojukang/post/a5707231-1bcf-49b7-8d74-07c1829adc0e/image.png)

스프링의 기본 전파 속성이다. 부모 트랜잭션에서 자식 트랜잭션이 발생할 경우 부모 트랜잭션에 포함된다. 트랜잭션이 없으면 새로 생성한다. 자식 트랜잭션에서 RollBack이 일어났을 때 `UnExpectedRollbackException`이 발생하여 부모 트랜잭션이 이 `RuntimeException`을 통해 Rollback이 발생한다. 

#### REQUIRES_NEW
![](https://velog.velcdn.com/images/sojukang/post/7e94fe6a-d581-4221-8639-0af10a65d904/image.png)

부모 트랜잭션에서 자식 트랜잭션이 발생할 경우 자식 트랜잭션이 종료되면 다시 부모 트랜잭션으로 돌아온다. 자식 트랜잭션은 독립적으로 동작하여 RollBack이 일어나도 부모 트랜잭션은 계속 진행한다. 

#### NESTED
자식 트랜잭션이 부모 트랜잭션에 포함된다. 하지만 자식 트랜잭션이 독립적인 RollBack 포인트를 가지게 되어 RollBack이 일어나도 부모 트랜잭션은 영향 없이 진행한다. 

### Isolation
Propagation 속성이 `REQUIRED`, `REQUIRED_NEW`일 때만 적용된다. 

#### DEFAULT
데이터 저장 계층에 기본적으로 지정된 격리 수준을 사용한다. 

#### READ_COMMITTED
Dirty Read, Non-Repeatable Read, Phantom Read가 일어날 수 있는 격리 수준이다.

#### READ_UNCOMMITTED
Non-Repeatable Read, Phantom Read가 일어날 수 있는 격리 수준이다. 

#### REPEATABLE_READ
Phantom Read가 일어날 수 있는 격리 수준이다. 

#### SERIALIZABLE
모든 Anormal Read를 방지하지만 병렬 처리가 불가능하다.

### ReadOnly
Propagation 속성이 `REQUIRED`, `REQUIRED_NEW`일 때만 적용된다. 
트랜잭션에 `readOnly=true` 옵션을 주면 Hibernate Session flush 모드를 `MANUAL`로 설정하여 강제로 플러시를 호출하지 않는 한 플러시가 일어나지 않는다. 따라서 트랜잭션이 Commit 되어도 영속성 컨텍스트가 플러시되지 않고, 읽기 전용으로 영속성 컨텍스트는 변경 감지를 위한 스냅샷을 보관하지 않으므로 성능이 향상된다. 

### rolebackFor
RollBack이 일어날 예외를 정의한다. Spring의 기본 RoleBack 정책은 Uncheck Exception이기 때문에 Checked Exception에 대해서도 RollBack하기 위해서는 rolebackFor옵션으로 CheckedException을 지정해주어야 한다. 

# 참고
[Spring docs transaction](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#spring-data-tier)
[Spring docs isolation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/Isolation.html)
[[JPA]@Transaction(readOnly=ture) 성능 향상 이유?](https://willseungh0.tistory.com/75)
