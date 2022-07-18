
# **Blocking/Non-blocking**
![.](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fda50Yz%2Fbtq0Dsje4ZV%2FlGe8H8nZgdBdgFvo7IczS0%2Fimg.png)
- 한 작업이 다른 작업을 호출하는 경우, 호출되는 함수가 바로 리턴을 하는지 여부
- `호출된 함수`가 `호출한 함수`에게 제어권을 건네주는 유무의 차이
- ex) 함수 A, B가 있고, A 안에서 B를 호출했다고 가정해보자.
    - 호출한 함수 = A , 호출된 함수 =  B
    - 현재 B가 호출되면서 B는 자신의 일을 진행해야 한다. (제어권이 B에게 주어진 상황)

## **Blocking**

> 호출된 함수가 자신의 작업을 완료할때까지 제어권을 리턴하지 않는다
>
- 호출된 함수는 자신의 작업을 완료하면 호출한 함수에게 제어권을 넘겨주므로 호출한 함수는 다른 일을 하지 않고 대기한다
- **제어권은 호출된 함수에게 있다**

## **Nonblocking**

> 호출된 함수가 바로 제어권을 리턴한다
>
- 호출된 함수가 제어권을 바로 호출한 함수에게 넘겨주어 다른 일을 할 수 있도록 한
- 제어권은 호출한 함수에게 있다

→ 즉, 호출된 함수에서 일을 시작할 때 바로 제어권을 리턴해주느냐, 할 일을 마치고 리턴해주느냐에 따라 블럭과 논블럭으로 나누어진다.

# **Synchronous/Asynchronous**

- 한 작업이 다른 작업을 호출하는 경우, 호출되는 함수의 작업 완료 여부를 누가 신경쓰는지에 따라 나뉜다
- 일을 수행 중인 `동시성`에 주목하자
- 아까처럼 함수 A와 B라고 똑같이 생각했을 때, B의 수행 결과나 종료 상태를 A가 신경쓰고 있는 유무의 차이라고 생각하면 된다.

## **Synchronous**

> 함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크한다.
>
- 호출하는 A는 호출되는 B의 작업 완료 여부 또는 작업 완료 후 리턴을 기다리고 있다
- 즉, 호출된 함수(B)를 호출한 함수(A)가 신경쓰며, 기다리거나 물어본다.

## **Asynchronous**

> 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리한다. (Callback)
>
- 호출되는 함수에게 Callback을 전달해서 작업을 완료하면 실행하도록 한다
- 기다리지도, 물어보지도 않는다
- Asynchronous를 구현하기 위해 **호출된 함수의 작업은 별도의 thread로 빼서 실행**하며 완료된 호출한 함수에게 알려준다
- 비동기는 호출시 Callback을 전달하여 작업의 완료 여부를 호출한 함수에게 답하게 된다. (Callback이 오기 전까지 호출한 함수는 신경쓰지 않고 다른 일을 할 수 있음)

# 치킨집예시 + 정리

위 그림처럼 총 4가지의 경우가 나올 수 있다. 이걸 좀 더 이해하기 쉽게 Case 별로 예시를 통해 보면서 이해하고 넘어가보자

`상황 : 치킨집에 직접 치킨을 사러감`

### **Blocking & Synchronous**

- 호출하는 함수는 호출된 함수의 작업 완료/리턴을 계속 기다린다
- 호출된 함수는 자신의 작업이 완료되면 리턴한다

따라서 호출한 함수는 함수를 호출한 후 리턴을 받기 전까지 다른 일을 하지 않고 대기한다

⇒ ex) 사장님이 치킨 튀기는 동안 멀뚱히 서서 치킨 튀기는거 기다림

### **Blocking & Asynchronous**

- 호출하는 함수는 호출된 함수의 작업 완료/리턴을 기다리지 않는다
- 호출된 함수는 자신의 작업이 완료되면 리턴한다

호출한 함수는 호출한 함수의 리턴을 기다리지는 않지만, 호출된 함수는 자신의 작업이 완료될 때까지 제어권을 넘겨주지 않기 때문에 호출된 함수의 작업이 완료될 때까지 대기하게 된다

⇒ ex) 언제 되는지는 안궁금하고, 그냥 잠깐이래서 될때까지 서서 기다리는 상황.

### **Non-blocking & Synchronous**

- 호출하는 함수는 호출된 함수의 작업 완료/리턴을 계속 기다린다
- 호출된 함수는 호출되면 바로 리턴한다

따라서 호출한 함수는 호출 이후 제어권을 바로 받기 때문에 작업을 계속 하면서, 호출했던 함수의 작업완료는 계속해서 확인하게 된다

⇒ ex) 사장님이 치킨은 알아서 튀기고, 나는 다른일 하다가 n분마다 한번씩 물어봄

### **Non-blocking & Asynchronous**

- 호출하는 함수는 호출된 함수의 작업 완료/리턴을 기다리지 않는다
- 호출된 함수는 호출되면 바로 리턴한다

따라서 호출한 함수는 호출 이후 바로 제어권을 넘겨받아 다른 일을 한다

⇒ 사장님이 치킨은 알아서 튀기고, 나는 다른일 하다가 사장님이 부르면 감.

# **Blocking I/O**

I/O 작업이 진행되는 동안 User Process의 작업을 중단함.

1. Process(Thread)가 Kernel에게 I/O를 요청하는 함수(recvfrom)를 호출
2. Kernel이 작업을 완료
3. 작업 결과를 리턴받음

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5185b000-cba2-40b2-8b98-59efa09a91e9%2FUntitled.jpeg?table=block&id=829278c5-2568-4fba-8348-1ca2bace44b0&spaceId=ae7599b2-a6a0-4ad1-9149-e9ef3a1ab56c&width=1700&userId=1283b1b0-5fc9-41f0-9b53-56b46ea4c788&cache=v2)

## 특징

- I/O 작업이 진행되는 동안 user Process(Thread) 는 자신의 작업을 **중단한 채 대기**
- Resource **낭비가 심함**(I/O 작업이 CPU 자원을 거의 쓰지 않으므로)
- `여러 Client 가 접속하는 서버를 Blocking 방식으로 구현하는 경우`
  - I/O 작업을 진행하는 작업을 중지되어도, 다른 Client가 진행중인 작업을 중지하면 안됨.
  - 그러므로, client 별로 별도의 Thread를 생성해야 함 → **접속자 수가 매우 많아짐**

이로 인해, 많아진 Threads 로 *컨텍스트 스위칭 횟수가 증가함,,, 비효율적인 동작 방식!*

# **Non-Blocking I/O**

I/O 작업이 진행되는 동안 User Process의 작업을 중단하지 않음.

1. 프로세스/스레드가 커널에게 I/O를 요청하는 함수(recvfrom) 호출
2. 커널은 곧바로 리턴
3. 커널 작업이 완료되면 데이터를 리턴함

![Untitled](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd993502c-6b25-4b00-bda3-6b33fa00712e%2FUntitled.jpeg?table=block&id=65f49ee5-f0be-49bd-ab49-371a0c4dc85d&spaceId=ae7599b2-a6a0-4ad1-9149-e9ef3a1ab56c&width=1700&userId=1283b1b0-5fc9-41f0-9b53-56b46ea4c788&cache=v2)

## 진행 순서

1. User Process가 recvfrom 함수 호출 (커널에게 해당 Socket으로부터 data를 받고 싶다고 요청함)
2. Kernel은 이 요청에 대해서, 곧바로 recvBuffer를 채워서 보내지 못하므로, "EWOULDBLOCK"을 return함.
3. Blocking 방식과 달리, User Process는 다른 작업을 진행할 수 있음.
4. recvBuffer에 user가 받을 수 있는 데이터가 있는 경우, Buffer로부터 데이터를 복사하여 받아옴.

   > 이때, recvBuffer는 Kernel이 가지고 있는 메모리에 적재되어 있으므로, Memory간 복사로 인해, I/O보다 훨씬 빠른 속도로 data를 받아올 수 있음.
>
5. recvfrom 함수는 빠른 속도로 data를 복사한 후, 복사한 data의 길이와 함께 반환함.