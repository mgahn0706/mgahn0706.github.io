---  
tags:  
  - linear-transformation  
  - vector-space  
share: "true"  
github_title: 2024-09-23-linear-transformations-and-matrices  
title: 2. Linear Transformations and Matrices  
date: 2024-09-23  
categories:  
  - Lecture Notes  
  - Signals and Systems  
math: "true"  
---  
# 1.1 Continuous - Time & Discrete-time  
  
- **Continuous-time signal:** $x(t)$, $t \in \mathbb{R}$  
      
- **Discrete-time signal:** $x[n]$, $n \in \mathbb{Z}$  
      
  
ex) RC circuit  
  
[회로도: 전압원 $v_s(t)$가 저항 $R$과 커패시터 $C$에 직렬로 연결됨. 출력 전압 $v_c(t)$는 커패시터 양단에서 측정.]  
  
- $Z_R = R$  
      
- $Z_C = \frac{1}{j\omega C}$  
      
  
**Note**  
  
- $\omega$ : 입력신호의 주파수 $(rad/s)$  
      
- $f$ : 초당회전 횟수 $(Hz)$  
      
  
**Recall**  
  
- In capacitor, $f \rightarrow ?$ ... $2\pi f = \omega$.  
      
- $f=0 \rightarrow Z_C = \infty$, open circuit ($V_c = V_s$)  
      
- $f=\infty \rightarrow Z_C = 0$, short circuit  
      
  
Transfer Function:  
  
$$\frac{V_c(j\omega)}{V_s(j\omega)} = H(j\omega) = \frac{\frac{1}{j\omega C}}{R+\frac{1}{j\omega C}} = \frac{1}{1+j\omega RC}$$  
  
Magnitude:  
  
$$|H(j\omega)| = \frac{1}{\sqrt{1+\omega^2(RC)^2}}$$  
  
---  
  
# 1.1.2 Signal energy & Power  
  
### Definition  
  
**Continuous-time signal**  
  
- $Energy = \int_{t_1}^{t_2} |x(t)|^2 dt$  
      
    - $E_{\infty} = \lim_{T \rightarrow \infty} \int_{-T}^{T} |x(t)|^2 dt$  
          
  
**Discrete-time signal**  
  
- $Energy = \sum_{n=n_1}^{n_2} |x[n]|^2$  
      
    - $E_{\infty} = \sum_{n=-\infty}^{\infty} |x[n]|^2$  
          
  
### Definition (Power)  
  
- $Power = \frac{1}{t_2 - t_1} \int_{t_1}^{t_2} |x(t)|^2 dt$  
      
    - $P_{\infty} = \lim_{T \rightarrow \infty} \frac{1}{2T} \int_{-T}^{T} |x(t)|^2 dt$  
          
- Discrete: $P = \frac{1}{2N+1} \sum_{n=-N}^{N} |x[n]|^2$  
      
    - $P_{\infty} = \lim_{N \rightarrow \infty} \frac{1}{2N+1} \sum_{n=-N}^{N} |x[n]|^2$  
          
  
**Remark**  
  
- If $P_{\infty} \neq 0 \Rightarrow E_{\infty} = \infty$  
      
- If $E_{\infty} < \infty \Rightarrow P_{\infty} = 0$  
      
  
---  
  
# 1.2 Transformation of indep. variable  
  
(1) Time Shift  
  
$$x[n] \mapsto x[n - n_0] \quad (n_0 \text{만큼 shift})$$  
  
- if $n_0 > 0$: **delay** (과거신호)  
      
- if $n_0 < 0$: **advance** (미래신호)  
      
  
(2) Time Reversal  
  
$$x[n] \mapsto x[-n]$$  
  
- $n=0$ 대칭 (카세트 reverse)  
      
  
**(3) Time Scaling**  
  
- $x[t] \mapsto x[2t]$ : 2배 빠르게 (compressed)  
      
- $x[t] \mapsto x[\frac{1}{2}t]$ : 느리게 (expanded)  
      
- to consider combined transformations... (순서 중요)  
      
  
---  
  
### 1.2.2 Periodic signals  
  
Definition  
  
If for $\forall t$ s.t.  
  
$$x(t) = x(t+T)$$  
  
$x(t)$ is periodic signal.  
  
$\Rightarrow x(t) = x(t+T)$ 를 만족하는 양수 $T$가 존재한다.  
  
- **Fundamental Period:** 주기 $T$ 중 최솟값 $T_0$.  
      
  
**Note**  
  
- **Fundamental frequency:** 주파수 중에 가장 작은 주파수 $\omega_0$.  
      
- **Is constant signal periodic?**  
      
    - $\rightarrow$ Yes, by definition. but no $T_0$ (undefined).  
          
  
### 1.2.3 Even & Odd signal  
  
**Def)**  
  
- **Even signal:** $x(-t) = x(t)$ (y축 대칭)  
      
- **Odd signal:** $x(-t) = -x(t)$ (원점 대칭)  
      
  
$\rightarrow$ We can decompose signal.  
  
$$Ev\{x(t)\} = \frac{x(t) + x(-t)}{2}$$  
  
$$Od\{x(t)\} = \frac{x(t) - x(-t)}{2}$$  
  
$$\Rightarrow x(t) = Ev\{x(t)\} + Od\{x(t)\}$$  
  
---  
  
# 1.3 Exponential & Sinusoidal signal  
  
$$x(t) = C e^{at} \quad (C, a \in \mathbb{C})$$  
  
**i) If $C, a \in \mathbb{R}$**  
  
- $a > 0$: Growing exponential  
      
- $a < 0$: Decaying exponential  
      
  
ii) If $a$ is pure imaginary number, $a = j\omega_0$  
  
$$x(t) = e^{j\omega_0 t} = \cos(\omega_0 t) + j\sin(\omega_0 t)$$  
  
(Euler's Formula)  
  
Ex) Find $T$ of periodic $e^{j\omega_0 t}$  
  
$$e^{j\omega_0 t} = e^{j\omega_0 (t+T)}$$  
  
$$e^{j\omega_0 t} = e^{j\omega_0 t} \cdot e^{j\omega_0 T}$$  
  
$$\Rightarrow e^{j\omega_0 T} = 1$$  
  
$$\Rightarrow j\omega_0 T = j2\pi n$$  
  
$$\therefore \omega_0 T = 2\pi n \quad \text{or} \quad T = \frac{2\pi}{|\omega_0|} \cdot n$$  
  
- **Fundamental period** $T_0 = \frac{2\pi}{|\omega_0|}$  
      
- 자연계에는 복소수가 없지만 계산 편의를 위해 복소수 signal 사용.  
      
    - $\hookrightarrow$ 실제 측정값은 real part. $Re\{x(t)\} = \frac{x(t) + x^*(t)}{2}$  
          
  
Energy & Power of Periodic Signal:  
  
$$E_{period} = \int_{0}^{T_0} |e^{j\omega_0 t}|^2 dt = \int_{0}^{T_0} 1 dt = T_0$$  
  
$$P_{period} = \frac{1}{T_0} \cdot E_{period} = 1$$  
  
### Harmonically related exponentials  
  
Def) 어떤 양수 주파수 $\omega_0$의 정수배 집합.  
  
$$\phi_k(t) = e^{jk\omega_0 t}, \quad k = 0, \pm 1, \pm 2, \dots$$  
  
Ex 1.5)  
  
$$x(t) = e^{j3t} + e^{j2t}$$  
  
(Change to one cosine function)  
  
$$= e^{j2.5t} (e^{j0.5t} + e^{-j0.5t})$$  
  
(conjugate 관계)  
  
$$= e^{j2.5t} (2 \cos(0.5t))$$  
  
$$= 2 e^{j2.5t} \cos(0.5t)$$  
  
### Generalized complex-exponential signals  
  
$$C, a \in \mathbb{C}$$  
  
$$C = |C| e^{j\theta}, \quad a = r + j\omega_0$$  
  
$$x(t) = C \cdot e^{at}$$  
  
$$= |C| e^{j\theta} \cdot e^{(r + j\omega_0)t}$$  
  
$$= |C| e^{rt} \cdot e^{j\theta} \cdot e^{j\omega_0 t}$$  
  
$$= |C| e^{rt} \cdot e^{j(\omega_0 t + \theta)}$$  
  
$$= |C| e^{rt} (\cos(\omega_0 t + \theta) + j\sin(\omega_0 t + \theta))$$  
  
[그래프: 진동하며 진폭이 지수적으로 커지는 파형]  
  
- $|C|e^{rt}$: 진폭 (Envelope)  
      
- $\omega_0$: 주파수 (Frequency)  
      
- $\theta$: phase offset  
      
  
---  
  
# Discrete-time Signal  
  
$$x[n] = C \cdot \alpha^n$$  
  
(physically meaningful even if $\alpha < 0$)  
  
**다음을 관찰하자.**  
  
1. $x[n] = \cos(\frac{2\pi}{12} n) \Rightarrow N_0 = 12$  
      
2. $x[n] = \cos(\frac{8\pi}{31} n) \Rightarrow N_0 = 31$  
      
3. $x[n] = \cos(\frac{1}{6} n) \Rightarrow N_0 = \frac{2\pi}{1/6} = 12\pi \dots \notin \mathbb{Z}$ (periodic 하지 않음)  
      
  
- discrete signal 에서는 $\omega_0 = 2\pi \times (\frac{m}{N})$ 꼴이어야만 periodic 하다.  
      
  
### Periodicity properties of discrete-time complex exponentials  
  
**Continuous-time signal** 에서는 $\cos(\omega_0 t)$  
  
- 주파수는 $\omega_0$이고, $\sim \infty$까지 의미가 있다.  
      
- $\Rightarrow \omega_0$가 다르면 신호의 의미가 다르다.  
      
- $\Rightarrow$ 음수 주파수는 회전 방향이 반대이다.  
      
  
**Discrete-time signal** 의 경우는 $\cos(\omega_0 n)$  
  
- 가장 낮은 주파수: $0$ (or $2\pi, \dots$)  
      
- 가장 높은 주파수: $\pi$ (or $3\pi, \dots$)  
      
- $\pi \sim 2\pi$ 까지는 주파수가 증가해도 주기가 길어지는 효과 (Aliasing).  
      
- 물리적인 의미는 $0$부터 $\pi$까지.  
      
  
---  
  
### Discrete-time signal fundamental period  
  
$$e^{j\omega_0 n} = e^{j\omega_0 (n + N_0)}$$  
  
$$e^{j\omega_0 n} = e^{j\omega_0 n} \cdot e^{j\omega_0 N_0}$$  
  
$$\Rightarrow e^{j\omega_0 N_0} = 1$$  
  
$$\Rightarrow \omega_0 N_0 = 2\pi m \quad (m \text{ is integer})$$  
  
$$N_0 = \frac{2\pi}{|\omega_0|} \cdot m$$  
  
- 이것이 정수가 되는 $m$을 찾아 계산.  
      
  
ex) $x[n] = \cos(\frac{8\pi}{31} n)$  
  
$$\omega_0 = \frac{8\pi}{31}$$  
  
$$N = \frac{2\pi}{(8\pi/31)} m = \frac{31}{4} m$$  
  
- For $N$ to be integer, let $m=4$.  
      
- $\therefore N_0 = 31$.  
      
  
### Harmonically related periodic exponentials (공통주기 N)  
  
$$\phi_k[n] = e^{jk(\frac{2\pi}{N})n}, \quad k = 0, \pm 1, \dots$$  
  
$\Rightarrow$ 어느 순간 같은 신호가 나올 것이다.  
  
proof)  
  
$$\phi_{k+N}[n] = e^{j(k+N)\frac{2\pi}{N}n}$$  
  
$$= e^{jk \frac{2\pi}{N} n} \cdot e^{j N \frac{2\pi}{N} n}$$  
  
이때 $e^{j 2\pi n} = 1$  
  
$$= \phi_k[n] \cdot 1 = \phi_k[n]$$  
  
$\Rightarrow$ $N$개의 서로 다른 harmonically related periodic exponentials 존재.  
  
---  
  
# 1.4 Unit Impulse & Unit step function  
  
(1) Unit Impulse (Discrete)  
  
$$\delta[n] = \begin{cases} 0 & n \neq 0 \\ 1 & n = 0 \end{cases}$$  
  
(2) Unit Step (Discrete)  
  
$$u[n] = \begin{cases} 0 & n < 0 \\ 1 & n \ge 0 \end{cases}$$  
  
**Thm (Relationships):**  
  
1. $\delta[n] = u[n] - u[n-1]$  
      
2. $u[n] = \sum_{k=0}^{\infty} \delta[n-k] = \sum_{m=-\infty}^{n} \delta[m]$  
      
  
Properties:  
  
3. $x[n]\delta[n] = x[0]\delta[n]$ ($n=0$ 에서의 sampling)  
  
4. $x[n]\delta[n - n_0] = x[n_0]\delta[n - n_0]$ ($n=n_0$에서의 sampling)  
  
### How about continuous-time?  
  
(1) Unit step  
  
$$u(t) = \begin{cases} 0 & t < 0 \\ 1 & t > 0 \end{cases}$$  
  
(Undefined at $t=0$, 이런 함수는 없으니 근사하자)  
  
(2) Unit Impulse  
  
$$\delta(t) = \frac{du(t)}{dt}$$  
  
[그림: 폭 $\Delta$, 높이 $1/\Delta$ 인 사각형 펄스 $\delta_{\Delta}(t)$]  
  
- $\delta(t) \approx \delta_\Delta(t)$  
      
- 넓이가 1로 일정, 적분시 값은 1이다.  
      
- $\delta(t) = \lim_{\Delta \to 0} \delta_\Delta(t)$  
      
- $\int_{-\infty}^{\infty} \delta(t) dt = 1$  
      
  
**What do $u(t)$ and $\delta(t)$ mean?**  
  
Note:  
  
$$u(t) = \int_{-\infty}^{t} \delta(\tau) d\tau = \int_{\infty}^{0} \delta(t-\sigma) (-d\sigma) \quad (\text{subst } \sigma = t-\tau)$$  
  
$$u(t) = \int_{0}^{\infty} \delta(t-\sigma) d\sigma$$  
  
**Properties:**  
  
1. $x(t)\delta(t) = x(0)\delta(t)$ ($t=0$ 에서의 신호만 남음)  
      
2. $x(t)\delta(t - t_0) = x(t_0)\delta(t - t_0)$ ($t=t_0$ 에서의 sampling)  
      
3. Sifting Property:  
      
    $$\int_{-\infty}^{\infty} x(\tau) \delta(t - \tau) d\tau = x(t)$$  
      
    (어차피 $\tau=t$ 일 때만 값을 가진다)  
      
    $$= x(t) \int_{-\infty}^{\infty} \delta(t-\tau) d\tau = x(t)$$  
      
  
Doublet (Derivative of Impulse):  
  
$$\delta'(t) := \frac{d\delta(t)}{dt}$$  
  
By convolution property, $\int_{-\infty}^{\infty} x(\tau) \delta(t - \tau) d\tau = x(t)$  
  
Let $\tau' = t - \tau$:  
  
$$\frac{d}{dt} \int_{-\infty}^{\infty} x(t - \tau') \delta(\tau') d\tau'$$  
  
$$= [x(t-\tau')\delta(\tau')]_{-\infty}^{\infty} - \int_{-\infty}^{\infty} x(t-\tau') \delta'(\tau') d\tau'$$  
  
(Integration by parts)  
  
$$= \int_{-\infty}^{\infty} x(t-\tau') \delta'(\tau') d\tau'$$  
  
(디렉 델타가 1번 미분)  
  
$$\frac{dx(t)}{dt} = \int_{-\infty}^{\infty} x(t-\tau') \delta'(\tau') d\tau'$$  
  
Generalize:  
  
$$\frac{d^n x(t)}{dt^n} = \int_{-\infty}^{\infty} x(t - \tau') \delta^{(n)}(\tau') d\tau'$$  
  
: 자기자신보다 다른 signal 과 결합할 때 의미가 있다.  
  
---  
  
**Q. How can I prove $\frac{d^{2}x(t)}{dt^{2}} = \int_{-\infty}^{\infty} x(t-\tau') \delta^{(2)}(\tau') d\tau'$ ?**  
  
# 1.5 Continuous-Time and Discrete-Time systems  
  
- Continuous: $x(t) \to \boxed{\text{System}} \to y(t)$  
      
- Discrete: $x[n] \to \boxed{\text{System}} \to y[n]$  
      
  
Ex 1.11 Simulation  
  
Model: $\dot{y}(t) + ay(t) = bx(t)$  
  
Approximate derivative: $\dot{y}(t) \approx \frac{y(t) - y(t-h)}{h}$  
  
$$\frac{y(t) - y(t-h)}{h} + a y(t-h) = b x(t)$$  
  
$$y(t) = (1 - ha) y(t-h) + hb x(t)$$  
  
Convert to discrete ($t \to n$, $t-h \to n-1$):  
  
$$y[n] = (1 - ha) y[n-1] + hb x[n]$$  
  
- $y(t-h) \approx y[n-1]$ : 한 sample 이전의 값. 미소 시간 전만큼의 값.  
      
- 근사 가능!  
      
  
---  
  
# 1.6 Basic System Properties  
  
### (1) Memory  
  
- **Memoryless system:**  
      
    - Ex: $y[n] = 2x[n] - x^2[n]$  
          
    - Ex: $y(t) = Re(x(t))$ 등. 해당시간의 input에만 영향을 받음.  
          
- **System with Memory:**  
      
    - Ex: $y[n] = \sum_{k=-\infty}^{n} x[k]$  
          
    - Ex: $y(t) = x(t) + x(t+1)$ 등. 과거나 미래 입력을 고려.  
          
    - Ex: $y(t) = \frac{1}{C} \int_{-\infty}^{t} i(\tau) d\tau$  
          
  
### (2) Invertibility  
  
- Invertible system:  
      
    $$x[n] \to \boxed{S} \to y[n] \to \boxed{S^{-1}} \to x[n]$$  
      
    If distinct inputs lead to distinct outputs.  
      
- **Non-invertible system:**  
      
    - Ex: $y[n] = 0$  
          
    - Ex: $y(t) = x^2(t)$ 등.  
          
  
### (3) Causality  
  
- **Causal System:** 출력이 입력의 현재와 과거 값에 의해서 결정된다. (non-anticipative).  
      
- **Non-causal System:** 미래값에 의해 결정.  
      
  
**Note**  
  
- All memoryless systems are causal.  
      
- Almost all real-life continuous systems are causal.  
      
- Discrete-time systems do not have to be causal. (Just wait. 모든 sample을 미리 받은 후 실행).  
      
  
**Ex)** $y[n] = \frac{1}{2M+1} \sum_{k=-M}^{M} x[n-k]$ (Moving Average)  
  
### (4) Stability  
  
[그림: (상단) 진자 운동 - 안정, (하단) 역진자 - 불안정]  
  
"BIBO": Bounded Input, Bounded Output.  
  
유한한 입력 $\rightarrow$ 유한한 출력.  
  
Ex: $y(t) = e^{x(t)}$  
  
i) $\forall |x(t)| < B \Rightarrow |y(t)| = |e^{x(t)}| \le e^{|x(t)|} < e^B < \infty$  
  
ii) $\exists t$ s.t. $|x(t)| < B \dots$ (내용 끊김, 불안정 조건 반례에 대한 언급으로 추정됨)  
  
### (5) Time Invariance  
  
$$x(t) \to \boxed{S} \to y(t)$$  
  
$$x(t - t_0) \to \boxed{S} \to y(t - t_0) \quad \text{for } \forall t_0$$  
  
$\therefore t_0$ delay $\rightarrow$ 출력도 $t_0$ delay : 언제 실험하든 같은 결과.  
  
**Diagram:**  
  
1. $x(t) \xrightarrow{\text{Shift}} x(t-t_0) \xrightarrow{\text{Sys}} Y_1$  
      
2. $x(t) \xrightarrow{\text{Sys}} y(t) \xrightarrow{\text{Shift}} y(t-t_0)$  
      
  
$$T \cdot S_{t_0} = S_{t_0} \cdot T \quad \text{일 때 Time-invariant.}$$  
  
### (6) Linearity  
  
1. **Additivity:** $x_1[n] + x_2[n] \to y_1[n] + y_2[n]$  
      
2. **Homogeneity:** $a x_1[n] \to a y_1[n]$  
      
  
**보이는 법:** $x[n]$ 대신에 $a x_1[n] + b x_2[n]$ 넣기