![IBM developerWorks](https://velog.velcdn.com/images/sojukang/post/e37d66ec-299f-4ee3-b57e-0221a85fab05/image.png)
# Blocking/Non-blocking
- 호출된 함수가 자신의 로직 실행을 전부 마치고 리턴한다 or 호출된 함수가 바로 리턴한다  
## Blocking
- 호출된 함수가 자신의 로직 실행을 전부 마치고 리턴한다.
- 함수 A가 실행중인 로직 내에서 함수 B를 호출할 경우 함수 B가 종료되어 리턴할 때까지 A의 로직은 진행되지 않는다(제어권이 A -> B...B완료 -> A로 넘어간다).
- 함수 A가 실행중인 상태에서 함수 C를 호출할 경우 A가 종료되어 리턴할 때까지 C는 대기한다.
## Non-blocking
- 호출된 함수가 바로 리턴한다. 
- 함수 A가 실행중인 로직 내에서 함수 B를 호출할 경우 함수 B는 즉시 리턴하여 함수 A의 로직이 진행된다(제어권이 A -> B -> A... A와 B 중 어느 것이 먼저 끝나도 상관 없음).
# Synchronous/Asynchronous
- 호출되는 함수의 작업 완료 리턴을 기다린다 or 기다리지 않는다 
## Synchronous 
- 호출되는 함수의 작업 완료 리턴을 기다린다.
### Blocking(안정성 높음)
- 호출된 함수가 자신의 로직 실행을 전부 마치고 리턴하며, 다른 함수들은 대기한다.
### Non-blocking
- 호출된 함수가 바로 리턴하며, 다른 작업을 할 수 있으나 호출된 함수의 리턴을 기다리며 체크한다.
## Asynchronous 
- 호출되는 함수의 작업 완료 리턴을 기다리지 않는다.
### Blocking
- 호출된 함수가 자신의 로직 실행을 전부 마치고 리턴하며, 호출된 함수의 작업 완료 리턴을 기다리지는 않는다.
### Non-blocking(가용성 높음)
- 호출된 함수가 바로 리턴하며, 작업 완료 리턴을 기다리지 않는다. 
# 참고
[gyoogle.dev](https://gyoogle.dev/blog/computer-science/network/Blocking,Non-blocking%20&%20Synchronous,Asynchronous.html)
[HomoEfficio](http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)