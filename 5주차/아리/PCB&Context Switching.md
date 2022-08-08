# PCB & Context Switching

## Process Metadata

: CPU가 각 프로세스를 식별하고 스케쥴링하기 위해 필요한 프로세스 정보

- Process ID
- Process State
- Process Priority
- CPU Registers
- Owner
- CPU Usage
- Memeory Usage

## PCB

: Process Metadata를 저장해 놓은 곳. 하나의 PCB에는 한 프로세스의 Metadata가 저장된다.

- 각 PCB는 LinkedList 형태로 저장 → 삽입/삭제 쉬움
- 프로세스가 생성될 때 함께 생성되고, 프로세스 완료시 삭제된다.
- 이전의 프로세스 상태를 PCB에 저장하고, 새로운 프로세스 상태를 PCB에서 읽어 레지스터에 저장하는 과정이 Context Switching이다!
- 프로세스를 수행하다가 대기상태가 될 경우 대기 할 동안 또다른 프로세스를 실행시키기 위해 Context Switching을 진행함으로써 더 빠른 일처리가 가능해진다.
