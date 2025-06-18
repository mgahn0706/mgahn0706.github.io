---  
tags:  
  - verilog  
  - hierarchy  
share: "true"  
github_title: 2024-10-21-hierarchical-modeling  
title: 8. Hierarchical Modeling  
date: 2024-10-21  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
## Module definitions with Parameters  
  
```verilog  
module module_name [(#param)] [port]  
other dec.  
endmodule  
```  
  
---  
  
# Parameters  
  
파라미터는 elaboration step에서 평가된 후, 시뮬레이션에서는 해당 값을 넣게되는, 값이다.  
  
parameter는 delay를 특정시키거나 어떤 변수의 길이를 지정할 때 자주 쓰인다.  
  
종류는  
  
- module parameter  
- specify parameter  
  
가 있다.  
  
---  
  
### Parameter declaration  
  
가장 흔한 파라미터 정의 방식.  
  
defparam이나 모듈 # 등으로 override할 수 있다.  
  
```verilog  
parameter signed [3:0] mux_selector = 4'b0000;  
```  
  
→ parameter는 integer, time, real 등이 될 수 있다.  
  
---  
  
### Localparam declaration  
  
모듈에 local하게 parameter를 정한다.  
  
즉, defparam이나 module instantiation으로 덮어쓸 수 없음.  
  
---  
  
### Parameter Ports  
  
파라미터는 모듈 instantiation시에 넘겨줄 수 있는데,  
  
```verilog  
module module_name #(parameter SIZE = 7) (input [3:0] a);  
```  
  
와 같이 넘겨주어 사용할 수 있다. localparam으로 선언된 파라미터는 사용할 수 없다.  
  
---  
  
### Parameterized Module  
  
```verilog  
module counter #(PARAM = 4) (input [3:0] a);  
endmodule  
  
counter #(4) cnt_4bits(.a(a1)); // module initiatiation  
counter cnt_8bits(.a(a1));  
defparam cnt_8bits.PARAM = 8; // use defparam (old style)  
  
```  
  
Example: n - to - m decoder!  
  
```verilog  
module decoder_n2m   
#(parameter N = 3, parameter M = 8)  
(input [N-1:0] x, input enable, output reg [M-1:0] y);  
  
always@(*) begin  
	if(enable == 1'b1) begin  
		y = {M-1{0}, 1} << x;  
	end  
	else y = {M{0}};  
  
endmodule  
```  
  
---  
  
## Hierarchical Names  
  
각 identifier는  
  
- 모듈  
- 태스크  
- 함수  
- named block  
  
과 정의될 수 있다. 즉, 위계를 나타내며 pinpoint할 수 있다!  
  
```verilog  
4-bit-adder.fa_1.ha_1.xor1.s // 애더의 풀 애더의 하프 애더의 xor의 net s  
```  
  
단, automatic은 매번 실행마다 만들고 부수고 하기 때문에 pinpoint할 수 없다.  
  
---  
  
## Generate Block structure  
  
Generate block은 selection과 replication을 허용한다. (elaboration time에!)  
  
변수 선언, 함수 등 하드웨어 적으로 select하거나 replicate할 수 있다.  
  
- always block 안의 for loop은 sequential logic을 구현하기 위해 dynamic하게 평가된다.  
    - procedure 코드만 쓸 수 있고, continuous한 assign 사용 불가능  
- generate는 말 그대로 elaboration time에 해당 수만큼 반복하여 static한 하드웨어를 만든다.  
    - 단순 코드 반복이라 사용 가능  
  
|Aspect|`for` Loop in `always` Block|`for` Loop in `generate` Block|  
|---|---|---|  
|**Purpose**|Used for sequential behavioral logic|Used for generating repeated hardware|  
|**Timing**|Runs during simulation (dynamically)|Runs once during elaboration (statically)|  
|**Synthesis Impact**|Typically synthesizes into sequential logic|Unrolls into multiple hardware instances|  
|**Use Cases**|Looping over signals for calculations|Replicating hardware (wires, modules, etc.)|  
|**Triggering**|Triggered by an event (e.g., `posedge clk`)|Not event-driven; happens at synthesis|  
|**Code Generation**|Simulates like a software loop|Generates multiple instances of logic|  
|**Example**|Summing an array's values|Replicating registers or module instances|  
  
→ 이때, generate 안에서 사용하는 for문은 genvar를 써야함.  
  
→ 또, block 안에 name을 지정해줘야 hardware를 Pinpoint할 수 있음.  
  
---  
  
### Generate Loop Construct  
  
- begin 뒤에 name을 꼭 쓰기.  
- genvar로 인덱싱하기  
- 즉, genvar는 시뮬레이션에서 존재하지 않는다.  
- for loop은 같은 genvar를 쓰면 nested될 수 없다.  
  
---  
  
```verilog  
module adder_nbit #(parameter N = 4)  
(input [N-1:0] x, y;  
 input cin,  
 o  
```