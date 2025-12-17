---  
tags:  
  - score-based  
  - deep-learning  
  - diffusion  
share: "true"  
github_title: 2025-12-01-score-based-model-1  
title: 13. Score-based Model 1  
date: 2025-12-01  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# Recall: Deep Generative Models  
  
## Likelihood-based  
  
- ① Autoregressive model  
      
- ② VAE  
      
- ③ Flow based model  
      
- **Diffusion model (score-based)**  
      
  
## Likelihood free  
  
- GAN  
      
  
# Diffusion Model  
  
- ↳ Tractability flexibility trade off  
      
- [Learn]  
      
    - Data $\leftrightarrow$ Noise  
          
  
# 7 Fundamentals!  
  
### (1) Forward process & Reverse process  
  
- **Forward diffusion (predefined)**  
      
    - $\text{Data } [\mathcal{X}] \rightarrow \cdot\cdot\cdot \rightarrow \boxed{\text{noise } [\mathcal{N}(0, I)]}$  
          
- **Reverse diffusion (learned)**  
      
  
### (2) Diffusion steps  
  
- Data  
      
    - $\begin{bmatrix} X_0 \\ \mathcal{X} \end{bmatrix} \rightarrow \cdot\cdot\cdot \rightarrow \begin{bmatrix} X_T \\ \mathcal{N}(0,I) \end{bmatrix}$  
          
    - $t=0 \dots T$  
          
  
### (3) Signal & Noise rates  
  
- Assume $t$ is discrete. (can be continuous)  
      
- $\alpha, \beta (\because \beta := 1-\alpha)$  
      
    - $(0 \le \alpha, \beta \le 1)$  
          
- **Signal rate $\alpha_t$**: ($\alpha_t$)  
      
- **Noise rate $\beta_t$**: ($\beta_t = 1 - \alpha_t$)  
      
- **$\bar{\alpha}_t$**  
      
    - $\bar{\alpha}_t = \prod_{s=1}^{t} \alpha_s$  
          
    - ($X_t$에서 $X_0$가 얼마나 남아있는가)  
          
    - Graph: Linear decay labeled $\frac{t}{T}$  
          
  
### (4) Diffusion kernels  
  
- $q$  
      
    - ↳ transition probabilistic kernel 로 설명  
          
- **Forward diffusion kernel**: $q(x_t|x_{t-1})$  
      
- **Reverse**: $p(X_{t-1}|X_t)$  
      
    - $q(z|x)$: 분포가 나오는 이것을 kernel이라 부름.  
          
- **Learning target**: $p_\theta(X_{t-1}|X_t)$ (reverse diffusion kernel)  
      
  
### (5) Gaussian approximation  
  
- Noise level ($\beta$)가 충분히 작다면 reverse diffusion kernel은 Gaussian으로 근사 가능.  
      
  
### (6) L. comb of img & noise  
  
- $X_t = \sqrt{\alpha_t}X_{t-1} + \sqrt{1-\alpha_t}\epsilon$  
      
- **Note**: $X_t = \sqrt{\bar{\alpha}_t}X_0 + \sqrt{1-\bar{\alpha}_t}\cdot \epsilon$  
      
  
### (7) Referencing $X_0$  
  
- $q(X_{t-1}|X_t)$: intractable  
      
- $q(X_{t-1}|X_t, X_0)$: tractable  
      
  
# DDPM Overview  
  
## Training  
  
- $X_t = \sqrt{\bar{\alpha}_t}X_0 + \sqrt{1-\bar{\alpha}_t}\epsilon$  
      
    - (급행열차)  
          
- ($X_0$ is given when training)  
      
- Model: U-Net  
      
- Loss $(\epsilon, \hat{\epsilon})$  
      
  
## Sampling  
  
- $X_{t-1} = \frac{1}{\sqrt{\alpha_t}}(X_t - \frac{1-\alpha_t}{\sqrt{1-\bar{\alpha}_t}}\hat{\epsilon}) + \sigma_t Z$  
      
- Model: U-Net  
      
- Iterative process: $X_t \rightarrow X_{t-1} \dots \rightarrow X_0$  
      
  
# Forward Diffusion Details  
  
- $X_0 \rightarrow X_1 \rightarrow \cdot\cdot\cdot \rightarrow X_{t-1} \rightarrow X_t \rightarrow \cdot\cdot\cdot \rightarrow X_T$  
      
- Noise $\sim \mathcal{N}(0, I)$  
      
- $q(x_t|x_{t-1})$  
      
    - ↳ $q(x_{1:T}|x_0) := \prod_{t=1}^{T} q(x_t|x_{t-1})$  
          
  
### Mathematical Definition  
  
- $q(X_t|X_{t-1}) := \mathcal{N}(X_t; \sqrt{1-\beta_t}X_{t-1}, \beta_t I)$  
      
- $X_t$: Signal rate $\sqrt{1-\beta_t}$  
      
- 직전 상태에만 의존  
      
- $q(X_t|X_{t-1})$ is not [learning] 아니라 $\beta_t$ Scheduling으로 고정됨.  
      
- $\Rightarrow$ 적절한 $\beta_t$ scheduling 에서 $X_T$ isotropic Gaussian distribution으로 만들 수 있다.  
      
- $\Rightarrow X_t = \sqrt{1-\beta_t}X_{t-1} + \sqrt{\beta_t}\epsilon$  
      
    - $= \sqrt{\alpha_t}X_{t-1} + \sqrt{1-\alpha_t}\epsilon$  
          
  
### "Express Train" Derivation  
  
- $X_t = \sqrt{\alpha_t}X_{t-1} + \sqrt{1-\alpha_t}\epsilon_{t-1}$  
      
- $= \sqrt{\alpha_t}(\sqrt{\alpha_{t-1}}X_{t-2} + \sqrt{1-\alpha_{t-1}}\epsilon_{t-2}) + \sqrt{1-\alpha_t}\epsilon_{t-1}$  
      
- $= \sqrt{\alpha_t \alpha_{t-1}}X_{t-2} + \sqrt{\alpha_t}\sqrt{1-\alpha_{t-1}}\epsilon_{t-2} + \sqrt{1-\alpha_t}\epsilon_{t-1}$  
      
    - $\epsilon_t \sim \mathcal{N}(0, I)$  
          
    - $\epsilon_{t-1} \sim \mathcal{N}(0, {\sigma_{t-1}^*}^2 I)$  
          
    - Sum of variances: $\epsilon_{t-2} + \epsilon_{t-1} \sim \mathcal{N}(0, ({\sigma_{t-2}}^2 + {\sigma_{t-1}}^2)I)$  
          
- Result: $\sqrt{\alpha_t \alpha_{t-1}}X_{t-2} + \sqrt{1-\alpha_t \alpha_{t-1}}\bar{\epsilon}_{t-2}$  
      
  
### Definition of $\bar{\alpha}_t$  
  
- Define $\bar{\alpha}_t = \prod_{s=1}^{t} \alpha_s$  
      
- $X_t = \sqrt{\bar{\alpha}_t}X_0 + \sqrt{1-\bar{\alpha}_t}\epsilon$  
      
- Randomly sample $\epsilon$ and get $X_t$!  
      
  
# More on $X_t$ Analysis  
  
- **$\beta$? Noise $\epsilon$:**  
      
    - ① $\sqrt{\bar{\alpha}_t}X_0$: $X_t$에서 $X_0$가 남아있는 비율 (signal)  
          
    - ② $\sqrt{1-\bar{\alpha}_t}$: cumulative variance (noise)  
          
        - $\sqrt{1-\bar{\alpha}_t}$: noise 더해진 비율  
              
        - $\bar{\alpha}_t$는 cumulative product  
              
    - ③ $\sqrt{1-\bar{\alpha}_t}$는 standard deviation sum이 아님!!  
          
        - ↳ noise는 additive 함.  
              
        - 차라리 $\bar{\beta}_t := 1 - \bar{\alpha}_t$ 로 정의하자.  
              
        - $\bar{\alpha}_t + \bar{\beta}_t = 1$  
              
  
## Noise Composition  
  
- $X_{t-1} = \sqrt{\bar{\alpha}_{t-1}}X_0 + \sqrt{1-\bar{\alpha}_{t-1}}\epsilon'$  
      
- $X_t = \sqrt{\alpha_t}X_{t-1} + \sqrt{\beta_t}\epsilon$  
      
- $= \sqrt{\alpha_t}(\sqrt{\bar{\alpha}_{t-1}}X_0 + \sqrt{1-\bar{\alpha}_{t-1}}\epsilon') + \sqrt{\beta_t}\epsilon$  
      
- $= \sqrt{\alpha_t}\sqrt{\bar{\alpha}_{t-1}}X_0 + \sqrt{\alpha_t}\sqrt{1-\bar{\alpha}_{t-1}}\epsilon' + \sqrt{\beta_t}\epsilon$  
      
    - Trick:  
          
    - $= \sqrt{\bar{\alpha}_t}X_0 + \sqrt{(\alpha_t(1-\bar{\alpha}_{t-1}) + \beta_t)}\epsilon''$  
          
    - $= \sqrt{\bar{\alpha}_t}X_0 + \sqrt{\alpha_t(1-\bar{\alpha}_{t-1}) + 1 - \alpha_t}\epsilon''$  
          
        - Inherited noise: $\alpha_t(1-\bar{\alpha}_{t-1})$  
              
        - New noise: $1-\alpha_t$  
              
- $= \sqrt{\bar{\alpha}_t}X_0 + \sqrt{1-\bar{\alpha}_t}\epsilon$ (Cumulative noise)  
      
  
### Noise Ratio Analysis  
  
- $1-\bar{\alpha}_t = \alpha_t(1-\bar{\alpha}_{t-1}) + \beta_t$  
      
- Cumulative noise = Inherited noise + New noise  
      
- $1 = \frac{\beta_t}{1-\bar{\alpha}_t} + \frac{\alpha_t(1-\bar{\alpha}_{t-1})}{1-\bar{\alpha}_t}$  
      
- Let $\lambda_t := \frac{\beta_t}{1-\bar{\alpha}_t}$  
      
    - $\lambda_t$: Total noise 에서 newly added 비율  
          
  
## Multi-step Kernel  
  
- $q(X_t|X_0) = \mathcal{N}(X_t; \sqrt{\bar{\alpha}_t}X_0, (1-\bar{\alpha}_t)I)$  
      
    - Why? $X_t = \sqrt{\bar{\alpha}_t}X_0 + \sqrt{1-\bar{\alpha}_t}\epsilon$  
          
  
## Diffused Data Distribution  
  
- $q_t(x_t) = \int q(x_0, x_t)dx_0 = \int q(x_0)q(x_t|x_0)dx_0$  
      
- But.... intractable.  
      
- Use ancestral sampling:  
      
    - (1) $x_0 \sim q(x_0)$  
          
    - (2) $x_t \sim q(x_t|x_0)$  
          
- 사실상 $X_t \sim \Phi(X_t) \oplus \Psi$ (Input $\oplus$ Diffusion kernel)  
      
  
# Reverse Diffusion Process  
  
- $X_{t-1} \sim q(x_{t-1}|x_t)$  
      
- ↳ Posterior: $q(x_{t-1}|x_t) = \frac{q(x_{t-1}, x_t)}{q(x_t)} = \frac{q(x_t|x_{t-1})q(x_{t-1})}{q(x_t)}$  
      
  
## Gaussian Approximation  
  
- $\beta_t$ 가 충분히 작으면 $q(x_{t-1}|x_t)$ ~ $\mathcal{N}$ 이다.  
      
- **Idea**:  
      
    - ① Gaussian $P_\theta(X_{t-1}|X_t)$로 $q(X_{t-1}|X_t)$ 근사  
          
    - ② $P_\theta$ parameterize  
          
  
## Parameterization  
  
- $P_\theta(X_{0:T}) := P(X_T) \prod_{t=1}^{T} P_\theta(X_{t-1}|X_t)$  
      
- $P(X_T) \sim \mathcal{N}(X_T; 0, I)$  
      
- Kernel: $P_\theta(X_{t-1}|X_t) := \mathcal{N}(X_{t-1}; \mu_\theta(X_t, t), \Sigma_\theta(X_t, t))$  
      
    - PPM은 둘다 learn  
          
  
## DDPM Specifics  
  
- Isotropic  
      
- DDPM은 $\mu_\theta$만 learn  
      
- Covariance $\Sigma_\theta(x_t, t) = \sigma_t^2 I$  
      
    - $p_\theta(x_{t-1}|x_t) = \mathcal{N}(X_{t-1}; \mu_\theta(x_t, t), \sigma_t^2 I)$  
          
    - $\sigma_t^2 = \beta_t$로 설정하여 predetermined.  
          
    - $\mu_\theta$ learn by U-Net  
          
- **Stochastic denoising**: $X_{t-1} \sim P_\theta(X_{t-1}|X_t)$  
      
    - $X_{t-1} = \mu_\theta(X_t, t) + \sigma_t z$  
          
    - $z \sim \mathcal{N}(0, 1)$  
          
    - Denoised ($\mu_\theta$) + Added noise ($\sigma_t z$)  
          
- (DDIM은 $\sigma_t$를 넣지 않음; deterministic)  
      
  
# Setting a Learning Target  
  
- $q(x_{t-1}|x_t)$ is intractable. ($\rightarrow p_\theta(x_{t-1}|x_t)$가 진짜 보장하는가? intractable 한걸...)  
      
- Condition on $X_0$: $q(x_{t-1}|x_t, x_0) = \frac{q(x_t|x_{t-1}) \cdot q(x_{t-1}|x_0)}{q(x_t|x_0)}$ (Tractable)  
      
    - Proof: $\sim \mathcal{N}(x_{t-1}; \tilde{\mu}_t(x_t, x_0), \tilde{\beta}_t I)$  
          
    - $\tilde{\mu}_t(x_t, x_0) = \frac{\sqrt{\bar{\alpha}_{t-1}}\beta_t}{1-\bar{\alpha}_t}X_0 + \frac{\sqrt{\alpha_t}(1-\bar{\alpha}_{t-1})}{1-\bar{\alpha}_t}X_t$  
          
    - $= \frac{1}{\sqrt{\alpha_t}}(X_t - \frac{\beta_t}{\sqrt{1-\bar{\alpha}_t}}\epsilon)$  
          
    - $\tilde{\beta}_t = \frac{1-\bar{\alpha}_{t-1}}{1-\bar{\alpha}_t}\beta_t$  
          
  
## Intuition  
  
- $X_{t-1}$ is linear comb. of $X_0$ & $X_t$  
      
- Convex combination  
      
- $X_0$ (Original) $\leftrightarrow$ $X_t$ (Noisy)  
      
- $\tilde{\mu}_t(X_t, X_0)$: $X_{t-1}$ (추정하려는 것)의 평균  
      
- $\therefore X_0$와 $X_t$의 balance를 바탕으로 $X_{t-1}$를 얻는다.  
      
    - (1) 만약 여기 올때 당장의 $\beta_t$가 컸다면 ($X_{t-1} \rightarrow X_t$):  
          
        - $\uparrow$ ($X_0$를 더 많이 믿자): 축적된 noise가 클수록.  
              
        - Coefficient $\frac{1}{\sqrt{\alpha_t}}$ increases as noise ($\beta_t$) decreases.  
              
    - (2) 축적된 $\beta_t$가 더 크다면:  
          
        - ↳ ($X_t$를 더 많이 믿자)  
              
  
### Scale Up & Noise Removal  
  
- Form: $\tilde{\mu}_t(x_t, x_0) = \frac{1}{\sqrt{\alpha_t}}(X_t - \frac{\beta_t}{\sqrt{1-\bar{\alpha}_t}}\epsilon)$  
      
- Amount of noise to 'remove':  
      
    - (제거할 noise) = (xt에서의 총 noise) x (제거할 noise proportion $\frac{\beta_t}{1-\bar{\alpha}_t}$)  
          
    - $=$ ($\epsilon$) x ($\frac{\beta_t}{\sqrt{1-\bar{\alpha}_t}}$)  
          
    - Ratio: $t$에서 추가된 noise / $t$까지 축적된 noise  
          
  
# Training DDPM  
  
## Training Objective  
  
- 결국 $P_\theta$와 $q$ 차이를 줄여야하는데 VAE와 동일.  
      
- $L_{VLB} = \mathbb{E}_{q}[\dots]$  
      
- $L = L_T + L_{t-1} + \dots + L_0$  
      
  
### Loss Components  
  
1. **$L_T$ (Encoder)**: $D_{KL}[q(x_T|x_0) || p(x_T)]$  
      
    - ↳ 실제 $X_T$가 Gaussian과 얼마나 비슷한가.  
          
    - $q(x_T|x_0) = \mathcal{N}(x_T; \sqrt{\bar{\alpha}_T}x_0, (1-\bar{\alpha}_T)I)$  
          
    - $P(X_T) \sim \mathcal{N}(0, I)$.  
          
    - DDPM에서는 $\beta_t$ (즉, $\alpha_t$도)가 고정이라 무시 가능.  
          
2. **$L_0$ (Decoder)**: $-\log P_\theta(x_0|x_1)$  
      
    - ↳ $t=1$ 전용 reconstruction term  
          
    - Independent decoder.  
          
3. **$L_{t-1}$ (Denoiser)**: $D_{KL}[q(x_{t-1}|x_t, x_0) || p_\theta(x_{t-1}|x_t)]$  
      
    - 실제 denoiser (with target) vs learned general denoiser  
          
    - $D_{KL}$ (Gaussian 분포의 $D_{KL}$):  
          
        - $= \frac{1}{2\sigma_t^2} || \tilde{\mu}_t(x_t, x_0) - \mu_\theta(x_t, t) ||^2 + \text{const.}$  
              
    - 결국 $\tilde{\mu}_t$와 $\mu_\theta$간 Squared error 줄이기임.  
          
  
## Parameterization  
  
- So, $\mu_\theta(X_t, t)$을 뭐로 예측해야함?  
      
    - (1) $\tilde{\mu}_t$ 평균 자체 예측  
          
    - (2) $X_0$: 원본 예측  
          
    - (3) $\epsilon$: noise 예측 $\rightarrow$ 얘가 제일 잘하더라.  
          
- $\mu_\theta(x_t, t) = \frac{1}{\sqrt{\alpha_t}}(x_t - \frac{\beta_t}{\sqrt{1-\bar{\alpha}_t}}\epsilon_\theta(x_t, t))$  
      
- $X_{t-1} = \frac{1}{\sqrt{\alpha_t}}(X_t - \frac{\beta_t}{\sqrt{1-\bar{\alpha}_t}}\epsilon_\theta(x_t, t)) + \sigma_t Z$  
      
  
## Final Loss  
  
- Set $\lambda_t = 1$  
      
- $L_{simple} = \mathbb{E}_{x_0, \epsilon} [ || \epsilon - \epsilon_\theta(\sqrt{\bar{\alpha}_t}x_0 + \sqrt{1-\bar{\alpha}_t}\epsilon, t) ||^2 ]$  
      
- **Note**: Content-detail trade off  
      
- **Gradient**: $\nabla_\theta || \epsilon - \epsilon_\theta(\sqrt{\bar{\alpha}_t}x_0 + \sqrt{1-\bar{\alpha}_t}\epsilon, t) ||^2$  
      
  
# Sampling & Implementation  
  
## Sampling Process  
  
- $X_t (\mathcal{N}) \xrightarrow{t} \text{U-Net}(\epsilon_\theta) \rightarrow \hat{\epsilon} \rightarrow \mu_\theta \rightarrow \oplus (\sigma_t z) \rightarrow X_{t-1}$  
      
  
## Additional Details  
  
- **Slow sampling**  
      
    - ↳ DDPM의 drawback.  
          
    - All T (x1000) iterations should be performed sequentially.  
          
    - Slower than GAN (one-shot)  
          
- **Variance Scheduling?**  
      
    - $X_{t-1} \xleftarrow{q} X_t$  
          
    - $\beta_t$: Forward diffusion process  
          
    - $\sigma_t$: Reverse diffusion process  
          
    - 보통은 $\sigma_t^2 = \beta_t$  
          
    - Schedules:  
          
        - Linear  
              
        - Cosine-based ($\rightarrow$ 급격히 떨어지는거 방지)  
              
        - SNR based schedule  
              
            - $SNR := \frac{\text{mean}^2}{\text{variance}} = \frac{\bar{\alpha}_t}{1-\bar{\alpha}_t}$  
                  
- **Implementation**  
      
    - U-Net with ResNet + Self-attention  
          
  
# Connection to VAEs?  
  
## (1) VAE  
  
- $X \xrightleftharpoons[P_\theta(X|Z)]{q_\phi(Z|X)} Z$  
      
  
## (2) Diffusion  
  
- $X_0 \xrightleftharpoons[P_\theta]{q} X_1 \rightleftharpoons \cdot\cdot\cdot \rightleftharpoons X_T$  
      
- Encoder: Fixed diffusion process  
      
- Decoder: Learnable denoising process  
      
- ↳ 사실상 $\dim X = \dim Z$ 이고 encoder fix된 VAE임.