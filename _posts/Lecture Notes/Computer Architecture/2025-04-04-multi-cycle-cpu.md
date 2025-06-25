---  
tags:  
  - architecture  
  - instruction  
  - stage  
  - cpu  
  - state  
  - dependency  
share: "true"  
github_title: 2025-04-04-multi-cycle-cpu  
title: 5. Multi-Cycle CPU  
date: 2025-04-04  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
### Single-cycle implementation is…  
  
Sequential 하고, atomic하여 ISA의 의미와 잘 부합한다.  
  
instruction이 다음 상태를 직접 의미한다. (ex. LOAD 명령어는 다음 cycle의 레지스터가 어떻게 변할것인지를 알려줌)  
  
→ but, inefficient  
  
- 모든 명령어의 실행 시간이 `가장 오래 걸리는 명령어 (=load)` 에 bound되게 된다.  
- 즉, clock frequency를 Load 명령어의 시간보다 더 길게 만들 수 엇다.  
- CISC에서는 이 문제가 더욱 부각된다.  
  
---  
  
## Single cycle Datapath Analysis  
  
Mem: 200, ALU: 100, Reg: 50  
  
||IF|ID|EX|MEM|WB|Total Delay|  
|---|---|---|---|---|---|---|  
|R-type|200|50|100||50|400|  
|I-type|200|50|100||50|400|  
|Load|200|50|100|200|50|**600**|  
|Store|200|50|100|200||550|  
|Jump|200|||||200|  
|Branch|200|50|100|||350|  
  
따라서, 한 사이클이 600ps보다는 커야한다.  
  
즉, frequency가 1/600ps (약 1.67GHz) 보다 작아야한다. 헉…  
  
---  
  
## Multi-cycle Implementation 1.0  
  
그럼 딱 명령어별로 필요한 시간만큼만 돌리자.  
  
50ps로 1-cycle을 돌리되, programmer visible state를 각 cycle의 끝마다 바꾸는 것이지.  
  
그렇다면 각 state별로 바꿔야할 PVS가 정해지게 된다.  
  
각 상태에 따라, instruction의 종류에 따라 다음 state가 정해지게 되며, 한 상태는 필요한 cycle만큼 머무르게 된다. 이때, 각 state마다 켜줘야할 yellow signal들이 다르다. 이걸 어떻게 control할 것인가.  
  
<aside> 💡  
  
What is PVSWriteEN?  
  
- PVS를 변경하는 것을 작동시키는 신호. → 각 instruction이 끝나고 IF로 갈때 켜주면 된다.  
  
왜? 멀티사이클까지는 파이프라인, 인터럽트가 없어서 하나의 명령어는 하나의 PVS 변경을 의미하니까.  
  
</aside>  
  
---  
  
### MicroSequencer v 1.0  
  
ROM을 combinational logic의 lookup table처럼 만들어서 각 state의 다음 상태와, output들을 저장할 수 있게하면 된다.  
  
ex)  
  
000…00(32)_0000 ⇒ 000…00의 32bit 명령어가 들어오고, 현재 상태가 0000일때의 control signal과 다음 state의 정보  
  
즉, row는 2^(32+4) = 2^36개 필요하고 데이터는 각 row마다 output-bit수와 state 4만큼 필요하다.  
  
근데 너무 낭비가 크지 않겠냐싶긴해~  
  
모든 instruction가 현재 상태에 따른 다음 상태와 output이 정해져있다는 뜻.  
  
---  
  
### Microcoding  
  
각 상태마다, 현재 명령어의 type에 따라만 다음 상태를 정해주면 된다.  
  
---  
  
### Micro-code controller  
  
sequencing과 control 목적을 둘 다 가지는 프로세서.  
  
마이크로 명령어는 다음과 같다.  
  
- RegDest를 켜  
- Jump를 꺼  
- 상태를 바꿔  
  
이런 명령어들이 저장되어있고, 마이크로 pc를 이용해 해당 명령어를 가져온다.  
  
**여기서 PC 하나는 현재 state를 의미한다. << 녹음 확인 필요. GPT는 마이크로명령어 주소라고 함.**  
  
<aside> 💡  
  
Micro-code로 상태 말고 아예 program visible state를 제어하죠?  
  
→ 복잡성 증가, 시간 증가, 아키텍쳐 상태와의 선 지키기  
  
</aside>  
  
---  
  
## Performance Analysis  
  
결국 우리가 측정하고 싶은건 한 명령어 실행 당 몇초 걸렸냐  
  
$$ T_{wall-clock} = inst \times CPI \times T_{clk} $$  
  
명령어 구조가 같고, 돌리는 프로그램이 같다면, 사실 CPU 성능은 아래와 같이 나타낼 수 있다.  
  
$$ T_{avg-inst} = T_{clk} \times CPI $$  
  
근데 CPI와 평균 소요 시간은 낮아야 좋은 거거든? 정말 비직관적이니 아래와 같이 쓰자.  
  
$$ MIPS = f_{clk} \times IPC $$  
  
이제 multi-cycle이 왜 좋은지 확인해보자.  
  
### Single Cycle CPU  
  
IPC가 항상 1임.  
  
만약 한 clock을 12개의 마이크로 clock으로 쪼갰다고 하자.  
  
$$ MIPS = IPC_{avg} \times f_{clk} $$  
  
그러면 평균 IPC는 뭘까. JMP는 IPC가 높을꺼고, LOAD는 엄청 낮을 것이다.  
  
각 명령어별로 cycle 소모를 확률에 곱하면 평균 CPI가 나온다.  
  
이를 역수 취하면 된다.  
  
---  
  
### Reducing datapath  
  
Adder는 ALU에서도 수행되고 있지만, Jump address를 4만큼 더하는데에도 사용되고 있다. single-cycle에서는 이 두 연산이 동시에 이루어져야하기 때문에 따로따로 써야했지만, 이제 cycle이 분리되면서 가능해졌다!  
  
대신, PC=PC+4하는 과정과 Instruction을 바탕으로 IF/ID를 하는 과정이 분리되어야한다. (서로 다른 시간에 실행되어야 한다.) 이는 instruction register를 통해 달성할 수 있다.  
  
---  
  
### Removing Redundancy  
  
명령어 메모리와 데이터 메모리가 따로 있는 것이 어색하지 않는가.  
  
그렇다면 하나의 메모리에서 관리하고, 명령어는 명령어 레지스터에, 데이터는 메모리 데이터 레지스터에 저장하자.  
  
이러면 메모리, ALU를 여러번 사용하기 때문에 ALUOut, A, B 등의 레지스터가 필요하다.  
  
<aside> 💡  
  
Why do we need IR, MR?  
  
**IR과 MR은 시간차를 맞추고, 데이터 출처(source)를 명확히 구분하기 위해 필요한 중간 정류장이다.**  
  
**RTL 흐름 상, 다음 단계로 넘길 값이 사라지지 않도록 붙잡아두는 버퍼 역할!**  
  
</aside>  
  
---  
  
### Full control points  
  
→ See the textbook!  
  
---  
  
## Synchronous Register Transfers  
  
### Latch when enabled by control  
  
- PC, IR, MEM, RF  
  
### Latch, always  
  
- MDR, A, B, ALUOut  
      
- IR ← MEM[PC] requires: IorD → 0, MemRead → 1, IRWrite → 1  
      
- PC ← PC, JumpTarget requires: PCWrite → 1, PCSource → 2’b10  
      
- PC ← PC + ALUSrcB requires: PCWrite →1, ALUSrcB → 2’b01 (4), PCSource → 2’b00, ALUSrcA → 2’b00  
      
- MDR ← MEM[ALUOut] requires: MemRead → 1, IorD → 1 (D)  
      
- ALUOut ← PC + ALUSrcB requires: ALUOp: ADD, ALUSrcA = 2’b00 (PC)ALUSrcB → 2’b11 (signed extended)  
      
  
---  
  
## RT Sequencing: R-type ALU  
  
- IF  
    - IR ← MEM[PC]  
    - PC ← PC+4  
- ID  
    - A ← RF[IR[25:21]]  
    - B ← RF[IR[20:16]]  
- EX  
    - ALUOut ← A + B  
- MEM  
    - 그런건 없어용~  
- WB  
    - RF[IR[15:11]] ← ALUOut  
  
각 RT마다 dependency가 있다.  
  
따라서 이들 중 conflict가 나서 한번에 (하나의 cycle 내에서 할 수 없는 것이 있다.)  
  
반대로 말하면, 이를 적절히 잘 피해서 설계하면 회로를 적게 사용할 수 있다.  
  
Note:  
  
- 빨강: 저장한 후에 가져다 써야한다는 의존성  
- 파랑: 값을 덮어 씌우기 전에 써야한다는 의존성  
- 보라: 동일한 ALU등의 리소스를 쓰기 때문에 발생하는 의존성  
  
---  
  
이렇게 각 RT마다 의존성이 존재한다. 그리고 각 step안에는 동시에 해도 되는 RT들이 들어있으며, 각 state는 control signal의 한 상태를 의미한다.  
  
---  
  
## Microcode  
  
CPU가 명령어를 실행할 때 필요한 제어코드를 모아둔 작은 프로그램.  
  
control unit의 신호들을 제어한다고 보면 됨.  
  
언제 하드웨어로 신호 컨트롤 다 할래?  
  
### Horizontal  
  
각 주소에 있는 명령어들이 k-bit의 control output임.  
  
n-bit의 마이크로명령어 주소를 접근하면 바로 튀어나옴  
  
- 빠름 (No decoding)  
- 병렬성이 높음  
- ROM크기가 커짐  
- 제어 신호가 많아질수록 유지보수 어려움  
- 너무 low-level이라 수정이 어려움  
  
### Vertical  
  
제어 신호를 직접 나열하지 않고, 각 m-bit가 저장되어있음. m비트 출력 = m개의 RT.  
  
ROM에서 디코딩하여 신호를 내보낸다.  
  
- 메모리 작아짐.  
- 관리 쉬움  
- Latency 증가  
- 병렬 실행 어려움  
  
---  
  
### Microcoding for CISC  
  
복잡한 명령어를 추가해야한다.  
  
사실상 CISC에서는 필수임