# Blocking I/O
## 무엇인가?
- I/O 작업이 진행되는 동안 User Process(Thread)는 대기한다.
## 과정은?
1. Process(Thread)가 Kernel에게 I/O를 요청하는 함수를 호출한다(system call).
2. Kernel이 작업을 완료하면 Process는 작업 결과를 반환받는다.
## 특징은?
- I/O 작업은 CPU 작업을 거의 쓰지 않으므로 가장 중요한 CPU 자원이 유휴 자원으로 낭비된다.
- I/O 요청 클라이언트별로 별도의 Thread를 생성하여 동시 요청을 처리하므로 Context Switching 비용이 크다.

## 어떻게 쓰는가?
- Java의 기본 I/O는 Blocking I/O를 사용한다.
- Java의 NIO(New I/O)는 Blocking, Non-Blocking 모두 지원한다.
# Non-Blocking I/O
## 무엇인가?
- I/O 작업이 진행되는 동안 User Process의 작업을 계속 진행한다.
## 과정은?
1. User Process가 recvfrom(receive from) 함수를 호출한다(Kernel에게 해당 Socket으로부터 데이터 요청)
2. Kernel은 이 요청에 대해서 곧바로 revcBuffer(receive Buffer)를 채워서 보내지 못하므르 , `EWOULDBLOCK`을 리턴한다.
3. User Process는 작업을 계속 진행한다.
4. recvBuffer에 User가 받을 수 있는 데이터가 쓰인(write) 경우 Buffer로부터 데이터를 복사한다.
> recvBuffer는 Kernel의 메모리에 적재되어 I/O보다 훨씬 빠른 속도로 read/write 가능하다.
5. revcform 함수는 데이터를 복사 후 복사한 data의 길이와 함께 User Process에 반환한다. 

## 어떻게 쓰는가?
- Node.js는 싱글 스레드 기반의 Event-driven Non-Blocking I/O를 사용한다.
- Java의 NIO(New I/O)는 Blocking, Non-Blocking 모두 지원한다.
# 참조
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/network/Blocking%20&%20Non-Blocking.html)