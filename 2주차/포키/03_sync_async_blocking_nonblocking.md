# Blocking/Non-blocking & Synchronous/Asynchronous



호출한 함수 = A

호출된 함수 = B

# 

# Blocking/Non-blocking

> 호출된 함수가 호출한 함수에게 제어권을 주는지

- Blocking: B가 자신의 일을 마칠 때 까지 제어권을 가지고, A는 B가 일을 다 마칠 때까지 기다림
- Non-blocking: B가 할일을 마치기 전에 A에게 제어권 return, A가 B를 기다리면서도 할 일을 할 수 있음



## I/O 작업 시

> I/O 작업을 위해서는 Process, Thread가 Kernel에게 요청해야 함

### 

### Blocking I/O

1. user process(Thread)가 Kernel에게 I/O 요청
2. Kernel의 작업이 완료되어야 작업 결과 반환

단점

- I/O 진행될 동안 작업이 중단되어 resource 낭비
- 여러 Client가 접속할 경우, 서로의 작업을 중단하면 안되기 때문에 Client마다 별도의 Thead 생성 → 비효율적



### Non-Blocking I/O

1. user process가 Kernel에게 I/O 요청
2. Kernel은 작업 완료 여부와 무관하게 즉시 응답
   - 미완료 → 에러코드 응답
3. user process는 중간 중간에 I/O 완료 여부를 체크하면서 다른 할 일을 할 수 있음



# Synchronous/Asynchronus

> 동시성에 주목

- Synchronous: A는 B가 일 하는 동안 상태를 계속 체크
- Asynchronous: B의 상태를 A는 신경쓰지 않고 B 혼자 신경쓰면서 처리
  - 작업이 완료되면 Callback 전달하여 A에게 알림
  - Callback이 오기 전까지 A는 신경쓰지 않고 다른 할 일 할 수 있음



# 4가지 경우

![Untitled](C:\YJ\wooteco\workspace\level3\study\2022-ConquerCS\2주차\포키\images\sync_async_blocking_nonblocking.png)

> 엄마: 밥차리는 중, 나: 밥 먹으려고 기다리는 중



### Blocking & Synchronous

- 엄마: 밥 다 될 때까지 딴 짓 하지말고 여기서 기다려!
- 나: 아무것도 안하고 엄마가 밥 하는 거지켜보는 중

### 

### Blocking & Asynchronous

- 엄마: 밥 다 되면 부를테니까 딴 짓 하지말고 거실에 있어!
- 나: 아무것도 안하고 엄마가 부를때까지 멀뚱멀뚱

### 

### Non-blocking & Synchronous

- 엄마: 밥 아직이니까 너 할거 하고 있어!
- 나: 할 거 하면서 틈틈이 주방 기웃기웃거리면서 다 됐는지 확인중



### Non-blocking & Asynchronous

- 엄마: 밥 다 되면 부를테니까 너 할거 하고 있어!
- 나: 엄마가 부를때까지 할거 열심히 하는중



---

### 

### 예상 질문

- Q. 동기/비동기와 블로킹/논블로킹의 차이를 설명해주세요.
  - A. 동기/비동기는 상태에 관한 것이고, 블로킹/논블로킹은 제어에 관한 것입니다. 동기화와 비동기의 차이가 실행 도중 실행 결과를 확인할 수 있는지의 차이라면 블로킹과 논블로킹은 실행 도중에 제어권을 넘겨받을 수 있는지의 차이입니다.


