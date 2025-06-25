---  
tags:  
  - architecture  
  - instruction  
  - stage  
  - cpu  
share: "true"  
github_title: 2025-04-02-single-cycle-cpu  
title: 4. Single Cycle CPU  
date: 2025-04-02  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## Program Visible State  
  
- PC  
    - 현재 실행중인 명령어의 주소를 저장하는 32비트 레지스터  
- Registers  
    - 5-bit의 read할 레지스터 주소를 넣으면, 저장된 값을 출력한다.  
- Instruction memory  
    - 명령어 주소를 넣으면 32비트 명령어 값이 나온다.  
- Data memory  
    - 주소를 넣으면 저장된 데이터가 나온다.  
  
→ 사실 1-cycle CPU라 한번에 읽고 써야함. 우리 상식으로는 통하지 않는 것이지만, read는 항상 하도록 하고, write 신호를 half-cycle로 주면 하나의 cycle 내에서 read/write가 모두 가능해진다. (교육용 ㅋㅋ)  
  
→ Combinational read, synchronous write.  
  
---  
  
## Instruction Processing  
  
There are 5 generic steps!  
  
1. `IF` : Instruction Fetch  
    - 메모리에서 주소를 바탕으로 명령어를 불러온다.  
2. `ID` : Instruction Decode  
    - 나온 명령어를 바탕으로 combinational logic을 통해 이게 어떤 type의 명령어인지 확인한다.  
    - 해당 결과에 따라 control signal들을 켜고 끈다.  
3. `EX` : Execution  
    - 각 type에 따라 지정된 행동을 수행한다.  
    - ALU에서 덧셈을 한다.  
4. `MEM`: 메모리에 엑세스하여 (load & store)를 한다.  
5. `WB` : Load의 경우에는 write-back을 하여 레지스터에 다시 써줘야 한다.  
  
---  
  
### Let’s Start with R-type…  
  
GP[rd] ← GP[rs] + GP[rt]  
  
Note 1: ALU control signal has 3-bits  
  
Note 2: Wrtie_enable at register files enabled in half-cycle  
  
---  
  
### For I-type too  
  
Note 1: We need to sign-extend the immediate 16-bit to 32-bit.  
  
Note 2: We need to select signals by MUX. (Signals are actually in circuit, even though MUX did not select it), due to (is rt is destination?) and (what data should we add?)  
  
---  
  
### Let’s add Load-Store datapath  
  
Note 1: Need to check whether it is load  
  
---  
  
### Now for jump?  
  
Note: Only for unconditional jump. J, JR(register의 값 주소로 jump), JAL (PC+4 r31에 저장하고 jump), JALR (PC+4를 지정 레지스터에 저장하고 JR 점프)  
  
---  
  
### Finally, for conditional jump  
  
---  
  
### 어떤게 Decode되었을 때 어떤 control 신호를 켤지가 시험에 나올 것이니 꼭 확인할 것.  
  
---  
  
<aside> 💡  
  
OPCODE의 case에 따라 control signal과 ALU Control이 달라진다.  
  
</aside>  
  
---  
  
### Practice Here!  
