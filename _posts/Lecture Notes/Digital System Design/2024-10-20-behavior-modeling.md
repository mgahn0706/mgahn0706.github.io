---  
tags:  
  - verilog  
  - behavior  
share: "true"  
github_title: 2024-10-20-behavior-modeling  
title: 3. Behavior Modeling  
date: 2024-10-20  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
Assignment  
  
- continuous assignment  
- blocking assignment  
- nonblocking assignment 등등  
  
---  
  
## Procedure Blocks  
  
(1) initial block  
  
reg를 초기화하고, wire에 값을 drive하기 위함  
  
(2) always block  
  
continuous한 동작을 하는 하드웨어를 만들기 위함  
  
→ 각각의 always block는 하나의 logic을 의미함. (마치 useEffect)  
  
- 두 block 모두 어떤 동작을 표현하며,  
- simulation 0에 시작하고  
- nested 될 수 없다.  
  
---  
  
## Initial block  
  
testbench에서만 쓰고, design-level에서는 사용하지 않는다.  
  
- reg를 초기화하거나, port에 값을 넣어줄 때 쓴다. (net를 초기화하지 않는다!)  
  
```verilog  
initial begin  
	statement;  
end  
```  
  
- 전체 시뮬레이션에서 1번만 실행된다.  
- 모든 Initial block은 t=0에서 동시에 시작한다.  
  
```verilog  
reg clock;  
initial clock = 0;  
// or  
reg clock = 0;  // 이것도 initial block에 해당함에 유의.  
  
module inc(input [3:0] x, output reg[3:0] y = 4'b0000);  
endmodule  
  
module inc(nput[3:0]x, output reg [3:0] y);  
y = 4'b0000;  
endmodule  
  
// 위의 경우 모두 가능하다.  
```  
  
위처럼 design module에서 initial block을 사용할 수는 있지만, 쓰지는 말자. FPGA는 가능하다!  
  
아래는 initial block의 예시이다.  
  
```verilog  
module main;  
reg [3:0] a = 2;  
wire [3:0] b;  
inc my_inc(.x(a), .y(b));  
  
initial begin  
	$display("Hi a=%d b=%d", a, b);  
	$finish  
end  
endmodule  
  
module inc(input[3:0] x, output reg[3:0] y);  
	y = 4'b0000;  
endmodule  
```  
  
<aside> 📖  
  
항상 initialize할 때에는, output reg인지 꼭 확인하자. 많이 헷갈린다.  
  
</aside>  
  
<aside> 📖  
  
wire b에 b = 4’0000이 되는지 베릴로그에서 확인해보자  
  
</aside>  
  
### Synthesizability  
  
- ASIC → not synthesizable!  
- FPGA → synthesizabe  
  
→ ASIC에서는 안돌아가니까, design module에서는 쓰지 말자.  
  
대부분의 공정에서는  
  
RTL → Simulation → FPGA(verify first, lookup table) → ASIC  
  
과정을 거친다.  
  
---  
  
## Always block  
  
sensitivity list가 occur하면 실행되는 block  
  
→ sequential block(latch, flip-flop) 구현에 필수적이며  
  
→ 복잡한 combinational logic에도 사용할 수 있다.  
  
<aside> 📖  
  
복잡한 combinational logic에서 사용하는 것이 왜 유리할까?  
  
</aside>  
  
```verilog  
module flip_flop(input [3:0]D, input CLK, output reg[3:0] Q);  
	always@(posedge CLK) begin  
		Q <= D;  
	end   
endmodule  
```  
  
위와 같이 flip flop을 구현할 수 있다.  
  
**주의점**  
  
- LHS (여기서는 Q)는 항상 reg type이어야 함.  
- assignment는 non-blocking assignment(< = )를 쓴다.  
  
<aside> 📖  
  
왜 sequential에서는 no-blocking, comb에서는 blocking을 쓸까?  
  
</aside>  
  
⇒ 위의 회로를 합성하면 4-bit register로 합성딘다.  
  
### How about Latch?  
  
```verilog  
module latch(input CLK, input[3:0] D, output reg[3:0] Q);  
	always@(CLK, D) begin  
		if(CLK==1) Q <= D;  
	end  
endmodule  
```  
  
→ CLK 이 high이면 assign. D-latch 4개 합성된다.  
  
### Inverter  
  
combinational logic에도 alwyas를 쓸 수 있다.  
  
```verilog  
module inverter(input [3:0] a, output reg[3:0] y);  
// combinational logic이지만, always block 안이라서 reg로 선언해야한다.  
	always@(*) begin  
		y = ~a;  
	end  
endmodule  
```  
  
always@(*)는 block 내에서 output을 변화시킬 수 있는 값들이 변화하면 바꾸라는, useEffect의 원리와 유사한 성질을 갖는 표시이다.  
  
→ 여기서는 a가 바뀌면 다시 실행한다.  
  
→ @(*) 를 이용하면 코드짜기가 쉽고, 버그도 적다.  
  
위의 코드를 합성하면, 인버터가 각 비트마다 연결된다. 즉, 모든 reg가 register로 합성되지 않는다!  
  
→ 이것은 베릴로그가 판단해서 해준다.  
  
### Encoder  
  
encoder도 comb로직인데, 이렇게 짜면 어떨까?  
  
```verilog  
module encoder4to2(input[3:0] y, output reg[1:0] x);  
always@(*) begin  
	if(y == 4'b1000) x = 2'b00;  
	else if(y == 4'b0100) x = 2'b01;  
	else if(y == 4'b0010) x = 2'b10;  
	else if(y == 4'b0001) x = 2'b11;  
end  
endmodule  
```  
  
이것은 로직상으로는 combinational logic이지만, sequential로 합성된다. 왜일까?  
  
→ Unwanted Latches!  
  
1000, 0100 등 one-hot 신호가 아닌 경우 (ex. 0111)에는 따로 y가 처리되어있지 않다.  
  
즉, 베릴로그는 이런 경우에 ‘기존 값을 유지한다’라는 것으로 해석한다.  
  
그렇다면, 기존값을 유지하기 위해 latch를 쓸 수 밖에 없게 되는 것이다.  
  
if 조건을 쓸 때에는 항상 else를 써서 모든 케이스를 다 처리할 수 있도록 하자.  
  
---  
  
## Blocking and Nonblocking  
  
### Procedural assignment  
  
assign이나 wire을 쓰지 않는, continuous하지 않은 assignment  
  
- initial이나 always block 안에서 ‘만’ 써야한다.  
- variable data type (reg, integer 등)의 값을 업데이트 한다.  
  
<aside> 📖  
  
reg와 integer의 차이는 무엇인가  
  
</aside>  
  
예시)  
  
```verilog  
reg a = #5 4'b1111; // evaluation 후 5ns delay -> assign  
#5 reg a = 4'b1111; // 5ns delay 후 evaluation  
```  
  
### Blocking assignment  
  
```verilog  
module blocking;  
	reg x, y, z;  
initial begin  
	x = #5 1'b0;  
	y = #3 1'b1;  
	z = #6 1'b0;  
	end  
endmodule  
```  
  
오른쪽(RHS)에 있는 값들을 evaluate하고, assign하는데 작성된 순서대로 하나하나 실행함.  
  
즉, 1’b0 ev → 5초 → x assign → 1’b1 ev → 1s → y assign → 1’b0 ev → 6s → z assign 순으로 진행되므로 z는 14초 시점에 assign된다.  
  
```verilog  
module blocking;  
	reg x, y, z;  
initial begin  
	#5 x = 1'b0;  
	#3 y = 1'b1;  
	#6 z = 1'b0;  
	end  
endmodule  
```  
  
5초 후 evaluation → x assign → 3초 → evaluate → y assign → 6초 → evaluate → z assign  
  
### Nonblocking assignment  
  
```verilog  
module nonblocking;  
	reg x, y, z;  
initial begin  
	x <= #5 1'b0;  
	y <= #3 1'b1;  
	z <= #6 1'b0;  
	end  
endmodule  
```  
  
모든 value들이 동시에 evaluate. 모든 값들은 block 마지막에 assign된다.  
  
→ 3s에 y assign → 5초에 x assign → 6초에 z assign  
  
```verilog  
module blocking;  
	reg x, y, z;  
initial begin  
	#5 x <= 1'b0;  
	#3 y <= 1'b1;  
	#6 z <= 1'b0;  
	end  
endmodule  
```  
  
3초에 1 evaluate 후 assign → 5초에 0 evaluate 후 assign → 6초에 0 evaluate 후 assign  
  
<aside> 📖  
  
이 부분이 헷갈림. assign은 마지막까지 가야 진행되는 것이라면 이렇게 행동해서는 안됨.  
  
베릴로그로 확인하기  
  
</aside>  
  
---  
  
### Example  
  
```verilog  
always @(*) begin  
	p = a ^ b;  
	g = a & b;  
	s = p ^ cin  
	cout = g | (p & cin);  
end  
```  
  
1. a, b, cin = 0 and a became 1!  
2. p = a ^ b, p = 1;  
3. g = a & b, q = 0;  
4. s = p ^ cin: s = 1 (because p has assigned to 1 in 1.)  
5. cout = g | (p & cin): cout = 0  
  
<aside> 📖  
  
여기서도 p가 바뀌는데 동시에 되기 때문에 always block이 다시 실행되지 않는걸까?  
  
delay가 p assign 시에 있었다면 무한 loop를 돌 여지가 있을까?  
  
</aside>  
  
```verilog  
always@(*) begin  
	p <= a ^ b;  
	g <= a & b;  
	s <= p ^ cin  
	cout <= g | (p & cin);  
end  
```  
  
1. a, b, cin = 0 and a became 1!  
2. Evaluate all RHS  
    1. a^b = 1  
    2. a&b = 0  
    3. p ^ cin = 0  
    4. g | (p& cin) = 0  
3. assign’em all!  
4. p가 바뀌었으니 다시 always block을 실행. (1,0,1,0)을 assign 함.  
  
---  
  
### Combinational Logic with Nonblocking assignment  
  
- 위의 경우, 같은 결과가 나오지만 nonblocking은 evaluate를 2번하기 때문에 느리다.  
  
<aside> 📖  
  
2번이 최대일까? 계속 값이 바뀐다면 3번 이상, 어쩌면 무한번 반복될 수 있을까?  
  
</aside>  
  
- 또, * 대신 일일히 값들을 써줬다면 wrong result를 낼 가능성이 높다.  
- 어떤 합성 툴은 시뮬레이션 값이 틀린 값이 나와도 하드웨어를 적절히 합성해준다.  
    - mismatched result를 야기할 수 있다.  
  
→ 그냥 combinational이면 Nonblocking 쓰지마!  
  
---  
  
### Race Condition  
  
example of swap  
  
```verilog  
always@(posedge clk) begin  
	x = y;  
end  
  
always@(posedge clk) begin  
	y = x;  
end  
```  
  
이 경우에는  
  
둘 중 하나가 먼저 assign되고, 그 다음에 해당 값을 다른 값이 복사하여 swap되지 않는다.  
  
<aside> 📖  
  
어떤 것이 먼저인지는 랜덤인가?  
  
</aside>  
  
각 timestep마다 evaluation된 값은 task queue로 들어갔다가 조건에 맞을 때 Javascript 엔진마냥 실행된다.  
  
```verilog  
always@(posedge clk) begin  
	x <= y;  
end  
  
always@(posedge clk) begin  
	y <= x;  
end  
```  
  
이 때는 x, y가 미리 한번에 evaluate되고 x, y에 assign되기 떄문에 swap이 가능하다.  
  
이는 nonblocking assignment는 해당 timestamp에 발생하는 모든 RHS를 모아서 한번에 처리하기 때문이다.  
  
shifter등을 구현할 때에도 유용하다.  
  
```verilog  
module shifter(input clk, input sin, output reg[3:0] out);  
  
always@(posedge clk) begin  
	qout[0] <= sin;  
	qout[1] <= qout[0];  
	qout[2] <= qout[1];  
	qout[3] <= qout[2];  
end  
  
endmodule  
```  
  
위에서 blocking을 썼다면 sin의 값이 qout에 복사되는 대참사가 벌어진다.  
  
---  
  
### What happens in conditional?  
  
```verilog  
always @(posedge clk) begin  
count = count - 1;  
if(count == 0) finish = 1;  
end  
  
always @(posedge clk) begin  
count <= count -1;  
if(count == 0) finish <= 1;  
```  
  
blocking에서는 count가 0으로 assign되고 if문을 실행하기 때문에 finish가 1이된다.  
  
nonblocking에서는 count-1 = 0으로 evaluation이 되고, finish = 1은 if(count ==0)을 만족하지 않아 아예 evaluate되지 않았다.  
  
따라서 finish는 0이다.  
  
⇒ 이후 clock에서는 count = 0이기 떄문에 실행되며 이는 1 clk 차이를 야기한다.  
  
---  
  
## 총정리  
  
- Sequential logic은 always@(clk) block + nonblocking  
- combinational logic은 blocking (dataflow modeling)  
- 복잡한 combinational logic은 always@(*) block + blocking  
- 하나의 값을 서로 다른 always에서 바꾸지 말기  
- 섞어 쓰지 말기