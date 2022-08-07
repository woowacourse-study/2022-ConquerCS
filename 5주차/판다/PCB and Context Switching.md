## Process Management
- CPU가 복수의 프로세스를 CPU 스케쥴링을 통해 관리
- 관리를 위해 프로세스의 특징을 저장하는 `Process Metadata`
- 해당 Metadata는 `PCB (Process Control Block)` 에 저장

## PCB (Process Control Block)
- 인터럽트 발생 시 waiting 중인 프로세스의 정보를 저장해 놓아야 한다. 
- 해당 정보를 metadata 형태로 PCB에 저장
- 삽입 삭제가 잦으므로 LinkedList 형태로 저장
- 프로세스 생성시 PCB 생성, 프로세스 완료시 제거

## Context Switching
- CPU가 기존 프로세스의 상태를 PCB에 저장하고, 다른 프로세스의 정보를 PCB에서 레지스터에 등록하는 과정
- 인터럽트 발생 또는 입출력을 위한 대기 시 발생
- CPU가 유휴 상태에 들어가지 않도록 하기 위함
