---  
tags:  
  - sequential-logic  
share: "true"  
github_title: 2024-10-22-sequential-logic-module  
title: 9. Sequential Logic Module  
date: 2024-10-22  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
이제 베릴로그 문법은 모두 배웠다.  
  
combinational logic은 적당히 truth table 그려서 하자.  
  
sequential logic module을 어떻게 설계하면 좋을까?  
  
---  
  
## D-Flip flop  
  
앞에서 배웠던 대로 always block에 clock때마다 Q에 D값을 넣어주면 된다.  
  
### Asynchronous reset  
  
```verilog  
module d_flip_flop(input D, input CLK, input reset, output reg Q);  
  
always@(posedge CLK, posedge reset) begin  
	if(reset == 1'b1) Q <= 0;  
	else Q <= D;  
end  
  
endmodule  
```  
  
### Synchronous reset  
  
```verilog  
module d_flip_flop(input D, input CLK, input reset, output reg Q);  
  
always@(posedge CLK) begin  
	if(reset == 1'b1) Q <= 0;  
	else Q <= D;  
end  
  
endmodule  
```  
  
---  
  
## Registers  
  
- 레지스터는 정보를 저장하는 수단을 제공하는 모든 것을 말한다.  
- 레지스터에는 아래 3가지가 있다.  
    - Data register (d-flip flop으로 만듦)  
    - register file  
    - SRAM (store a large data)  
  
→ flip flop은 SRAM보다 빠르지만, gate가 더 많이 든다. 즉, cache할 때는 SRAM이 유리하다.  
  
- FPGA에서는 레지스터 파일과 SRAM 모두 SRAM으로 합성되고, LUT로 구성된다.  
  
```verilog  
module register  
#(N = 4)  
(input[N-1:0] din, input reset, input clk, output reg [N-1:0] dout);  
  
always@(posedge clk, negedge reset) begin  
	if(reset !== 1'b1) dout <= {N{1'b0}};  
	else dout <= din;  
end  
  
endmodule  
```  
  
만약 Load를 원할때만 하고 싶다면  
  
```verilog  
module register  
#(N = 4)  
(input[N-1:0] din,   
input reset,   
input clk,   
input load,  
output reg [N-1:0] dout);  
  
always@(posedge clk, negedge reset) begin  
	if(reset !== 1'b1) dout <= {N{1'b0}};  
	else if(load == 1'b1) dout <= din;  
	// 아무것도 없을때는 상태 유지  
end  
  
endmodule  
```  
  
그렇다면 Register file은 어떨까?  
  
보통 WRITE를 하려면 address와 값이 모두 필요해서 회로가 커진다. 그래서 보통 1W2R형태를 쓴다. 이번에도 그렇게 구현하자.  
  
```verilog  
module register_file   
#(parameter N = 4, parameter M = 16, parameter WORD = 8)  
(input [N-1:0] raddr_a, raddr_b, waddr,  
 input clk,  
 input [WORD-1:0] din;  
 input we, //write enable  
 output [WORD-1:0] dout_a, dout_b);  
   
 reg [WORD-1:0] memory [M-1:0];  
 reg [N-1:0] raddr_a_buffer, raddr_b_buffer, waddr_buffer;  
 reg we_buffer;  
 reg [WORD-1:0] din_buffer;  
   
 assign dout_a = memory[raddr_a];  
 assign dout_b = memory[raddr_b];  
   
 always@(posedge clk) begin  
	 raddr_a_buffer <= raddr_a; ... // and the other buffers  
	 din_buf <= din;  
	 if(we==1'b1) memory[waddr_buffer] <= raddr_a_buffer;  
end  
  
   
 end  
   
   
 endmodule  
```  
  
buffer를 사용하면 clock edge에서의 상태가 버퍼에 저장되고, 그 다음 사이클에서 안정적으로 read write가 가능해진다.  
  
---  
  
## Shifter  
  
shifter는 clock cycle에 맞추어서 다음 FF로 값을 전달한다.  
  
하나의 shifter은 serial 또는 parallel한 input과 output을 가질 수 있는데,  
  
즉, 어디서 인풋을 주고 어디서 아웃풋을 받느냐에 따라  
  
- SISO  
- PISO  
- SIPO  
- PIPO  
  
로 나뉜다.  
  
```verilog  
//n-bit shifter, SIPO  
module shifter_register  
#(parameter N)  
(input din,   
 input reset,  
 input clk,  
 output reg [N-1: 0] Q);  
   
 always @(posedge clk) begin  
	if(reset != 1'b1) Q <= {N{1'b0}};  
	else Q <= {din, Q[N-1:1]};	   
end  
   
 endmodule  
```  
  
parallel로 하고 싶다면 din을 [N-1:0]으로 받고 load 신호를 주자.  
  
---  
  
### Universal Shift Register  
  
위에서 언급한 4개가 모두 되는 레지스터.  
  
즉,  
  
- Shift left / right 선택  
- data parallel (load)store  
- serial in and out  
  
다 되는걸 만들자.  
  
기본적인 회로 설계는,  
  
- 0 0 _ nothing  
- 0 1 _ right shift  
- 1 0 _ left shift  
- 1 1 _ load data  
  
  
MUX로 값을 select해서 DFF에 값을 넣어준다. 즉, 다음 행동을 어떻게 할지 mux가 설정하는 것과 같다.  
  
```verilog  
module universal_shifter  
#(parameter N = 4)  
(input clk,  
input reset,  
input rsi, lsi,  
input [N-1:0] din,  
input [1:0] s,  
output reg [N-1:0] qout);  
  
always @(posedge clk) begin  
if(!reset) qout <= {N{1'b0}};  
else  
	case(s)  
		2'b00: ;  
		2'b01: qout <= {rsi qout[N-1:1]};  
		2'b10: qout <= {qout[N-2:0], lsi};  
		2'b11: qout <= din;  
  endcase  
end  
  
endmodule  
```  
  
---  
  
## Counters  
  
counter에는  
  
- synchronous counter  
    - Binary counter  
    - BCD counter: decimal하게 count  
    - Gray counter: 00 - 10 - 11 - 01 과 같이 count  
- asynchronous counter  
    - binary ripple counter (up and down counter)  
  
가 존재한다.  
  
### JK flip-flop으로 카운터 만들기  
  
- **JK flip-flop: 1, 1일때 output이 toggle**  
    - J는 1, K는 0  
  
clk은 일정하게 준다. 첫번째 J, K에는 1과 1이 들어가기 때문에 매 clk negedge마다 값이 바뀐다.  
  
→ 해당 값은 qout[0]이며, 이 값은 clk에 들어간다.  
  
→ 그러면 주기가 2배 증가한채로 다음 JK FF가 작동한다.  
  
즉, qout을 보면 0000 → 0001 → 0010 → 0011 → 0100 → 0101로 count가 올라간다.  
  
Q. 왜 이건 asynchronous인가?  
  
clk에 전체 count가 같이 올라가지 않고, delay가 존재하며 각 카운터의 값이 clk에 의존하지 않고 서로 다른 값에 의존하기 때문에, 모두 edge triggered하지 않기 때문이다.  
  
```verilog  
module binary_ripple_counters  
#(parameter N = 4)  
(input clk,  
output reg Q[N-1:0]);  
  
genvar i;  
generate  
	for(i=0; i<N; i = i +1) begin: ripple_counter  
		if(i==0)always@(negedge clk) qout[1] <= ~qout[0];  
		else always@(negedge qout[i-1]) begin  
			qout[i] <= ~qout[i];  
		end  
	end  
endgenerate  
  
endmodule  
```  
  
---  
  
## Binary Counter (Synchoronous)  
  
```verilog  
module binary_counter  
#(parameter N = 4)  
(input clk, enable, reset  
output reg [N-1:0] qout  
output reg rco);  
  
wire cout;  
  
always @(posedge clk) begin  
	if(reset) qout <= {N{1'b0}};  
	else begin  
	qout <= qout + 1;  
end  
  
assign cout = &qout;  
  
always@(negedge clk) begin  
	rco <= cout;  
end  
  
endmodule  
```  
  
위는 ripple하지 않고 1을 계속 더해주는 binary counter module이다.  
  
rco는 왜 있는가?  
  
→ clk을 `{cout, qout} <= qout + 1` 처럼 따로 줬다고 생각해보자. 이러면 다음 사이클 동안에는 cout = 1이고, qout = 0000이다. 즉, 더 큰 모듈이 해당 값을 받을 때, posedge에서 업데이트할 것이기 때문에  
  
0000 1111 → 0000 0000 → 0001 0001  
  
(cout: 0) → (cout : 1). → (cout = 0)  
  
처럼 한 사이클이 늦게 도착하게 된다.  
  
그러면 바로 assign하면 되지 않을까?  
  
이 경우, 뭔가 동시에 딱 해버리면 어떻게 운이 좋아서 안그럴것 같지만,  
  
clock skew로 인해 더 위쪽의 counter가 늦게 발동되면, 이미 rco가 1이 된 상태이기 때문에 동시에 1이 되버릴 위험이 있다.  
  
0000 1110 → 0001 1111  
  
(cout = 0) → (cout = 1, but skew로 인해 왼쪽것이 바로 반영됨)  
  
따라서, negedge로 rco를 바깥으로 안전하게 전달하는 장치 하나가 필요하다.  
  
rco를 enable에 넘겨서, rco가 발생했을 때만 1을 올리도록 하는 것을 볼 수 있다.  
  
---  
  
## Binary Up&Down counters  
  
up과 down을 모두 커버하려면 이 2가지 버전이 있다.  
  
```verilog  
module binary_up_down_counter  
#(parameter N = 4)  
(input clk, reset, enable, upcnt,   
  output reg [N-1:0] qout,  
  output reg rco, bco  
  );  
    
  wire cout, bout;  
    
  assign cout = &qout;  
  assign bout = ~(|qout);  
    
  always @(posedge clk) begin  
	  if(!reset) qout <= {N{1'b0}};  
	  else if (enable) begin  
		  if(upcnt == 1'b1) qout <= qout + 1;  
		  else qout <= qout - 1;  
			end  
	  end  
	    
	  always @(negedge clk) begin  
		  rco <= cout;  
		  bco <= bout;  
		 end  
		    
```  
  
또는 enable, upcnt로 받지 않고 eup, edn을 따로 받은 다음에, 각각을 update해줄 수 있다.  
  
둘다 1이면 그대로 있겠지.  
  
이때, eup, edn은 enabled + 방향이므로,  
  
(&qout) & eup을 해줘야 정상적으로 올라간다. down인 경우에도 1111인 경우는 오기 떄문이다.  
  
<aside> 📖  
  
그렇다면 version 1에서도 &upcnt가 있어야하는거 아닌가?  
  
</aside>