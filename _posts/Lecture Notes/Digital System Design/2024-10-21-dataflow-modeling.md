---  
tags:  
  - verilog  
  - dataflow  
share: "true"  
github_title: 2024-10-21-dataflow-modeling  
title: 4. Dataflow Modeling  
date: 2024-10-21  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
Dataflow modeling은 primitive gate 대신 operator를 쓰는 설계 방식이다.  
  
## Continuous Assignment  
  
- net에 값을 drive하는 것  
- always active - RHS가 변하면 값이 항상 바뀐다.  
- combination logic에 유용  
  
```verilog  
assign [drive_strength] [delay] <net_expression> =   
different signals or constant value  
```  
  
```verilog  
wire out;  
assign out = 1'b1; // explicit (기본적인 continuous assignment)  
  
wire out = 1'b1; // implicit  
  
assign out = 1'b; // implicitily makes wire  
```  
  
- net은 한번만 declare되어야함  
  
---  
  
## Delays  
  
evaluation과 assignment 사이의 시간 간격  
  
- regular continuous  
- implicit continuous  
- net delay  
  
시뮬레이션에서도 쓸 수 있는데,  
  
- Inertial delay  
    - 소자 내의 RC (내부 delay)를 구현  
- Transport delay  
    - net delay와 같음  
  
---  
  
### Inertial delay  
  
```verilog  
wire in1, in2, out  
assign #10 out = in1 & in2;  
  
또는  
  
wire #10 out = in1 & in2; // assign이 생략되었다고 가정  
```  
  
in1과 in2가 T ~ T+12까지 유지되는 신호라고 하자.  
  
out은 T+10부터 T+22까지 유지된다.  
  
만약, T ~ T+2까지, 즉 delay보다 지속시간이 짧다면  
  
이는 out에 반영되지 않는다.  
  
→ Inertial delay는 회로 소자가 스파이  
  
### Net delay  
  
```verilog  
wire #10 out;  
```  
  
이러면 해당 net의 delay가 된다.  
  
in1, in2 지속시간에 관계없이 무조건 10초 후에 출력된다.  
  
---  
  
## Operators  
  
### Operators  
  
다른건 C와 똑같고, 알아둘 것만 적겠다.  
  
- << : logical left shift  
      
- > > : logical right shift  
      
- <<< : arithmetical left shift  
      
- > > > : arithmetic right shift : sign 부호를 유지해준다.  
      
- &, |, ^를 앞에 쓴다 = Reduction, 벡터를 스칼라 하나로 압축시킴.  
      
    - ex) &4’b0001 = 0  
- &를 하나만 가운데 쓴다 = bitwise operation  
      
    - ex) 4’b0001 & 4’b1101 = 0001  
- &&로 쓴다 = 값으로 보고 계산  
      
    - ex) 110 && 101 = 1  
- === : case sensitive equality  
      
  
---  
  
### Constants  
  
상수에는 세가지 타입이 있다.  
  
- real  
- integer  
- string  
  
reg와 다르게 integer는…  
  
- 기본적으로 32비트 ‘signed’ 값이다.  
  
**Base format notation**  
  
- 기본적으로 unsigned임.  
      
    - 16’babcd = 1010_1011_1100_1101  
    - 2006 = 32bit decimal  
    - 4’sb1001 = 1001을 signed로 해석하라. -0111, 즉 -7  
    - 5’sb1001 = 01001을 signed로 해석하라. +1001 즉, 9  
    - -4’sb1001 = 1001을 sign으로 해석하고 부호를 바꾸어라.  
        - -(-0111) = 7  
      
    ⇒ s 표시는 결국 어떻게 해석하느냐에 대한 문제이다.  
      
  
More examples  
  
- 4’shf = (1111)을 signed로 해석하시오 = -0001 = -1  
- 3’sd12 = (1)100 을 signed로 해석하시오. = -100 = -4  
- -4’sd12 = 1100을 signed로 해석하고 부호를 바꾸시오. = -0100 = -(-4) = 4  
- -4’sb0010 = -0010 = -2  
  
---  
  
## Variable Data types  
  
(1) reg  
  
unsigned by default  
  
```verilog  
reg a, b;  
reg [7:0] data_a; // MSB ... LSB  
reg [0:7] data_b; // LSB ... MSB  
```  
  
<aside> 📖  
  
data_b = data_a 하면 오류나나?  
  
</aside>  
  
(2) integer  
  
기본 32비트 decimal 값.  
  
→ 얘는 range를 쓸 수 없다. 이미 벡터이다. 즉, integer [1:0] a가 불가함.  
  
```verilog  
integer i, j;  
integer array [7:0] // 8개의 정수 배열  
```  
  
(3) time  
  
시뮬레이션 타임 정보 저장용. unsigned integer이고 64비트 저장함.  
  
(4) real, realtime  
  
기본적으로 실수 값.  
  
range 정의 불가.  
  
---  
  
## Vectors  
  
- endiannes [high: low] or [low:high]  
  
둘다 상관없는데 기본으로 [high:low]가 직관적임.  
  
→ 다른 곳에 쓸 때에도 순서를 맞춰야하고 맞추지 않으면 컴파일 에러남.  
  
---  
  
### Bit-select, part-select  
  
(여기서는 integer까지 허용)  
  
- wire [15:0] h_to_l;  
    - h_to_l[8+:8] ⇒ 8 9 10 11 12 13 14 15, 즉 [15:8]  
    - h_to_l[7-:8] ⇒ 7 6 5 4 3 2 1 0 [0:7]  
- wire [0:15] l_to_h;  
    - l_to_h[8+:8] ⇒ 8 9 10 11 12 13 14 15  
  
이런식으로 select한다.  
  
---  
  
### Array  
  
vector와 size 쓰는 부분이 다름에 주의!!  
  
```verilog  
reg a [1:0] // 1-d array  
wire [7:0] mem [15:0] // 16 of 8-bit array  
  
reg [3:0] state [3:0];  
state[1:0] = {4'b0000, 4'b1111}; // illegal!. vector에서만 가능  
```  
  
---  
  
## Relational Operators  
  
operand 중 하나만 unsigned면 그 식은 둘다 unsigned로 처리됨.  
  
```verilog  
wire signed [3:0] a = -4'd4;  
wire unsigned [3:0] b = 4'd5;  
  
a = 1100  
b = 0101  
a > b = true! (unsigned로 처리됨)  
```  
  
<aside> 📖  
  
display에서 signed로 하고 싶다면 어떻게 해야할까  
  
</aside>  
  
만약 사이즈가 다르다면,  
  
- 둘다 signed였다? → sign-bit extension + signed comparison  
- 어느 하나가 unsigned였다? → zero-bit extension  
  
---  
  
## Equality  
  
== 는 bit-by-bit operation.  
  
사이즈가 다르다면 sign-bit or zero-padding  
  
===는 x와 z도 체크하는데 합성 가능하지 않음.  
  
<aside> 📖  
  
그렇다면 signed 2’b11 == signed 3’b111 은 true지만, signed 2’b11 == 3’b111은 false이겠군.  
  
</aside>  
  
---  
  
### Concatenation, Replication  
  
```verilog  
module four_bit_adder  
(input [3:0] x, input [3:0] y, input cin, output [3:0] sum, output cout);  
  
assign { cout, sum } = x + y + cin;  
  
endmodule;  
  
```  
  
```verilog  
module twos_adder  
(input [3:0] x; input [3:0] y, input c_in, output [3:0] sum, output cout);  
wire [3:0] t;  
assign t = y ^ {4(c_in)};  
assign {cout, sum} = x + t + c_in; // t + c_in is -y when c_in = 1  
endmodule  
```  
  
---  
  
## Conditional Operator  
  
- expression ? true_exp : false_exp;  
  
조건에 따라 evaluate된다. 즉, conditional expression이 ev → 결과에 따라 true 또는 false expression이 evaluate된다.  
  
<aside> 📖  
  
그러면 always@(posedge clk) begin  
  
condition < = 1’b1;  
  
result < = (condition == 1’b1 ? a : b);  
  
end 는 어떤 순서로 evaluation될까?  
  
</aside>  
  
---  
  
## Reduction  
  
- vector를 scalar로 합쳐줌.  
- bit-by-bit으로 오른쪽부터 왼쪽으로 계산.  
- parity에 유용  
  
---  
  
## Logical  
  
- 각 값을 truthy, falsy하게 보고 계산  
  
ex) a = 123 || 0 ⇒ 1;  
  
- x, z는 falsy하지만, x로 계산될 것임.  
- negation은 ! 임에 유의  
  
---  
  
## Bitwise operator  
  
- negation은 ~임에 유의  
- 길이가 다르면 zero padding or signed extension.  
  
---  
  
## Shift  
  
- Logical : Bitwise, vacant will be zero  
- Arithmetic: <<< >>>  
    - left shift는 빈 곳에 0이 들어온다. 즉, 부호가 보존되지 않는다.  
    - right shift는 sign부호를 복붙한다.  
        - 정확히는, signed 로 저장되었는지 여부에 따라 0인지 1인지를 결정한다.  
  
```verilog  
-4d'3  = 1011 = display = '13' = >>> = 0110  
-4s'd3 = 1011 = display = '-3' = >>> = 1101  
```