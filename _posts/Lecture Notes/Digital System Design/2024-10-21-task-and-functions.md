---  
tags:  
  - verilog  
  - task  
  - function  
share: "true"  
github_title: 2024-10-21-task-and-functions  
title: 7. Task and Functions  
date: 2024-10-21  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
개발자들은 항상 쉬운걸 원하고, 재사용하기를 원한다.  
  
→ Task and Function!  
  
Task: display, monitor등 system이 실행하는 업무  
  
Function: function name에 값을 저장해서 return  
  
## Task와 Function의 차이점  
  
||Tasks|Functions|  
|---|---|---|  
|Arguments|아무 숫자의 input, output, inout|최소 하나의 input.|  
|output을 가질 수 없음|||  
|Return Value|output, inout 등으로 여러개가 될 수 있다.|하나|  
|Timing control|posedge, # 등 가능|안됨 (이유는 아래)|  
|Execution|task가 실행되는 시간은 0보다 큼|function 실행에 걸리는 시간은 0임.|  
|Invoke functions and tasks|Function이나 task를 부를 수 있음|function만 가능|  
  
---  
  
## Functions  
  
function은 단일 값을 반환한다.  
  
`function [autoatic] [signed] [return_type] name ([port_list]);`  
  
function의 input을 정하는 방법은  
  
```verilog  
function automatic signed 4'b0000 function_name (input [7:0] data, output reg out);  
```  
  
와 같다.  
  
function은  
  
- 모듈 안에서 정의되며, `function` 과 `endfunction`  
- 하나의 ouput을 가지며  
- timing control은 못쓰며 (즉, combinational logic으로 밖에 못씀)  
- global signal을 drive할 수 있음.  
- function을 call할 수 있으나, task는 할 수 없음.  
  
---  
  
### Static vs Automatic  
  
static은 해당 함수 처음 실행될 때 global하게 한번만 생성되며 프로그램이 끝나면 종료된다.  
  
automatic은 해당 함수가 execute되었을 때 실행되며, 함수가 값을 리턴하면 사라진다.  
  
- automatic은 함수를 reentrant하게 만든다.  
- 이전 함수 실행이 실패했어도 다시 새로 생성하기 때문에 데이터가 오염될  
  
→ 베릴로그에서는 static이 default임에 유의하라.  
  
- Item allocation  
      
    - static → 정적으로 할당됨.  
    - automatic → 각 call마다 동적으로 할당됨.  
      
    Automatic 함수에 있는 item들은  
      
    hierarchial reference에서 불릴 수 없다. 즉, 다른 모듈에서 해당 함수를 참조할 수 없다. 다만, name으로 invoke될 수 있다.  
      
  
```verilog  
function [3:0] count_0s_in_byte(input [7:0] data);  
	integer i; // local variable  
	begin  
		count_0s_by_byte = 0; // temporal byte에 있는 값을 0으로 초기화0  
		for (i=0; i<=7; i=i+1) begin  
			if(data[i]==1'b0;) count_0s_by_byte = count_0s_by_byte + 1;  
		end  
	end  
endfunction  
```  
  
---  
  
### Recursive!  
  
```verilog  
module factorial(input [7:0] n, output [15:0] result);  
assign result = fact(n);  
  
function automatic [15:0] fact (input [7:0] N);  
	if(N == 1'b1) fact = 1'b;  
	else fact = N * fact(N-1);  
endfunction  
endmodule  
```  
  
만약 automatic이 아니었다면?  
  
→ 4 → 3_3 → 2_2_2 → 1_1_1_1 = 1!  
  
---  
  
## Constant Function  
  
elaboration time에 평가되는 함수!  
  
베릴로그의 실행단계는 다음과 같다.  
  
1. Compilation  
    1. 소스코드 읽기  
    2. 문법 체크  
    3. parsing step  
2. Elaboration  
    1. flatten out model hierarchy (모듈의 위계를 하나로 만듦.)  
    2. 파라미터 전달  
    3. constant function을 평가함.  
3. Simulation  
    1. 실제로 하드웨어로 만들고 시뮬레이션을 시작  
  
```verilog  
module RAM #parameter(RAM_DEPTH = 1024) (  
input [count_log_b2(RAM_DEPTH)-1:0] addr_bus  
output reg [7:0] data_bus  
);  
  
function integer count_log_b2(input integer depth);  
begin  
	count_log_b2 = 0;  
	while(depth) begin  
		count_log_b2 = count_log_b2 + 1;  
		depth = depth >> 1;  
	end  
end  
endfunction  
endmodule  
```  
  
---  
  
# Tasks  
  
- task는 여러개의 값을 리턴할 수 있는, 좀 더 자유로운 친구이다.  
  
```verilog  
task automatic name ([port list]);  
  
endtask  
```  
  
task는…  
  
- Input이든 output이든 몇개든 가질 수 있고  
- delay와 timing control이 가능하며  
- task나 function을 call할 수 있음  
- function처럼 a= task(b)는 불가능  
  
```verilog  
task count_0s_in_byte(input [7:0] data, output reg count);  
integer i;  
begin  
	count = 0;  
	for(int i=0; i<=7; i = i+1) begin  
		count = count + 1;  
	end  
endtask  
```  
  
<aside> 📖  
  
integer i를 꼭 body 바깥에 선언하는 이유가 있을까?  
  
</aside>  
  
→ for문이 포함된 task를 always 밖에서 실행하면 오류가난다.