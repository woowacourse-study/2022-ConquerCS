# 경쟁 상태

## 경쟁 상태

- 여러 프로세스가 공유자원에 접근할 때 프로세스의 실행 순서에 따라 결과값이 달라짐으로써 data inconsistency가 발생할 수 있는 상황
    - data consistency : 데이터 일관성
- 발생하는 경우 예시
    - 커널 작업 수행 중 인터럽트 발생
        - 커널모드에서 데이터를 불러 작업을 수행하다가 인터럽트가 발생하여 해당 데이터를 다시 조작하는 경우
        - 커널모드인 경우 인터럽트가 발생하지 않도록 disable 하여 해결할 수 있다.
    - 프로세스가 system call을 통해 커널 작업을 하던 도중 context switch 발생
        - 프로세스가 system call을 통해 커널 작업을 하게된다면 context switch가 일어나지 않도록하여 해결할 수 있다.
    - 멀티프로세스 환경에서 공유메모리 접근
        - 접근할 때 마다 해당 데이터를 lock/unlock하여 동시접근이 불가하게 함으로써 해결할 수 있다.

## The Critical-Section Problem ( 임계 구역 문제 )

- Critical-Section : 공유 자원을 접근하는 코드 영역
- The Critical-Section Problem : critial section에 두 개 이상의 프로세스가 접근함으로써 데이터 일관성이 보장되지 않을 수 있는 문제 상황

## The Critical-Section Problem을 해결하기 위한 3가지 요구 조건

- 상호 배제 ( Mutual Exclusion )
    - 한 프로세스가 critial section에 진입하면 다른 프로세스는 critical section에 진입하지 않는다.
- 진행 ( Progress )
    - critial section에 진입하려는 다른 프로세스가 없다면 대기 없이 바로 진입할 수 있어야 한다.
- 한정된 대기 ( Bounded Waiting )
    - 상호 배제를 통해 진입하지 못한 프로세스도 언젠간은 진입할 수 있도록 보장되어야 한다.
    - 진입을 위해 무한히 기다리지 않아야 한다!

## The Critical-Section Problem 해결 방법

- Semaphore ( 세마포어 )
    - 군대에서 사용하는 수신호 라는 뜻
    - P와 V라는 두가지 동작을 통해 공유자원을 보호한다.
    - critial section에 접근하지 못하는 경우 대기줄(list)에 추가되는데, 이는 대부분 큐로 구현되어 있다.

  < P >

    - acquire의 의미
    - value값을 감소시키며 value값이 0보다 작으면 critial section에 어떤 프로세스가 접근해있음을 뜻한다. 따라서 현재 프로세스는 접근이 블가능함을 알 수 있다.
    - 현재 프로세스를 list에 추가한 뒤 block함으로써 대기줄에 자신을 추가한다.

  < V >

    - release의 의미
    - value값을 증가시키며 value값이 0보다 작거나 같으면 진입 대기중엔 프로세스가 존재함을 뜻한다.
    - list에서 하나를 꺼내어 수행될 수 있도록 한다.


- Mutex ( 상호배제 )
    - Mutual Exclusion의 줄임말
    - lock을 가진 프로세스만이 공유자원에 접근하고, 작업이 끝났다면 unlock 하여 lock을 반환한다.
    - 하나의 자원에 대해서만 적용할 수 있다.
    - 데커(Dekker) 알고리즘
        - flag와 turn 변수를 통해 critial section에 들어갈 프로세스를 결정한다.
        - flag : critial section에 들어가려하는 프로세스
        - turn : critial section에 들어갈 차례인 프로세스 → 차례가 끝나면 다음 turn으로 넘기는데 이용
    - 피터슨(Peterson) 알고리즘
        - 데커(Dekker)와 같으나 상대 프로세스에게 진입 기회 양보
    - 제과점(Bakery) 알고리즘
        - 가장 작은 수의 번호표를 가지고있는 프로세스가 진입
        - 여러 프로세스에 대한 처리 가능
