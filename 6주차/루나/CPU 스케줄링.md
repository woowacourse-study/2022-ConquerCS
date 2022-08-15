## CPU **스케줄링이란?**

> CPU 를 잘 사용하기 위해 프로세스를 잘 배정하기
>

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c2f0c51-ed2f-464e-b2d3-beaafd193673/Untitled.png)

- 조건 : 오버헤드 ↓ / 사용률 ↑ / 기아 현상 ↓

**다중 프로그래밍의 목적은 CPU 이용률을 최대화하기 위해 항상 실행 중인 프로세스를 가지게 하는데 있다.** 어떤 프로세스가 대기해야 할 경우, 운영체제는 CPU를 그 프로세스로부터 회수해 다른 프로세스에 할당한다.

즉, CPU 이용률을 최대화 하는 것은 다중 프로세서 운영체제 설계의 핵심이 된다.

### CPU I/O 버스트 사이클

**프로세스 실행은 CPU 실행과 I/O 대기의 사이클로 구성된다.**

프로세스의 실행은 CPU Burst로 시작된다. 뒤이어 I/O Burst가 발생하고, 그 뒤를 이어 또 다른 CPU Burst가 발생하며, 이어 또 다른 I/O Burst 등등으로 진행된다. 결국 아래의 그림처럼 마지막 CPU Burst는 실행을 종료하기 위한 시스템 요청과 함께 끝난다.

![https://imbf.github.io/assets/computer-science/CPU-Scheduling-1.png](https://imbf.github.io/assets/computer-science/CPU-Scheduling-1.png)

CPU Burst들의 지속시간을 광범위하게 측정한 그래프는 CPU 스케줄링 알고리즘을 구현할 때 매우 중요하다.

### ****Scheduling Criteria : Goals****

수 많은 프로세스들을 어떤 순서로 정렬할지 정책을 수립하는 것이 스케줄링이라면, "좋은" 정렬 방법과 "나쁜" 정렬 방법이 있을 것이다 이렇게 스케줄링 알고리즘을 평가할 수 있는 기준을 **Scheduling Criteria**라고 한다

1. **CPU Utilization** (Keep the CPU as busy as possible) CPU가 쉬고 있지 않게 해야 한다
2. **Throughput** (Number of processes that complete their execution per time unit) 단위 시간 당 처리량 → # of instructions / second
3. **Turnaround Time** (Amount of time to execute a particular process) 수행을 요청 한 후 작업이 끝날 때까지 걸린 시간
4. **Waiting Time** (Amount of time a process has been waiting in the ready queue) 수행을 요청 한 후 작업이 시작될 때까지 걸린 시간 → Running이 된 시간 - Ready queue에 들어간 시간
5. **Response Time** (Amount of time it takes from when a request was submitted until the first response is produced) 요청 이후 응답 시간

CPU Utilization, Throughput은 늘리고, Time 지표들은 감소시키는 것이 스케줄링 목표가 된다

### 시스템별 목표

CPU Scheduling의 세부적인 목표는 시스템 마다 다르다

**Batch System**

배치 시스템, 한번에 하나의 프로그램만 수행하는 것

- 가능한 한 많은 일을 수행하기 위해 throughout과 CPU utilization 이 중요

**Interactive System**

사용자가 컴퓨터 앞에서 대화형으로 동작하는 시스템

- Response Time → 프로세스가 Ready queue에서 대기하는 시간을 최소화한다
- Waiting Time → 프로세스가 Wait queue에서 대기하는 시간을 최소화한다
- Proportionality → 사용자가 요구하는 바를 이루어야 한다

이러한 시스템의 경우, Time Sharing 기법을 이용해야 한다

**Real-time System**

시간 제약 조건이 걸려있는 시스템

- Meeting Deadlines
- Predictability

## **선점 / 비선점 스케줄링**

### **선점 (preemptive)**

> OS가 CPU의 사용권을 선점할 수 있는 경우, 강제 회수하는 경우 (처리시간 예측 어려움)
>
- 장점
    - 높은 우선순위를 가진 프로세스를 빠르게 처리하려는 시스템에 유용
    - 빠른 응답 시간을 요구하는 시분할 시스템에 유용
- 단점
    - 높은 우선순위를 가진 프로세스들이 들어오는 경우 Overhead 발생

### **비선점 (nonpreemptive)**

> 프로세스 종료 or I/O 등의 이벤트가 있을 때까지 실행 보장 (처리시간 예측 용이함)
>
- **장점**
    - 모든 프로세스들에게 공정
    - 응답 시간 예측 가능
- **단점**
    - 짧은 작업을 수행하는 프로세스라도 긴 작업이 종료될 때 까지 기다려야하는 경우 발생****

### **[#](https://gyoogle.dev/blog/computer-science/operating-system/CPU%20Scheduling.html#_3-%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%89%E1%85%A6%E1%84%89%E1%85%B3-%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2)3. 프로세스 상태**

![https://user-images.githubusercontent.com/13609011/91695344-f2dfae80-eba8-11ea-9a9b-702192316170.jpeg](https://user-images.githubusercontent.com/13609011/91695344-f2dfae80-eba8-11ea-9a9b-702192316170.jpeg)

- 선점 스케줄링 : `Interrupt`, `I/O or Event Completion`, `I/O or Event Wait`, `Exit`
- 비선점 스케줄링 : `I/O or Event Wait`, `Exit`

---

**프로세스의 상태 전이**

✓ **승인 (Admitted)** : 프로세스 생성이 가능하여 승인됨.

✓ **스케줄러 디스패치 (Scheduler Dispatch)** : 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것.

✓ **인터럽트 (Interrupt)** : 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 준비 상태로 바꾸고, 해당 작업을 먼저 처리하는 것.

✓ **입출력 또는 이벤트 대기 (I/O or Event wait)** : 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때까지 대기 상태로 만드는 것.

✓ **입출력 또는 이벤트 완료 (I/O or Event Completion)** : 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것.

# **CPU 스케줄링의 종류**

## 비선점 스케줄링

### FCFS (First Come First Served)

- 큐에 도착한 순서대로 CPU 할당
- 실행 시간이 짧은 게 뒤로 가면 평균 대기 시간이 길어짐

**장점**

- 개발 용이
- **공평성 유지 (Fair)**
- No indefinite postponement (No Starvation)

**한계**

- **Convoy Effect**
    - 소요 시간이 긴 프로세스가 먼저 도달할 경우 효율성이 낮아진다
    - 실행 시간이 짧은 작업이어도 뒤로 가면 대기 시간이 길어진다

  → SJF 알고리즘 등장


### SJF (Shortest Job First)

- 수행시간이 가장 짧다고 판단되는 작업을 먼저 수행
- FCFS 보다 평균 대기 시간 감소, 짧은 작업에 유리

**한계**

- **Starvation**
    - 사용 시간이 긴 프로세스는 영원히 CPU를 할당받지 못할 수도 있다

### HRN (Hightest Response-ratio Next)

- 우선순위를 계산하여 점유 불평등을 보완한 방법(SJF의 단점 보완)
- 우선순위 = (대기시간 + 실행시간) / (실행시간)

## 선점 스케줄링

### Priority Scheduling

- 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 처리
- 선점형/비선점형 모두에 접목시킬 수 있다

**한계**

- Starvation (우선 순위가 낮은 프로세스가 무한정 기다림)
- Indefinite Blocking(무기한 봉쇄) 실행 준비는 되어 있으나 CPU를 사용하지 못하는 프로세스가 CPU를 무한정 기다리는 상태

→ Aging 기법으로 문제를 해결할 수 있다

### SRT(Shortest Remaining Time) 스케줄링

- 짧은 시간 순서대로 프로세스를 수행한다.
- 현재 CPU에서 실행 중인 프로세스의 남은 CPU 버스트 시간보다 더 짧은 CPU 버스트 시간을 가지는 프로세스가 도착하면 CPU가 선점된다.
- 새로운 프로세스가 도착할 때마다 스케줄링이 이루어진다

**한계**

- Starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시 하기 때문에 CPU 사용 시간을 측정할 수가 없다

### Round Robin

- FCFS에 의해 프로세스들이 보내지면 각 프로세스는 동일한 시간의 `Time Quantum` 만큼 CPU를 할달 받음
    - `Time Quantum` or `Time Slice` : 실행의 최소 단위 시간
- 현대적인 CPU 스케줄링 방식
- 할당 시간이 끝나면 프로세스는 선정 당하고 Ready Queue의 제일 뒤에 삽입된다
- CPU 사용시간이 랜덤한 프로세스들이 섞여 있을 경우에 효율적이다
- 프로세스의 Context를 save할 수 있기 때문에 가능하다

**장점**

- Response time이 빨라진다 N개의 프로세스가 Ready queue에 있고 할당시간이 q(Time Quantum)인 경우 각 프로세스는 q 단위로 CPU 시간의 1/n을 얻는다 → 어떤 프로세스도 (n-1) * q * Time unit 이상 기다리지 않는다
- 프로세스가 기다리는 시간이 CPU를 사용할 만큼 증가하는 공정한 스케줄링이다

**한계(주의점)**

- Time Quantum이 크면 FCFS와 같아진다
- Time Quantum이 작으면 Context Switching이 잦아져서 Overhead가 증가한다

→ 적당한 Time Quantum을 설정하는 것이 중요하다

### Multilevel-Queue (다단계 큐)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/253ad4c5-8da7-490d-9a03-6563df5922a2/Untitled.png)

- 작업들을 여러 종류의 그룹으로 나누어 여러 개의 큐를 이용하는 기법
- 우선순위가 낮은 큐들이 실행 못하는 걸 방지하고자 각 큐마다 다른 `Time Quantum`을 설정 해주는 방식 사용
- 우선순위가 높은 큐는 작은 `Time Quantum` 할당. 우선순위가 낮은 큐는 큰 `Time Quantum` 할당.

### Multilevel-Feedback-Queue (다단계 피드백 큐)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f18fd155-1991-4f8f-b417-dc755f45a329/Untitled.png)

- 다단계 큐에서 자신의 `Time Quantum`을 다 채운 프로세스는 밑으로 내려가고 자신의 `Time Quantum`을 다 채우지 못한 프로세스는 원래 큐 그대로
    - Time Quantum을 다 채운 프로세스는 CPU burst 프로세스로 판단하기 때문
- 짧은 작업에 유리, 입출력 위주(Interrupt가 잦은) 작업에 우선권을 줌
- 처리 시간이 짧은 프로세스를 먼저 처리하기 때문에 Turnaround 평균 시간을 줄옂줌
- 만약, 우선순위 순으로 큐를 사용하는 상황에서 우선순위가 낮은 아래의 큐에 있는 프로세스에서 starvation 상태가 발생하면 이를 우선순위가 높은 위의 큐로 옮길 수도 있다.
- 대부분의 상용 운영체제는 여러 개의 큐를 사용하고 각 큐마다 다른 스케줄링 방식을 사용한다. 프로세스의 성격에 맞는 스케줄링 방식을 사용하여 최대한 효율을 높일 수 있는 방법을 선택한다.