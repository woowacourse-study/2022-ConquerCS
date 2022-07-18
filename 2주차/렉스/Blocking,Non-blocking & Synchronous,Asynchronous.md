# Blocking/Non-blocking & Synchronous/Asynchronous
## ****Blocking/Non-blocking****

Block과 Non-blocking은 `호출된 함수`가 `호출한 함수`에게 제어권을 바로 넘겨주는지의 유무 차이가 있다.

### Blocking

호출된 함수가 본인의 작업을 마칠때까지 제어권을 갖고 있는다. 호출한 함수 입장에서는 호출된 함수가 종료될 때까지 아무런 작업을 하지 못한채로 기다려야한다.

### Non-Blocking

호출된 함수가 본인의 작업이 끝나지 않았더라도 호출한 함수에게 제어권을 바로 넘겨준다. 그래서 호출한 함수의 경우 Blocking과 다르게 호출된 함수의 작업이 끝나는 것을 기다리며 다른 작업들을 수행할 수 있다.

## ****Synchronous/Asynchronous****

Synchronous과 Asynchronous는 함수를 호출하여 일을 동시에 일을 수행할 때, 호출된 함수의 작업 완료 여부를 누가 신경쓰는지가 관심사이다.

### ****Synchronous****

호출하는 함수가 호출되는 함수의 작업 완료 후 리턴을 기다리거나, 또는 호출되는 함수로부터 바로 리턴 받더라도 작업 완료 여부를 호출하는 함수 스스로 계속 확인하며 신경쓰는 것이다.

### ****Asynchronous****

호출되는 함수에게 callback을 전달해서, 호출되는 함수의 작업이 완료되면 호출되는 함수가 전달받은 callback을 실행하고, 호출하는 함수는 작업 완료 여부를 신경쓰지 않는 것이다.

## 두 개념의 조합

![Untitled](img/blocking,nonblocking,Syn,Asyn.png)

### Blocking-Sync

- 호출되는 함수는 제어권을 함수가 종료될 때까지 갖고 있고 호출하는 함수는 호출된 함수의 완료 여부를 물어보며 기다린다.

### NonBlocking-Async

- 호출되는 함수는 제어권을 바로 반환하고 호출하는 함수는 호출된 함수의 완료 여부를 신경쓰지 않아 다른 작업을 수행할 수 있다.
- 성능과 자원의 효율적 사용 관점에서 가장 유리하다.

### ****NonBlocking-Sync****

- 호출되는 함수는 제어권을 바로 반환하고, 호출하는 함수는 작업 완료 여부를 물어본다.
- 즉, 함수를 호출 후 바로 제어권을 반환받아 다른 작업을 할 수는 있지만, 함수의 작업이 종료된 것은 아니라 호출부에서 호출받은 함수의 작업 완료 여부를 계속 확인한다.

### ****Blocking-Async****

- 호출되는 함수가 바로 제어권을 반환하지 않고, 호출하는 함수는 작업의 완료 여부를 신경쓰지 않는다.
- Blocking-Async는 별로 이점이 없어 해당 방법을 사용할 필요가 없기는 하지만 개발자가 NonBlocking-Async를 의도하였으나 의도한바와 다르게 Blocking-Async로 동작하는 경우가 있다고 한다.
    - NonBlocking-Async방식을 쓰는데 그 과정 중에 하나라도 Blocking으로 동작하는 작업이 포함되어 있다면 의도하지 않게 Blocking-Async로 동작할 수 있다.

## ****Blocking I/O & Non-Blocking I/O****

🧐 이 부분은 OS가 아닌가..??

## ****Blocking I/O****

1. 프로세스가 커널의 I/O 요청 함수를 호출한다.
2. 커널이 작업을 완료하면 결과를 프로세스에게 반환한다.

### 특징

- 커널의 I/O작업이 진행되는 동안 유저의 프로세스는 자신의 작업을 중단한 채로 대기한다. 작업을 중단한채 대기를 하는 만큼 리소스의 낭비가 발생하게 된다.
- 여러 클라이언트가 접속하는 서버를 Blocking방식으로 구현하는 경우 I/O작업을 진행하는 동안 다른 클라이언트의 요청도 받아야하기에 클라이언트 별로 별도의 Thread를 생성하여야 한다. 이로 인해 많아진 Thread들 간의 Context Switching이 증가하게 되게 된다.

## ****Non-Blocking I/O****

I/O 작업이 진행되는 동안 User Process의 작업을 중단하지 않고 다른 작업을 진행할 수 있다.

1. User Process가 recvfrom 함수 호출한다. (커널에게 해당 Socket으로부터 data를 받고 싶다고 요청함)
2. Kernel은 이 요청에 대해서, 곧바로 recvBuffer를 채워서 보내지 못하므로, "EWOULDBLOCK"을 return함.
3. Blocking 방식과 달리, User Process는 다른 작업을 진행할 수 있음.
4. recvBuffer에 user가 받을 수 있는 데이터가 있는 경우, Buffer로부터 데이터를 복사하여 받아옴.
5. recvfrom 함수는 빠른 속도로 data를 복사한 후, 복사한 data의 길이와 함께 반환함.

[Blocking-NonBlocking-Synchronous-Asynchronous](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)
