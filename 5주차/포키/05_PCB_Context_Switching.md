# PCB(Process Control Block)

> Process Metadata들을 저장하는 곳, 한 PCB에 한 Process 저장

## Process Metadata

CPU가 여러 Process를 관리할 때, 각 Process가 누군지 알아야 한다

이를 위해 저장되는 각 Process들의 정보가 Process Metadata

- Process ID
- Process State
- Process Priority
- CPU Registers
- Owner
- CPU Usage
- Memory Usage

### 역할

프로세스 교체 시 대기 시키는 프로세스에 대한 데이터를 저장해 두고, 다시 수행할 때 복구

### 관리 방식

주소값으로 연결된 리스트(Linked List 방식, 삽입/삭제 용이)

프로세스 생성 → 해당 PCB 생성, PCB List Head에 연결 → 프로세스 완료 시 제거

# Context Switching

> 프로세스의 상태를 저장하고 복원하는 일련의 과정

- 동작중인 프로세스를 대기 시킬 때 상태 PCB에 보관
- 대기중이던 프로세스를 다시 동작할 때 저장한 상태를 PCB에서 읽어 레지스터에 적재
- 인터럽트 발생, CPU 사용 허가 시간 소모 등 프로세스의 상태 변경 시 발생


