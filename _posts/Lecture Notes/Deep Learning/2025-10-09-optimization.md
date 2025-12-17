---  
tags:  
  - optimization  
  - gradient-descent  
  - noise  
  - EWMA  
  - batch  
  - deep-learning  
share: "true"  
github_title: 2025-10-09-optimization  
title: 3. Optimization  
date: 2025-10-09  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. Gradient-based Optimization  
  
**(1) Slope 기반 (Slope-based)**  
  
- Gradient 모으기 (Collect gradients) (vector) $\rightarrow$ **Gradient Descent**  
      
  
**(2) Curvature 기반 (Curvature-based)**  
  
- Hessian (matrix) $\rightarrow$ **Newton's Method**  
      
  
---  
  
### **Method of Gradient Descent**  
  
- $\hookrightarrow$ **First-order, iterative.**  
      
- $f(\theta)$: Target to minimize.  
      
  
### **Newton's Method**  
  
- $\hookrightarrow$ **Zero-finding**  
      
    - $\theta \leftarrow \theta - \epsilon \cdot \frac{\partial f}{\partial \theta}$ (Gradient Descent)  
          
    - $x_{t+1} = x_{t} - \frac{f(x_{t})}{f'(x_{t})}$ (Newton's root finding)  
          
- $\hookrightarrow$ **Minimization**  
      
    - $x_{t+1} = x_{t} - \frac{f'(x_{t})}{f''(x_{t})}$  
          
    - Note: $\frac{1}{f''(x_t)}$ acts as learning rate.  
          
- **Guarantees only local minima.**  
      
    - (Initial location is critical)  
          
- **Issues**:  
      
    - $nC_2$ is unbearable.  
          
    - 직관 (Intuition): 멀리 (Far jump based on curvature).  
          
    - $f: \mathbb{R}^n \rightarrow \mathbb{R}$, $\theta \leftarrow \theta - H^{-1}\nabla f$  
          
    - $H_f = \begin{bmatrix} \frac{\partial^2 f}{\partial x_1^2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\ \vdots & \ddots & \vdots \end{bmatrix} \in \mathbb{R}^{n \times n}$  
          
    - **O($n^2$) space!**  
          
    - Covariance matrix are needed: $C_{ij} = Cov(X_i, X_j)$, $C \in \mathbb{R}^{n \times n}$.  
          
    - $H^{-1}$를 구하려면 **O($n^3$) operation**.  
          
  
---  
  
### **2. Gradient Noise**  
  
**[Diagram: Trajectory of W]**  
  
- Smooth curve vs Wiggly curve (SGD)  
      
- **Stochastic**: On a set of $m$-examples.  
      
- $\hat{g} = \frac{1}{m} \nabla_{\theta} \sum_{i=1}^{m} L(y^{(i)}, \hat{y}^{(i)})$  
      
  
### **Optimize in DL**  
  
- Training이 제일 힘듦 (Training is the hardest).  
      
- **Stochastic Gradient Descent (SGD)**  
      
  
**Gradient Descent Steps**  
  
1. $\hat{g} =$ an estimate of gradient (avg. gradient).  
      
2. $\theta \leftarrow \theta - \epsilon \hat{g}$  
      
  
**But suffer from...**  
  
1. **Local minima**: Zero gradient.  
      
2. **Gradient noise**: (SGD path implies noise).  
      
3. **Poor condition of Hessian**: Half pipe shape.  
      
  
### **Reducing Noise**  
  
- **(1) Sample-wise**  
      
    - $m=1$ (SGD) $\rightarrow$ $1 < m < N$ (Mini-batch) $\rightarrow$ $m=N$ (Batch GD - expensive).  
          
    - Increasing batch size reduces noise ($1 \rightarrow 200$).  
          
- **(2) Time-wise**  
      
    - Moving average.  
          
    - **EWMA** (Exponentially Weighted Moving Average).  
          
  
---  
  
### **EWMA**  
  
- $v_t = \begin{cases} g_1 & t=1 \\ \alpha v_{t-1} + (1-\alpha)g_t & t > 1 \end{cases}$  
      
- $\rightarrow$ $v_t$: EWMA at time $t$.  
      
- $\alpha \in [0, 1]$: Constant smoothing factor.  
      
    - $\alpha = 0.9$: Smoother curve, adapts slowly.  
          
    - $\alpha = 0.5$: Adapts quickly.  
          
- **Expansion**:  
      
    - $v_t = (1-\alpha)[g_t + \alpha g_{t-1} + \alpha^2 g_{t-2} + \dots]$  
          
    - (Normalized sum: $\frac{g_t + \alpha g_{t-1} + \dots}{1 + \alpha + \alpha^2 + \dots}$)  
          
- **Interpretation**:  
      
    - $v_t \approx$ average over $\frac{1}{1-\alpha}$ last time points.  
          
    - Graph is shifted further.  
          
  
**Types of Moving Average**  
  
1. **SMA** (Simple Moving Average): $v_t = \frac{\hat{g}_t + \hat{g}_{t-1} + \hat{g}_{t-2}}{3}$  
      
2. **WMA** (Weighted Moving Average): $v_t = \frac{w_1 \hat{g}_t + \dots + w_3 \hat{g}_{t-2}}{\sum w_i}$  
      
    - Convolution with learned weight.  
          
    - $v_t = \alpha \hat{g}_t + (1-\alpha) v_{t-1}$ (Recursive).  
          
  
---  
  
### **Gradient Descent with Momentum**  
  
- (관성 느낌 - Like inertia)  
      
- $\hookrightarrow$ Compute EWMA of gradients and use it to update.  
      
- **Result**: Faster, less noise.  
      
  
Forms  
  
Let $g := \nabla_{\theta} J(\theta)$  
  
**(1) Standard Momentum**  
  
- $v \leftarrow \alpha v - \epsilon g$  
      
- $\theta \leftarrow \theta + v \Rightarrow \theta \leftarrow \theta - \epsilon (g + \frac{\alpha}{-\epsilon}v)$ ? (Note: Notation varies)  
      
  
**(2) Alternative Form**  
  
- $v \leftarrow \alpha v + (1-\alpha)g$  
      
- $\theta \leftarrow \theta - \epsilon v$  
      
  
**(3) Common Form**  
  
- $v \leftarrow \alpha v + g$  
      
- $\theta \leftarrow \theta - \epsilon v \Rightarrow \theta \leftarrow \theta - \epsilon (\alpha v + g)$  
      
- $\hookrightarrow \theta \leftarrow \theta - \epsilon (g + \text{constant} \cdot v)$  
      
  
**Note: Nesterov Accelerated Gradient (NAG)**  
  
- "Lookahead"  
      
- Calculate gradient at $\theta + \alpha v$ instead of $\theta$.  
      
  
---  
  
### **Per-Parameter Adaptive Learning Rate**  
  
- $\theta \leftarrow \theta - \epsilon_t \cdot g$  
      
- EWMA로 조절 (Adjust with EWMA).  
      
- 보폭도 달라져야 할텐데 (Step size should also change).  
      
  
**Motivation**  
  
- Vertical oscillations in steep directions.  
      
  
### **AdaGrad**  
  
- $\hookrightarrow$ Adapts learning rate.  
      
- Steep direction ($\frac{\partial J}{\partial \theta_i}$ large) $\rightarrow$ Slow down.  
      
- Gently sloped ($\frac{\partial J}{\partial \theta_j}$ small) $\rightarrow$ Speed up.  
      
- Formula:  
      
    - $G_t = G_{t-1} + g_t^2$  
          
    - $\theta \leftarrow \theta - \frac{\epsilon}{\sqrt{G_t + \delta}} \cdot g_t$  
          
- **Issue**: $G_t$ increases monotonically $\rightarrow$ Learning rate decreases to 0 (Stops learning).  
      
- (H를 안 구하고 이걸 해결할 수가 있나 - Can we solve this without finding H?)  
      
  
---  
  
### **RMSProp**  
  
- **AdaGrad for non-convex setting.**  
      
- Gradient accumulation to EWMA (최근값만 사용 - Use only recent values).  
      
- Exponentially decaying average.  
      
- Discard extreme past.  
      
- Note: Element-wise product ($g \odot g$).  
      
  
**Algorithm**  
  
- $r \leftarrow \rho r + (1-\rho) g \odot g$  
      
- $\theta \leftarrow \theta - \frac{\epsilon}{\sqrt{r+\delta}} \odot g$  
      
  
### **Adam**  
  
- $\hookrightarrow$ **RMSProp + Momentum + Bias Correction.**  
      
- First iterations: inaccurate (biased towards 0).  
      
  
**Steps**  
  
1. Calculate Gradient $g$.  
      
2. Momentum: $s \leftarrow \rho_1 s + (1-\rho_1)g$  
      
3. RMSProp: $r \leftarrow \rho_2 r + (1-\rho_2) g \odot g$  
      
4. **Bias Correction**:  
      
    - $\hat{s} = \frac{s}{1-\rho_1^t}$  
          
    - $\hat{r} = \frac{r}{1-\rho_2^t}$  
          
    - (원래 value보다 조금 크게 - Slightly larger than original)  
          
5. Update: $\theta \leftarrow \theta - \epsilon \frac{\hat{s}}{\sqrt{\hat{r} + \delta}}$  
      
  
---  
  
### **Learning Rate Scheduling**  
  
- Gradient based: SGD, SGD+Momentum, AdaGrad, RMSProp, Adam.  
      
- $\Rightarrow$ Need gradually decrease over time!  
      
- **Decay**: Step decay, Exponential decay.  
      
    - Loss vs Epoch graph showing drops (decay).  
          
  
### **Learning Rate Warm-up**  
  
- **Linear scaling rule**: When mini-batch size $m$ increases by $k$, learning rate should increase (multiply by $k$) to converge faster (분산 정복).  
      
- **Warm up**: Low learning rate at start of training.  
      
    - $\hookrightarrow$ Early optimization difficulty 극복 (Overcome).  
          
    - $\hookrightarrow$ 크게 크게 가도 됨 (Can go with larger steps later).  
          
  
### **Problem of Adaptive Learning Rate**  
  
- $\hookrightarrow$ **Its variance**.  
      
- Variance is large in early stage $\rightarrow$ Bad local minima.  
      
- **RAdam (Rectified Adam)**: Rectifies variance of adaptive learning rate.  
      
  
---  
  
### **Loss Landscape and Generalization**  
  
- **Sharp minima**: Fast convergence, but poor generalization.  
      
- **Flat minima**: Slow convergence, **better generalization**.  
      
  
### **SAM (Sharpness-Aware Minimization)**  
  
- $\hookrightarrow$ Minimizes loss value & loss sharpness.  
      
- **Def**: $\text{Sharpness} = \max_{||\epsilon||_2 \le \rho} (L(\theta+\epsilon) - L(\theta))$  
      
- Maximizes error in neighborhood, then minimizes that.  
      
- Better generalization, but additional computation.  
      
  
---  
  
### **Large-batch Training**  
  
- **Large batch** $\rightarrow$ $\hat{g}_{t+1}$ accurate $\rightarrow$ **Faster convergence**.  
      
    - Pros: Decrease training time by parallelization (GPU).  
          
- **But weaker regularization** (less noisy batch).  
      
    - Cons: **Generalization gap**.  
          
    - $\hookrightarrow$ Converge to sharp minima (Smaller batch is noisy, so escape $\rightarrow$ better generalization).  
          
  
**Solution: Ghost Batch**  
  
- Split a mini-batch into several small "ghost" batches.  
      
- **Diagram**:  
      
    - [Input Batch] $\rightarrow$ [Split] $\rightarrow$ [Ghost Batch 1, 2, ...] $\rightarrow$ [Net]  
          
    - Ghost batch (약간의 noise 발생 - Generates slight noise).