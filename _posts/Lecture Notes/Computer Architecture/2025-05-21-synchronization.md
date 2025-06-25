---  
tags:  
  - synchronization  
  - lock  
  - thread  
share: "true"  
github_title: 2025-05-21-synchronization  
title: 18. Synchronization  
date: 2025-05-21  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## Multithreading, Fork  
  
이건 시스템 프로그래밍에서 열심히 배웠으니 넘어가자  
  
---  
  
## Data race in shared memory  
  
if thread A, B has critical section, this should be atomic!  
  
→ We need to lock critical section.  
  
### Acquire(L)  
  
- if L == 0, set L ← 1 and advance to next line.  
  
### Release(L)  
  
- Set L ← 0  
  
```c  
Acquire(L)  
// critical section  
Release(L)  
```  
  
---  
  
## Atomic Read-Modify-Write  
  
- A special class of memory instruction. (=atomic instruction) is needed for synchronization  
  
```c  
Test&Set(addr, r):  
	r = M[addr];  
	M[addr] = 1;  
```  
  
```c  
Swap(addr, r):  
	temp = M[addr];  
	M[addr] = r;  
	r = temp;  
```  
  
```c  
Fetch&Add(addr, r):  
	r = M[addr];  
	M[addr] = r + 1;  
```  
  
```c  
Compare&Swap(addr, r1, r2):  
	if(r1 == M[addr])  
		Swap(addr, r2)  
```  
  
이것들이 atomic instruction으로, 다른 명령어가 끼어들지 않는다. RISC에는 안좋다.  
  
보통은 Test&Set으로 lock을 잡지만, 다른 명령어로 lock을 잡아볼까?  
  
---  
  
### Lock 잡기  
  
```c  
Acquire(L)  
do {  
	Test&Set(L, r_temp);  
	} while r_temp != 0;  
```  
  
```c  
Acquire(L)  
do {  
	r_temp <- 1;  
	Swap(L, r_temp);  
} while r_temp != 0;  
```  
  
```c  
Acquire(L)  
do {  
	Fetch&Add(L, r_temp);  
	} while (r_temp != 0);  
```  
  
```c  
Acquire(L)  
do {  
	r_comp <- 0; r_temp <- 1;  
	Compare&Swap(L, r_comp, r_temp);  
	} while (r_temp != 0);  
```  
  
---  
  
## Special Load and store  
  
- LL (load-locked)  
      
    - r ← M[addr];  
    - <flag, address> ← <1, addr>  
- SC (store-conditional)  
      
    - if <flag, address> = <1, addr> then  
        - M [addr] ← r;  
        - set status bit to succeed  
    - else  
        - set status bit to fail  
  
→ Each core has <flag, addr> register and status bits!  
  
---  
  
```c  
Test&Set(addr, r):  
loop: load-locked(r, addr);  
			store-conditional(1, addr);  
		if status_bit == failed, goto loop  
```  
  
→ 그냥 위에있는거 r에 저장하는건 load, M[addr]에 저장하는건 store로 감싸고 중간에 메모리 바뀐거 체크해서 loop 다시 돌리면 됨.  
  
---  
  
## Test-and-Test-and-set  
  
기존의 Test-and-set은 performance problem이 있다.  
  
항상 write 시도, cache invalidation 신호를 버스에 보낸다.  
  
→ Huge coherence traffic during spinning → Bus contention. + cache invalidation 유발  
  
매 loop마다 load → snooping bus에서 특히 느려진다.  
  
```c  
Acquire(L):  
   while(true):  
       load[L] -> original_value; // locally cached  
       if(original_value == UNLOCKED):  
	       old = test_and_set(LOCKED, L);  
	       if(old == UNLOCKED):  
		       break; // Lock acquired  
		    
```  
  
이러면 실제로 LOCK이 풀렸을 때만 test_and_set을 하기 때문에 요청이 줄어든다.  
  
---  
  
### Higher Performance & Fairness  
  
Test & Test & Set은 누가 잡을지 모른다. 어떤 CPU가 운빨로 잡으면 나머지 코어는 starve한다.  
  
→ ticket-lock 방식으로 하면 각 코어간 공정성을 확보할 수 있다. 이때 fetch&decrease 방식을 쓰며 내 번호가 될 때까지 기다렸다가 0이되면 write를 시도함으로써 test&set의 contention 및 invalidation 단점도 보완가능하다.  
  
---  
  
## Sequential Consistency  
  
1. Processors issue memory ops in `program order`  
2. Switching **randomly** after each memory op `provides single sequential order among all operations`  
3. Global memory 입장에서는 모두에게 똑같이 보임. 선택되는 순서가 모두에게 공개되어 보임.  
  
---  
  
### Problems  
  
- Difficult to implement in hardware  
- Unnecessary restrictive.  
- Conflicts with latency hiding techniques.  
  
### Store buffer  
  
- Load가 dependency가 없으면 먼저 나가자! store 명령은 메모리 접근 명령이라 오래걸릴 수 있다. 다만, program-order로 실행하면 주소간 dependency가 없더라도 기다려야하기 떄문에 사이클 낭비가 발생한다.  
- Load 앞에 store 명령어보다 먼저 나가므로, SC의 1번 원칙을 위배한다. → 어쩌지  
  
```c  
// Processor 1  
val1 = 1; // A1  
if(val2 != 0) { // A2  
 retry();  
}  
  
// Processor 2  
val2 = 1; // B1  
if(val1!=0) { // B2  
retry();  
}  
```  
  
위의 예시를 보자. 우리 write인 A1, B1이 엄~~~~~청 느리다고 하자.  
  
그러면 store buffer에 들어갈테고, 그 뒤에오는 A2, B2가 먼저 읽어버릴 것이다. (왜? dependency가 없거든) → 그러면 0과 0을 읽어버리고 retry를 못하게 된다. → critical section으로 둘다 들어가버림 → CHAOS  
  
---