---  
tags:  
  - cpu  
  - performance  
  - throughput  
share: "true"  
github_title: 2025-04-06-performance  
title: 6. Performance  
date: 2025-04-06  
categories:  
  - Lecture Notes  
  - Computer Architecture  
---  
## Latency VS Throughput  
  
- Latency: 하나의 명령어를 시작해서 끝내는데 까지 걸린 시간  
- Throughput: 단위시간당 끝마친 작업의 수  
  
동시에 작업을 수행할 수 있다면 항상 latency가 throughput의 역수는 아니다.  
  
bus는 latency는 큰데 thorughput은 큼. racecar는 지연은 작지면 thorughput도 작음  
  
---  
  
## IPC, MIPS, and GHz  
  
- IPC: Instruction per cycle. 한 사이클 당 몇 명령어를 수행하는가  
- CPI: cycle per insturction. 명령어당 평균 몇 사이클 먹는가  
- MIPS: million instruction per second. 초당 몇백만의 명령어를 수행하는가  
- GHz: 10^9 cycles per second  
  
### Iron Law  
  
wall clock time = (time/cyc) * (cyc/inst) * (inst/program)  
  
⇒ 하지만 이건 single-core latency-performance only  
  
---  
  
### FLOPS  
  
런타임 당 floating point 계산 얼마나 하냐의 지표  
  
FFT나 AI, 물리, 시뮬레이션 등에는 아주 유용하게 쓰인다. 하지만, 일반적인 지표는 아니다.  
  
---  
  
### Multi-dimensional Comparisons (Runtime, Energy…)  
  
- Power = Energy / Time.  
- But now we care only performance  
  
---  
  
## Relative Performance  
  
Performance = 1 / Time  
  
But, this expression is quite unclear..  
  
> If X is 50% slower than Y, TIme x = 1s, Time Y?  
  
So, we need fixed standard.  
  
X is `n times faster` than Y  
  
n = Performance X / Performance Y  
  
= Throughput X / Thorughput Y  
  
**= Time Y / Time X**  
  
X is `m % faster` than Y  
  
(1+ m/100) = Performance X / Performance Y  
  
- speedup도 Time y / Time x 로 얘기한다.  
  
---  
  
## Amdahl’s Law  
  
**성능을 더 빠르게 만들려고 개선한 부분이 전체 실행 시간에서 차지하는 비율이 낮으면, 전체 성능 향상 효과는 거의 없다** 는 걸 수식으로 보여주는 법칙  
  
Time_old = f + (1-f), where f = 쓰고자 하는 기술이 적용되는 비율  
  
Time_new = f/Sf + (1-f)  
  
Speedup = Time_old / tim_new  
  
f가 너무 작으면, Sf는 Speedup에서 무시할만하다.  
  
따라서, 메모리 로드같이 f가 큰 부분을 최적화해야한다. Make common case faster!  
  
---  
  
## Summarizing Performance  
  
X와 Y의 성능을 테스트한다고 했을 때,  
  
어떤 응용 프로그램은 X가, 어떤건 Y가 빠를 수 있다.  
  
따라서 우리는 `summarize`를 해야한다.  
  
- 목적에 따라 의미있는 값들이 있을 수 있다.  
  
### Arithmetic Mean  
  
단순히 모든 앱 실행시간을 더한 다음에 나눔.  
  
→ 단순하지만, 실행시간이 긴 프로그램이 더 많은 기여를 함.  
  
만약, 각 프로그램이 서로 다른 빈도로 실행된다면? (printf같은거는 엄청 많이 실행되니까)  
  
→ 특히, 가장 많이 실행되는 프로그램이 실행시간이 매우 짧으면 문제가 된다.  
  
→ 가장 많이 실행되는건 짧은 프로그램임에도 불구하고, 가장 길게 실행되는 것이 성능에 bias를 준다.  
  
### Weighted Arithmetic Mean  
  
각 프로그램마다 중요도를 두어, weight를 곱해서 더하자  
  
기준:  
  
실행빈도: 자주 실행되는 것이 중요하다  
  
중요도: 실제로 보이는 것이 중요하다.  
  
⇒ 결국 weight를 부여하는 사람의 주관이 들어간다.  
  
### Geometric Mean  
  
Time X / Time Y를 각 프로그램마다 구한 뒤, 모두 곱하고 n-제곱근을 취한다.  
  
- reference machine에 대한 성능을 아주 쉽게 체감 가능  
  
Nintendo Switch 2 / Nintendo Switch = 2. 아 2배 빠르구나~  
  
- 상대적 비율을 잘 반영함. 산술평균은 어느 한 프로그램이 빠른데 다른 부분이 느리면 이를 반영하지 못함  
    - (0.5 + 200) = 100배 빠른건가? 아님.  
    - 기하평균은 sqrt(0.5*200) = 10배 빠르다.  
  
### Harmonic Mean  
  
Do not take arithmetic mean of `rates` (Throughput)  
  
30km/h와 60km/h의 평균은 45km/h가 아니다.  
  
역수의 평균을 취하고 다시 역수를 하는 방식.  
  
Note: IPC에는 조화평균을 써야한다.  
  
Instruction per cycle: 높을수록 좋은, 클럭 사이클당 얼마나 많은 명령어는 차지하는지야.  
  
단순히 산술평균으로 해버리면, 각 프로그램이 모두 같은 실행시간이라고 가정하는 셈이라, 왜곡을 할 수 있다. 즉, 평균 IPC를 위해서는 n개의 프로그램을 동일하게 실행한 것을 잘 반영할 수 있다.  
  
평균 IPC = 1 / 평균 CPI (이게 더 자연스러움)  
  
= (실행 프로그램 수) / (CPI들의 합)  
  
= (실행 프로그램 수 ) / IPC의 역수들의 합  
  
= IPC의 조화평균  
  
---  
  
### Standard Benchmark  
  
- 근데 사람마다, 사용자마다 다른 응용 프로그램을 상정함.  
- 사실 어떤 프로그램들은 네 머신에서 안돌아갈 수 있음.  
  
→ SPEC benchmarks  
  
- 실제로 사용되고, 일반적 목적의 응용프로그램들을 잘 뽑아놓은 집합  
- 완벽하진 않아도, 같은 규칙에서 성능을 평가한다는 점에서 의미 있다.  
  
ex) CINT2006 (정수계산용), CFP2006 (소수점 계산이 많은 프로그램들), SPECratio (Sun UltraSparc II 칩에 대한 기하 평균)  
  
- 성능을 어떻게 평가할 것인가? 라는 시험 체계를 의미한다고 생각하면 편함. 중간고사-기말고사 비율 등  
  
### Many workloads run  
  
- 컴파일러, 워드 프로세서 등은 다 workload.  
- 하지만 이 스펙트럼은 매우 넓음  
    - CPU intensive, memory intensive, IO…  
- 이렇게 시험 문제들을 모아놓은 문제집이라고 생각하면 편함. 중간고사 문제 들…  
- SPEC CPU, SPEC Web, PARSEC…