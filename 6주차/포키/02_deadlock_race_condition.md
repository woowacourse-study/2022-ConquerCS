# DeadLock & Race Condition

## DeadLock

> 둘 이상의 프로세스 또는 스레드가 서로를 기다리느라 무한 대기하게 되는 상태

### 발생 조건

1. Mutual exclusion(상호 배제)
   - 자원은 한 번에 한 프로세스만
2. Hold and wait(점유 대기)
   - 최소 하나의 자원을 점유하면서 다른 프로세스가 사용중인 자원을 추가로 점유하기 위해 대기하는 프로세스 존재
3. No preemption(비선점)
   - 다른 프로세스에 이미 할당된 자원은 해당 프로세스가 다 쓸 때 까지 뺏을 수 없음
4. Circular wait(순환 대기)
   - 순환 형태로 자원을 대기

### 예방(prevention)

교착 상태 발생 조건 중 하나 제거(자원 낭비 심함)

- 상호 배제 부정: 여러 프로세스가 자원 공유
- 점유대기 부정: 프로세스 실행 전 모든 자원 할당
- 비선점 부정: 다른 프로세스에서 점유중인 자원 요구하면 가진 자원 반납
- 순환대기 부정: 자원에 고유 번호 할당, 순서대로 자원 요구

### 회피(avoidance)

- 은행원 알고리즘(Banker’s Algorithm)
  - 프로세스가 요구하는 자원을 할당하기 전에, 할당 후 시스템이 안정 상태로 남아있게 되는지를 사전에 검사
  - 안정적이지 않으면 다른 프로세스들의 자원이 해지될 때까지 대기

### 탐지(Detection)

- 자원 할당 그래프로 교착상태 탐지
- 자원 요청 시 탐지 알고리즘 실행 → 이에 따른 오버헤드 발생

### 회복(Recovery)

- 교착 상태 일으킨 프로세스 종료
  - 교착 상태의 프로세스 모두 중지
  - 교착 상태 제거될 때까지 하나씩 중지
- 할당된 자원 해제
  - 교착 상태의 프로세스가 점유중인 자원을 선점해서 다른 프로세스에게 할당(해당 프로세스는 일시정지)
  - 우선 순위 낮거나 수행 횟수 적은 프로세스 위주로 자원 선점

## Race Condition

> 공유 자원에 대해 여러 프로세스가 동시 접근, 결과값에 영향 줄 수 있는 상태

## 발생하는 경우

- 커널 작업 수행 중 인터럽트 발생
  - 문제: 커널모드에서 데이터를 로드하여 작업을 수행하다가 인터럽트 발생 → 해당 인터럽트 작업에서 같은 데이터 조작
  - 해결: 커널 모드에서 작업하는 동안은 인터럽트 disable
- 프로세스에서 System Call을 통해 커널 모드로 진입하여 작업을 수행하던 중 문맥 교환 발생
  - 문제: 한 프로세스가 커널모드에서 데이터 조작 → 시간 초과되어 다른 프로세스로 제어권이 넘어가고, 같은 데이터 조작
  - 해결: 프로세스가 커널모드에서 작업하는 중에는 시간 초과되어도 제어권 넘어가지 않도록
- 멀티 프로세서 환경에서 공유 메모리 내의 커널 데이터에 접근
  - 문제: 두 CPU가 동시에 커널 내부 공유 데이터에 접근하여 조작
  - 해결: 커널 내부 공유 데이터에 접근할 때 마다 해당 데이터를 lock/unlock
