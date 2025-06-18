---  
tags:  
  - verilog  
  - dataflow  
  - strutctural  
  - bahavioral  
share: "true"  
github_title: 2024-10-17-introduction-to-verilog  
title: Introduction to Verilog  
date: 2024-10-17  
categories:  
  - Introduction to Verilog  
---  
# Verilog is Hardware Description Language!  
  
## Module  
  
베릴로그의 main building block이다.  
  
모든 module은 input과 output을 가진다.  
  
- Core circuit  
    - 요구된 기능을 수행한다.  
- Interface (port)  
    - carries required communication  
  
```verilog  
module test (input a, input b, output y); // Don't forget to use semi-colon!  
  // some testing module codes!  
endmodule  
```  
  
위의 코드와 같이 모듈을 정의한다.  
  
---  
  
### Port declaration style  
  
(1) Old verilog style  
  
```verilog  
module test(a, b, y);  
input a;  
input b;  
output y;  
// some codes  
endmodule  
```  
  
(2) ANSI style  
  
```verilog  
module test(input a, input b, output y);  
//some codes  
endmodule  
```  
  
port 정의하는 방식은 두 가지 방식으로 나뉘는데, 아래처럼 쓰는게 오타나기도 어렵고 더 좋다 히히  
  
---  
  
### Software Programming vs hardware programming  
  
(1) Software programming  
  
각 statement 들을 program이 정의한 순서대로 실행한다.  
  
(2) hardware programming  
  
어떤 주어진 circuit을 기술하는 textform에 가까움  
  
예시) assign ⇒ RHS에서 LHS로 가는 어떤 data의 flow를 나타낸다. 오른쪽의 값이 왼쪽으로 할당된다고 해석하기 시작하면 파국이 일어남.  
  
---  
  
### Synthesizable  
  
Synthesis란: HDL 코드를 논리 게이트와 wire로 만드는 것 (netlists)  
  
코드를 synthesis하기 위해서는 베릴로그 코드가 synthesizable해야한다!  
  
⇒ initial은 합성 가능하지 않음.  
  
다만 Synthesizable 가능여부는 ASIC, FPGA 등 어떤 보드에 올리냐에 따라 달라지기 때문에 절대적인 개념이 아니다.  
  
---  
  
# Lexical Conventions  
  
대부분 C의 코드를 따라가는 베릴로그  
  
- Identifiers: c에서의 instance와 같음  
- keywords: assign, end, else 등…  
  
## Number Representation  
  
format: size ‘ value. ex) 8’b01101101;  
  
- **size**: 어떤 데이터의 사이즈를 지정함. 지정하지 않으면 32-bit  
- **base**: 이 값이 어떤 값으로 해석될지를 지정함. 지정하지 않으면 decimal  
    - b: binary  
    - o: octal  
    - d: decimal  
    - h: hexadecimal  
  
### Size  
  
→ 만약 실제 할당한 크기와 다른 값이 들어온다면?  
  
- (지정된 값이 너무 작음) : leftmost bit가 무시됨.  
    - ex) 4’b101111 = 4’b1111, 4’d12345 = 4’b2345  
- (지정된 값이 너무 큼): left most에 ‘0’이 채워짐, x나 z면 해당 값으로 채워짐  
    - ex) 4’b11 = 4’b0011. 4’bxx = 4’bxxxx  
  
### Unsized  
  
- 2007 → 32bit decimal.  
- ‘habc → 32bit hexadecimal.  
- ‘h1deadbeef → (0001) 이 없어짐  
  
<aside> 📖  
Need to check!  
</aside>  
  
### Negative number: -size’base value  
  
- 2’s complement format by default  
- -4’b1001 ⇒ 10111 로 저장되고, 해석할 떄는 -9로 해석함.  
- -16’habcd ⇒ -(1010_1011_1100_1101) ⇒ 0101_0100_0011_0011 로 저장.  
    - 즉, 이것을 16’h로 다시 읽으려고 하면 5433으로 읽힌다!  
  
---  
  
# Data types & Ports  
  
## Value sets  
  
- 1  
- 0  
- x (Unknown logic value)  
- z (high impedance)  
  
## Data types  
  
### Nets  
  
- Hardware connection point (값을 저장할 수 없다.)  
- 값이 통과하는 방향이 존재한다. wire a = b 이면 a로 b가 간다는 의미  
- ex) wire  
- 모듈 내 어떤 곳에서도 reference될 수 있다.  
- primitive나 assignment, port 등에서 driven되어야 한다.  
    - 보통 net 업데이트할 때 drive한다고 한다.  
  
### Variables  
  
- data storage elements (값을 저장할 수 있다.)  
- 꼭 physical register에 항상 대응되는 것은 아니다.  
    - 불필요한 reg라면 베릴로그가 알아서 지워주기 때문이다.  
- ex) reg, integer  
- 어디서나 reference될 수 있다.  
- 오직 procedual statement, task, function에서만 assigned될 수 있다.  
    - always block 안 등  
- input이나 inout port가 될 수 없다. (즉, in. 받아오는건 안되고 내보내기만 가능)  
    - continous한 값이 아니다!  
  
→ 그래서 위에서 잠깑잠깐 나온 continous와 procedure이 뭐냐?  
  
---  
  
## Verilog Assignment  
  
- 3가지가 있다.  
  
### Continuous Assignment  
  
- net으로 value를 drive하는 것  
- combinational logic을 짤 때 씀  
- (명시적으로 할 때에는) assign keyword를 쓴다.  
    - wire a;  
    - wire a= b;  
- (암시적으로 할 때에는) 그냥 바로 wire하기도 한다.  
    - wire a = b;  
  
### Procedural assigments  
  
- always block 안에서 reg에 저장된 값을 바꿔주는 것  
- register와 FSM 할 때 사용  
  
### Procedural Continuous assignment  
  
- 짬뽕  
- assign, deassign을 통해 override  
  
---  
  
### Ports  
  
1. input → net type  
2. output → net or var type  
3. inout → net type  
  
ex) Input signed [3:0] digits  
  
- port는 기본적으로 unsigned이다. (뭐 다른 것도 다 마찬가지이지만)  
  
**How to connect port**  
  
- By name  
    - .port_id1(port_expt_1) …  
- By positional association  
    - 위치 기반  
  
```verilog  
module half_adder(input x, input y, output s, output c);  
 // half-adder body  
xor xor1(s, x, y);  
and and1(c, x, y);  
endmodule  
  
module full_adder(input x, input y, input cin, output s, output cout);  
wire s1, c1, c2;  
half_adder(x, y, s1, c1);  
half_adder(.x(x), .y(y), .s(s), .c(c2));  
or or1(cout, c1, c2);  
endmodule   
```  
  
위와 같이 쓸 수 있다.  
  
---  
  
## Modelling 방식  
  
(1) Structual modelling  
  
- gate level  
- Built-in primitives  
- hierarchy를 기술  
  
```verilog  
module half_adder(input x, input y, output c, output s);  
xor xor1(s, x, y);  
and and1(c, x, y);  
endmodule  
```  
  
(2) Dataflow modelling  
  
- hardware를 Input과 output으로 기술  
- operator (+, -, &) 사용  
- continuous assignment 사용 - assign  
  
```verilog  
module full_adder(input x, input y, input c_in, output s, output c_out);  
	assign { c_out , sum } = x + y + c_in;  
endmodule  
```  
  
(3) Behavior modelling  
  
- sequential logic에 주로 사용  
- always block 사용  
- 꼭 reg여야 함.  
  
→ 보통 3개를 mixed한다.  
  
```verilog  
module full_adder(input x, input y, input c_in, output reg s, output reg c_out);  
	always @(*) begin  
		{cout, sum} = x + y + c_in;  
	end  
endmodule  
```  
  
RTL = synthesizable behavior model + dataflow constructs  
  
---  
  
## Simulation  
  
- $display - 값 출력  
- $monitor - 값 변화 감지  
- timescale  
    - `timescale time_unit / time_precision`  
    - timescale 1ns / 1ps 로 한다면, #15 = 15ns delay를 의미  
    - FPGA에서는 ns를 사용하는게 좋음