---  
tags:  
  - verilog  
  - behavior  
share: "true"  
github_title: 2024-10-21-behavior-modeling-2  
title: 5. Behavior Modeling 2  
date: 2024-10-21  
categories:  
  - Lecture Notes  
  - Digital System Design  
---  
# Timing Controls  
  
```verilog  
reg a = #5 10; // Intra  
#10 reg a = 10; // Inter  
```  
  
timing control에는  
  
- delay control  
- event control  
  
이 있다.  
  
---  
  
## Delay control  
  
- delay가 음수라면 절댓값의 2’s complement를 취하고 unsigned로 읽는다.  
- ex) -2 ⇒ 1110 → 14  
  
### Inter-assignment delay  
  
해당 procedure의 execution 자체를 미룬다.  
  
```verilog  
#25 y <= ~x;            
#15 count <= count +1;  
```  
  
#25 → y < = ~x ⇒ #15 ⇒ count 증가  
  
즉, 같은 timestep에서만 동시에 execution 및 evaluation이 이루어진다.  
  
### Intra assignment delay  
  
```verilog  
y = #25 ~x;        // ~x를 0에 계산, 25에 y에 assign   
count = #15 count +1; // count + 1을 25에 계산, count에 40에 assign  
```  
  
```verilog  
y <= #25 ~x;             // ~x를 0에 계산, 25에 assign  
count <= #15 count +1; // count+1을 0에 계산, 15에 assign  
```  
  
---  
  
### Edge triggered event  
  
```verilog  
always@(posedge clk) begin  
	reg1 <= #25 in1; // evaluate in 0, assign in 25  
	reg2 <= @(negedge clk) in2; // evaluate in 0, assign when clk negedge  
	reg3 <= in1; // evaluate in 0, assign in 0  
end  
```  
  
---  
  
### Level sensitive event control  
  
```verilog  
begin  
	wait (!enable) #10 a = b;  
	#10 c = d;  
end  
```  
  
enable = 1 이면 #10 a = b;의 evaluation 자체가 미뤄진다.  
  
즉, 0이 될 때 10초를 기다리고 a = b가 실행된다.  
  
그 후 10초 뒤에 c = d 실행된다.  
  
wait사용 예시 ) handshake  
  
---  
  
## Selection Constructs  
  
여기는 Example이 더 많다.  
  
아래에 유의할 점 몇개만 남겨둔다. example들은 코드와 회로도 둘 다 연습하길 바란다.  
  
if - else는 MUX와 Counter의 enable에 자주 쓰인다.  
  
- combinational 에서는 unwanted latch를 조심할 것.  
- %, *를 쓰면 clock 범위에서 벗어날 수 있다.  
- case 문에 있는 S도 read하는 신호임에 유의하라.  
- casex  
    - x를 상관없는 값으로 보겠다.  
        - ex) casex(t)  
              
            4’bxxx1 : out = 0; // 0011 , 0001등이 잡힘.  
              
  
---  
  
## Loop constructs  
  
- always나 initial 안에서만 쓸 수 있음.  
- 여러개의 하드웨어 인스턴스를 만드는 것임.  
- 즉, loop 내의 하드웨어사 replicate된다.  
  
⇒ compile time에 반복 횟수가 정해져야 하며  
  
⇒ 리소스가 부족해서는 안된다.  
  
(1) While loop  
  
- while 조건이 false일 때 까지 execute  
  
```verilog  
while(i <= 7) begin  
	out = out + 1;  
	i = i + 1;  
end  
```  
  
위 코드는 out = out + 1;과 같은 코드이다. 즉, while이 내부 코드를 여러번 쓴 것과 마찬가지인 것으로 컴파일한다. 이래서 컴파일 타임에 횟수가 정해져야한다는 것이다.  
  
만약 위에서 non-blocking을 썼다면 결국 out < = out + 1을 7번썼다는 건데 그것은 timestep이 같기 떄문에 모두 1로 evaluation될 거이다.  
  
(2) for  
  
for도 마찬가지이며, 마지막에 update가 하나 더 생긴다고 보면된다.  
  
integer i는 실제 register로 만들어지지 않는다.  
  
for ( initial value, 종료 조건, 업데이트 코드)  
  
(3) repeat  
  
고정된 횟수만큼 block의 statement를 실행한다.  
  
```verilog  
repeat (32) begin  
	// some code  
end  
  
repeat (a) begin // a는 이 block이 오기 전에 evaluation이 되어있어야함.  
  
end  
```  
  
<aside> 📖  
  
만약 evaluate된 값이 repeat 블록 안에서 바뀌면 어떻게 될까?  
  
</aside>  
  
---  
  
(4) forever  
  
영원히 반복하는 것. $finish가 있을 때 까지.  
  
→ 합성 가능하지 않음.