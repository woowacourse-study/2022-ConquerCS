## 시스템 콜 (System Call)
- OS는 대부분 커널 모드와 유저 모드가 분리되어 있음. 
- 커널 모드는 모든 권한을 갖고 있고, 커널과 모든 드라이버가 하나의 가상 메모리를 공유. 
- 유저 모드는 일반 어플리케이션이 동작하는 영역. 프로세스는 서로 독립적이고, 프로세스간 정보 공유를 위해서는 IPC를 통해야 한다.  
- 일반 프로그램은 커널 모드 접근 권한이 없지만, 작업 처리를 위해서 커널 권한이 필요한 일이 있다. 파일 I/O, 그래픽 처리 등. 
- 커널에 요청해서 커널 모드에서 작업을 처리하고 결과만 유저 모드에 반환.
- 윈도우의 경우 Windows API를 통해 내부적으로 커널 모드의 함수를 실행. 
