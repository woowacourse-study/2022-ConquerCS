## CPU 스케줄링 (CPU Scheduling)

- 프로세스가 항상 CPU를 사용하는 것은 아님
- CPU의 사용률을 높이기 위해 프로세스를 효율적으로 CPU에 배정하는 알고리즘
- 오버헤드와 기아현상을 줄이고, CPU 사용률을 높이는 것이 목표
- `Batch System` : 시간보다는 처리량이 중요
- `Interactive System` : 빠른 응답 시간 & 적은 대기 시간
- `Real-time System` : 기한 맞추기


## 프로세스 상태

- create : 프로세스가 생성되는 중 -> 승인되면 ready 상태로 전이
- running : 프로세스가 프로세서에 배정되어 명령어를 실행 중 -> 인터럽트 발생시 ready 상태로 전이 / 이벤트 처리 필요시 waiting 상태로 전이 / 종료 시 terminated 상태로 전이
- ready : 프로세스가 CPU 할당을 대기 -> 스케줄러 디스패치를 통해 running 상태로 전이
- waiting : 프로세스가 이벤트 발생을 기다리는 상태 -> 이벤트 완료 시 ready 상태로 전이
- terminated : 프로세스 실행이 종료됨


## 선점 / 비선점 스케줄링

  ### 비선점 스케줄링 (non-preemptive scheduling)
    - 이벤트가 있을 때까지 실행 보장 -> 처리 시간 예측 용이
    - FCFS 방식 : 큐에 도착한 순서대로 CPU 할당
    - SJF 방식 : 수행시간이 짧다고 판단되는 작업부터 CPU 할당
    - HRN 방식 : 대기시간과 실행시간의 비율로 우선순위를 계싼 -> 점유 불평등 보완
    
    
  ### 선점 스케줄링 (preemptive scheduling)
    - OS가 CPU의 사용권을 강제 회수할 수 있는 경우 -> 처리 시간 예측이 어려움
    - Priority Scheduling 방식 : 정적/동적으로 우선순위를 부여해서 우선순위 순으로 처리 -> 기아현상 발생 가능 -> Aging 방식으로 해결
    - Round Robin 방식 : 동일한 시간의 `Time Quantum` 만큼 CPU를 할당받음
    - 다단계 큐 방식 : 작업을 여러 그룹으로 분류하여 복수의 큐를 이용하는 기법 -> 큐마다 다른 Time Quantum 지정
    - 다단계 피드백 큐 방식 : CPU Burst를 막기 위해 Time Quantum을 다 채운 프로세스를 우선순위가 낮은 큐로 내려보내는 기법
    
    
## CPU 스케줄링 척도
  - Response Time : 작업이 처음 실행되기까지 걸린 시간
  - Turnaround Time : 실행 시간과 대기 시간을 합한 시간 
