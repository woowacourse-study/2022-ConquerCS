# CPU Scheduling

> 다른 프로세스가 지연되는 동안 한 프로세스가 CPU를 사용할 수 있게 해서 CPU를 최대로 활용하는 것

→ 시스템을 더욱 효과적이고 빠르고 공평하게 하는 것이 목적

## 프로세스의 상태 전이

### 프로세스의 상태

1. New: 생성됨
2. Ready: CPU 할당 받기 전 준비중
3. Running: CPU 할당 받아 실행중
4. Waiting: 입출력 또는 이벤트 대기중
5. Terminated: 종료된 상태

### 상태 전이

1. admitted(`New` → `Ready`): 프로세스 생성 승인
2. dispatch(`Ready` → `Running`): 상태인 프로세스들 중 하나가 scheduler에 의해 실행
3. Interrupt(`Running` → `Ready`): Timeout, 입출력 발생 → 실행중이던 프로세스를 대기시키고 해당 작업 먼저 처리(preemption)
4. I/O or event wait(`Running` → `Waiting`): 실행중인 프로세스에서 입출력 또는 이벤트 처리 해야할 때, 입출력 또는 이벤트가 끝날 때 까지 대기
5. I/O or event completion(`Waiting` → `Ready`): 입출력 또는 이벤트가 다 끝난 프로세스를 스케줄러에 의해 실행될 수 있는 상태로 전환

## 스케줄링 척도

1. Response Time
   - 작업 최초 실행까지 걸린 시간
2. Turnaround Time
   - 실행 시간 + 대기 시간 → 작업 완료까지 걸린 총 시간

## 선점 / 비선점 스케줄링

### 비선점(nonpreemptive)

프로세스 종료 또는 I/O 등 이벤트가 있을때 까지는 실행이 보장되는 경우

→ 처리시간 예측 용이

- FCFS(First Come First Served)
  - queue에 도착한 순서대로 CPU 할당
  - 먼저 도착한 프로세스의 실행 시간이 길면 평균 대기 시간도 길어짐
- SJF(Shortest Job First)
  - 실행 시간이 가장 짧다고 판단되는 작업 우선 수행
  - 평균 대기시간 감소, 짧은 작업에 유리
- HRN(Hightest Response-ratio Next)
  - 우선순위 계산 → SJF의 단점인 점유 불평등 보완
  - 우선순위 = (대기시간 + 실행시간) / 실행시간

### 선점(preemptive)

OS가 CPU 사용권을 선점할 수 있고 강제로 회수하는 경우

→ 처리시간 예측 어려움

- Priority Scheduling
  - 정적/동적으로 우선순위 부여, 우선순위대로 처리
  - 우선순위가 낮은 프로세스가 무한정 기다릴 수 있음 (Starvation)
    - Aging으로 해결 (오랫동인 Ready상태이면 우선순위 올려줌)
- Round Robin
  - FCFS에 의해 프로세스들이 보내지면 각 프로세스는 동일한 Time Quantum만큼 CPU 할당
  - Time Quantum 크면 FCFS와 다를 바 없어지고, 작으면 Context Switching 비용 증가 → 오버헤드 증가
- Multilevel-Queue
  - 작업을 종류에 따라 여러 큐에 나누고, 각 큐에 서로 다른 알고리즘, Time Quantum 설정
  - 우선순위가 높으면 작은 Time Quantum 할당하여 각 작업이 오래 대기하지 않게 골고루 처리
  - 우선순위 낮으면 큰 Time Quantum 할당 (주로 압축풀기 같은 백그라운드 작업)
- Multilevel-Feedback-Queue
  - 처음엔 모든 프로세스의 우선순위를 동일하게 보고, 실행 후 우선순위를 재조정
    - CPU burst가 크면 우선순위가 낮다고 봄 → Time Quantum을 다 채우면 우선순위 낮춤
    - 내려갈수록 점점 긴 Time Quantum → 오래 걸리는 작업일수록 후순위
  - 짧은 작업에 유리, Interrupt가 잦은 입출력 위주 작업에 우선권 부여
  - 처리시간 짧은 프로세스 먼저 처리 → Turnaround 평균 시간 감소

---

### references

- [CPU Scheduling in Operating Systems - GeeksforGeeks](https://www.geeksforgeeks.org/cpu-scheduling-in-operating-systems/)
- [[운영체제]프로세스(Process) 상태 전이도 (tistory.com)](https://wookkingkim.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4Process-%EC%83%81%ED%83%9C-%EC%A0%84%EC%9D%B4%EB%8F%84)
- [[운영체제 OS] multilevel feedback queue(다단계 피드백 큐) MLFQ 특징, 문제점 (tistory.com)](https://jhnyang.tistory.com/156)


