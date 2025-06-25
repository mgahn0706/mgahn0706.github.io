---  
tags:  
  - architecture  
  - exception  
  - interrupt  
share: "true"  
github_title: 2025-04-18-exceptions-and-interrupts  
title: 10. Exceptions and Interrupts  
date: 2025-04-18  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## CPU must prepare for `unplanned` events!  
  
- Instruction fail  
- External IO devices  
- Quantum expiration  
  
(1) Check for every possible contingency (Polling)  
  
- CPU 낭비  
  
(2) 그 문제는 별로 안일어나니까. 생길때만 처리  
  
### Interrupt 처리?  
  
이미 들어온 친구들은 다 나갈때까지, 아직 안들어온 애들은 파이프라인에서 다 빼야함.  
  
control transfer to the interrupt handler and back must be `transparent` to the interrupted thread! → 내 코드는 인터럽트 핸들러가 한 짓을 알면 안됨  
  
---  
  
## Types of Interrupt  
  
### Synchronous Interrupts (Exceptions)  
  
- Tied to a particular instruction  
- illegal OPCODE, illegal operand, virtual memory faults  
- Faulting instruction cannot be finished.  
  
→ No forward-progress unless handled immediately (다음 명령어 실행 불가. 무조건 처리하고 가야함)  
  
### Asynchronous Interrupts (Interrupts)  
  
- External events that not tide to instruction  
- Ctrl+C, IO Events, timer  
  
→ Some delay is allowed, but you cannot postpone forever!  
  
### Syscall / Trap Instruction (Planned)  
  
- Instruction that is purposed to raise an exception  
    - printf는… 내 관할이 아니다. OS 형님 카바좀 쳐주십쇼  
    - 형님 파일 디스크립터좀 바꿔주셈. 처리되면 얘기해주세요  
  
→ 끊는 시점이 비교적 자유로움  
  
---  
  
## Virtualization and Protection  
  
운영체제만 여러개의 프로세스를 돌리는걸 알고, 유저 레벨에서는 여러개 돌리는지 모름.  
  
architectural state 명확히 보존해주는 것.  
  
### Privilege Levels  
  
User - kernel - hypervisor  
  
여기서 상위 레벨의 행동을 하려면 interrupt를 걸어야함  
  
## Precise Interrupt  
  
synchronous: 예외 명령어 딱 이전에 멈추고, handling끝나고 다시 해당 예외발생 명령어 처리  
  
asynchronous: 자유긴 한데, 보통 예외 발생 이후는 다 flush함  
  
---  
  
## MIPS Interrupt Architecture  
  
### Exception Program Counter (EPC, CR14)  
  
- EPC(CR14): 문제 생긴 시점의 주소 (어디서 멈춰야 해요?)  
- CR13: 문제가 생긴 이유 레지스터  
    - pending interrupt: 내가 뭘 핸들링하고있었는지 적어두는 곳.  
- CR12: enable, disable interrupt 정보  
    - 제어용 레지스터. write (인터셉트 등)  
  
```cpp  
mfc0 r26, $14  
```  
  
로 가져온 후, jr로 pc 값을 바꿔서 복귀한다. 한번에 못가져옴  
  
---  
  
### Interrupt의 행동  
  
- 최대한 레지스터를 안쓰고 나가야한다.  
- function call처럼 r31을 쓸 수 없다.  
- 무조건 callee-saved를 해야한다.  
- 컨벤션: r26 & r27은 커널이 쓰는, 핸들러용 레지스터  
  
---  
  
### Interrupt Servicing  
  
이유를 적은 CR13이 있다.  
  
(1) Interrupt를 핸들하는 코드 자체가 메모리에 저장되어있음  
  
- flexible, but slow  
  
(2) 하드웨어가 바로 보고 처리한다. (vectored interrupt)  
  
- fast, but hard-coded  
  
---  
  
## Returning from Interrupt  
  
- exception은 해당 명령어 재 실행 (EPC에 해당 명령어 주소)  
- interrupt은 해당 명령어 다 보내고 그 다음 명령어 주소 넣기.  
  
(1) MIPS32 : `ERET`  
  
- Atomically restore saved CPU states  
- Restore privilege level  
- Jump back to EPC  
  
<aside> 💡  
  
CPU state는 어디에 저장해두는거지?  
  
→  
  
MIPS는  
  
```  
CR12.Status  
```  
  
레지스터에 **"stacked copies"**를 갖고 있어서, interrupt 발생 시 현재 상태를 백업해두고,**ERET 시 그걸 자동 복원**해줘.  
  
</aside>  
  
(2) MIPS2000  
  
- Assume mfc0 r26 done  
- jr r26 (EPC 복붙한걸로 jump)  
- rfe (restore from exception mode) - branch delay slot에서 실행되어야함  
  
---  
  
## Branch Delay Slot & RFE  
  
```cpp  
1000: BEQ  
1004: ADD (branch delay slot)  
  
5000: Handler (kernel)  
```  
  
여기서 1000에서 BEQ가 만족했지만, branch delay slot으로 1004까지 실행하고 jump한다고 하자. 1004가 page fault 등으로 exception이 났다고 가정하자.  
  
이러면 5000번에서 EPC의 값은 1004이고, ADD를 다시 실행하러 온다. 그런데? 이제 jump해야하는 정보가 사라져서 망해버렸다.  
  
→ 무한 Loop 발생  
  
Solution: Exception은 branch delay slot이면 1000을 걸자.  
  
### Harmful in `JALR r31`  
  
JALR r31이 실행되면 r31의 값으로 점프하면서, 자기의 PC+8을 r31에 넣는다. (이게 기본인데, 하필 가져오는 레지스터도 r31인 것)  
  
우리는 r31을 다시 보면 r31는 PC+8임. 원래 코드 날아감.  
  
→ 원치않는 동작이고, can be looped  
  
---  
  
## Brief Handler code  
  
```nasm  
_handler_short:  
	# prologue  
	addi sp, sp -0x8 # increast stack size by 8-byte  
	sw r8, 0x0(sp)  
	sw r9, 0x4(sp)  
	  
	// use r26, r27 to resolve   
	  
	# epilogue  
	lw r8, 0x0(sp)  
	lw r9, 0x4(sp)  
	addi sp, sp 0x8 # reduce stack size  
	mfrc0 r26, epc  
	jr r26  
	rfe  
```  
  
(1) 일단 handler는 exception이 안나도록 해야함  
  
(2) 그래도 나니까 우선순위를 잘 짜라 (CR12)  
  
→ async 인터럽트는 우선순위에 따라 처리되며, 타이밍이 중요한 친구가 우선 처리된다.  
  
서로 다른 우선순위의 인터럽트는 마스킹에 의해 disabled될 수 있다.  
  
→ 오로지 higher-priority만 re-enable하여 처리한다.  
  
만약 낮은 애들도 re-enable해버리면 무한 루프에 돌 수 있다.  
  
### Nested Handler  
  
```nasm  
_handler_short:  
	# prologue  
	addi sp, sp -0x8 # increast stack size by 8-byte  
	mfc0 r26, epc  
	sw r26, 0x0(sp)  
	sw r8, 0x4(sp)  
	  
	addi r26, r0, 0x405 // interrupt enable bit에 write하여 중간 인터럽트 허용  
	mtc0 r26, status // ??  
	  
	// handler  
	  
	#epilogue  
	  
	addi r8 r0 0x404  
	mtc0 r8, status // ??  
	  
	lw r26, 0x0(sp)  
	lw r8, 0x4(sp)  
	addi sp, sp 0x8 # reduce stack size  
	jr r26  
	rfe  
```