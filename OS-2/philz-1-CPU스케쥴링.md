> 운영체제 2

# CPU 스케쥴링

다중 프로그래밍을 가능하게 하는 운영 체제의 동작 기법.

OS는 프로세스들에게 자원 배정을 적절히 함으로써 시스템 성능을 개선할 수 있다.

- Burst Time : 실행에 필요한 시간 (milli second)
- Context Switching: 실행 중인 프로세스가 바뀌는 것.

> 참고: https://www.geeksforgeeks.org/difference-between-arrival-time-and-burst-time-in-cpu-scheduling/

## 비선점형 스케쥴링

프로세스가 작업을 수행하면, 종료될때까지 계속 실행되도록 보장한다.

- 순서대로 처리된다
- 응답시간 예상 가능
- 선점 방식에 비해 스케쥴러 호출 빈도가 낮음
- Context Switching 오버헤드 적음
- 일괄처리에 적합
- CPU 사용시간이 긴 것 하나가 나머지 짧은 것들을 대기시킬 수 있다
  - 시간당 처리율이 떨어질 수 있음

### Shortest Job First: 최단 작업 우선

CPU 점유 시간이 가장 짧은 프로세스에 CPU를 먼저 할당하는 방식의 스케쥴링 알고리즘.

- 평균 대기시간을 최소로 만듬
- 점유 시간이 긴 프로세스는 기아 상태가 발생 가능

### First Come First Served: 선입 선처리

먼저 자원을 요청한 프로세스에게 자원을 할당하는 방식

## 선점형 스케쥴링

CPU를 할당받은 프로세스를 중지하고 CPU를 강제로 점유할 수 있다

- 모든 프로세스에게 CPU 사용 시간을 동일할게 부여할 수 있다.
- 빠른 응답시간이 필요한 시분할 시스템에 적합

### Round Robin

프로세스들 사이에 우선순위를 두지 않고, 순서대로 시간단위 CPU를 할당하는 방식의 알고리즘.

- 보통 시간 단위는 10 ~ 100ms 정도이다.
- 문맥 전환의 오버헤드가 크다.
- 응답시간이 짧아지는 장점이 있다.

#### 타임 슬라이스 간격

- 너무 길면 interactive한 시스템에서 문제가 될 수 있음
  - 입력에 대한 반응 늦음
- 너무 짧으면 Context Switching 많이 발생해서 성능 문제 생김

- 최근 OS는 보통 15~20ms 간격으로 스케쥴링을 수행한다고 한다

## 참고

- https://genesis8.tistory.com/235
- https://ko.wikipedia.org/wiki/%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81_(%EC%BB%B4%ED%93%A8%ED%8C%85)
