# CPU 스케쥴링

## CPU 스케쥴링

: CPU를 최대한 효율적으로 이용하기 위하여 프로세스 실행순서를 결정하는 것

- 목표
    - Batch System
        - 최대한 많은 일을 수행한다.
        - 처리량(throughout)을 높이는 것!
    - Interactive System
        - 적은 시간 대기하고 빠르게 응답한다.
    - Real-time System
        - 기한에 맞춘다
- CPU 스케쥴링이 결정되는 네가지 상황
    - 실행 → 대기 ( I/O 발생 )
    - 실행 → 준비완료 ( 인터럽트 발생 )
    - 대기 → 준비완료 ( I/O 종료 )
    - 프로세스 종료
- 선점형 ( preemptive ) / 비선점형 ( nonpreemptive ) 으로 나뉨
- Response Time
    - 작업이 처음 실행되기까지 걸린 시간
- Turnaround Time
    - 실행시간 + 대기시간
    - 작업이 완료될 때 까지 걸린 시간

## 비선점형 CPU 스케쥴링

- CPU가 프로세스에 할당 된 순간, 프로세스가 종료되거나 대기상태가 될 때까지 CPU를 점유한다.
- 처리시간 예측이 쉽다.

< 종류 >

- FCFS (First Come First Served)
    - 큐에 도착한 순서대로 CPU 할당
- SJF (Shortest Job First)
    - 수행시간이 가장 짧은 순서대로 CPU 할당
    - 정확한 예측이 불가능하기에 구현하기 어렵다.
- HRN (Hightest Response-ratio Next)
    - 우선순위를 계산하여 높은 순서대로 CPU 할당
    - 우선순위 = ( 대기시간 + 실행시간 ) / 실행시간

## 선점형 CPU 스케쥴링

- 타임 슬라이스 소진, 인터럽스, 시스템 호출 종료 등 더 높은 우선순위의 프로세스가 발생한다면 강제로 CPU를 회수하여 전환한다. ( 우선순위가 높다면 뺏어오는 것! )
- 처리시간 예측이 어렵다
- 데이터가 여러 프로세스에 의해 공유된다면 race condition이 발생할 수 있다.

< 종류 >

- Shortest Remaing Time
    - SJF가 선점형으로 구현된 것!
    - 큐에 현재 작업중인 프로세스보다 더 짧은 수행시간을 가진 프로세스가 들어온다면 선점한다.
- Priority Scheduling
    - 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 CPU 할당 → 우선순위가 같다면 FCFS
    - 문제 상황
        - Starvation ( 기아상태 )

          : 우선순위가 낮은 프로세스는 실행되지 못하고 무한정 대기하는 현상

    - 해결방법
        - Aging

          : 기다린 시간에 비례하여 우선순위를 높이는 기법

- Round Robin
    - 특정 시간을 정해두고 해당 시간동안만 CPU 점유
    - Time Slice ( = Time Quantum ) : CPU를 점유할 시간
    - time slice를 초과하여 interrupt를 통해 CPU를 반납한 프로세스는 큐의 맨 뒤로 되돌아간다.
    - time slice가 너무 크다면 FCFS와 같은 효과를, 너무 작다면 너무 많은 context switch를 야기한다.
- Multilevel-Queue (다단계 큐)
    - Priority와 Round Robin이 혼합된 형태
    - 여러개의 큐가 존재함으로써 각 큐에 서로 다른 Time Slice를 할당한다.
    - 우선순위가 높다면 Time Slice가 작은 큐에 , 우선순위가 낮다면 Time Slice가 큰 큐에 할당한다.
- Multilevel-Feedback-Queue (다단계 피드백 큐)
    - 여러개의 큐가 존재함으로써 상위큐로 갈수록 짧은 Time Slice를 가진다
    - 새로운 프로세스가 실행되면 최상위큐로 들어가며 실행시간이 길어질수록 하위큐로 옮겨진다.
    - 입출력 등 CPU를 매우 짧게 이용하는 프로세스의 경우 우선권을 부여하여 빠르게 처리될 수 있도록 한다. → 평균 Turnaround Time을 줄여줄 수 있다.
