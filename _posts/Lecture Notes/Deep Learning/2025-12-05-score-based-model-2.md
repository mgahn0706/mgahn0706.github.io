---  
tags:  
  - score-based  
  - deep-learning  
  - diffusion  
share: "true"  
github_title: 2025-12-05-score-based-model-2  
title: 14. Score-based Model 2  
date: 2025-12-05  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# Main NCSN!  
  
## Key challenge for building complex gen-models  
  
- $x \rightarrow \prod_{A}f_{\theta}(x) \rightarrow O \rightarrow e^{f_{\theta}(x)} \rightarrow O = \frac{e^{f_{\theta}(x)}}{Z_\theta} = P_{\theta}(x).$  
      
    - Maybe negative  
          
- $\overline{Z}_{\theta} = \int e^{f_{\theta}(x)}dx$  
      
- **Computing $Z_\theta$ in general:**  
      
    - Intractable.  
          
  
## How to tackle intractable $Z_{\theta} = \int e^{f_{\theta}(x)}dx$?  
  
- Approximate $Z_\theta$ by energy-based  
      
    - ↳ inaccurate $P(x)$  
          
- Restricted  
      
    - In models  
          
    - ↳ restricted to flow, auto regressive, VAE  
          
- Modeling generation only  
      
    - ↳ no evaluation for $p(x)$ (DL)  
          
  
# Data modeling by Estimating Score Functions  
  
- $P(X)$는 확률 분포함수.  
      
- $\nabla_{x}\log P(x)$: Score function (preserves all info.)  
      
    - ↳ 가장 빨리 증가하는 방향  
          
- c.f.) $\nabla_\theta \log P(X|\theta)$: Fisher score function.  
      
  
## Bypass $Z_\theta$  
  
- $p_{\theta}(x) = \frac{e^{f_{\theta}(x)}}{Z_{\theta}}$  
      
- $\log p_{\theta}(x) = f_{\theta}(x) - \log Z_{\theta}$  
      
- $\nabla_{x}\log P_{\theta}(x) = \nabla_{x}f_{\theta}(x) - \nabla_{x}\log \overline{Z_{\theta}}$  
      
    - $= S_{\theta}(x)$ (Target)  
          
  
# Learning objective  
  
- **Given**: $x_{1}, \cdot\cdot\cdot, x_{N} \sim P_{data}(x)$  
      
- **Goal**: $\nabla_x \log P_{data}(X) \leftarrow \text{Score model}$  
      
  
## Score model  
  
- 비교?  
      
- $S_{\theta}(x): \mathbb{R}^{d} \rightarrow \mathbb{R}^{d} \approx \nabla_x \log P_{data}(x)$  
      
  
## Fisher divergence  
  
- $\frac{1}{2}E_{p_{data}}[||\nabla_x \log p_{data}(x) - S_\theta(x)||_{2}^{2}]: \text{learning target}$  
      
- 근데 $\nabla_x \log P_{data}(x)$를 모름.  
      
- $FD = E_{p_{data}}[\frac{1}{2}||S_\theta(x)||_{2}^{2} + trace(\nabla_{x}S_{\theta}(x))] + \text{const.}$  
      
- $\approx \frac{1}{N}\sum_{i=1}^{N}[\frac{1}{2}||S_{\theta}(x_{i})||_{2}^{2} + trace(\nabla_x S_{\theta}(x_{i}))]$  
      
    - ex) $S_{\theta}(x) = [3x_1, 4x_2^2, 5]$  
          
    - $||S_{\theta}(x)||_{2}^{2} = 9{x_{1}}^{2} + 16x_{2}^{4} + 25$  
          
    - $trace(\nabla_{x}S_{\theta}(x)) = 3 + 8x_2 + 0$  
          
- $\nabla_{x}S_{\theta}(x) = \begin{bmatrix} \frac{\partial S_{\theta 1}(x)}{\partial x_{1}} & \dots \\ \dots & \frac{\partial S_{\theta d}(x)}{\partial x_{d}} \end{bmatrix}$  
      
    - 합. 근데 $d$ 다 할 수 없으니  
          
- Backprop은 X의 차원만큼! $\mathcal{O}(\dim(x))$: 200만 차원. trace 구해야 하고 $S_{\theta}(x) \in \mathbb{R}^{d \times d}$  
      
  
## Denoising Score matching (noise 섞어서 구하자)  
  
- : 어려움  
      
- $X \sim P_{data}(x)$  
      
    - $\leftarrow \leftarrow \leftarrow (\times \sigma)$  
          
    - $\sigma$ 만큼  
          
- $q_{\sigma}(\tilde{x}) = \int p_{data}(x)q_{\sigma}(\tilde{x}|x)dx$  
      
- ↳ **Denoising score matching (2011)**  
      
- $\frac{1}{2} E_{p_{data}} E_{q_\sigma(\tilde{x}|x)} [||\nabla_{\tilde{x}} \log q_{\sigma}(\tilde{x}|x) - S_\theta(\tilde{x})||_{2}^{2}]$  
      
    - Noise kernel.  
          
    - 섞어라  
          
    - Easy to compute  
          
    - 안 backprop 하면됨  
          
- $q_{\sigma}(\tilde{x}|x) = \mathcal{N}(\tilde{x}|x, \sigma^{2}I)$ 이거 최소화하도록  
      
- $\nabla_{\tilde{x}}\log q_{\sigma}(\tilde{x}|x) = -\frac{\tilde{x}-x}{\sigma^{2}}$ (Closed form)  
      
  
# Scalable  
  
- $S_{\theta}(x) \approx \nabla_{x}\log q_{\sigma}(x) \ne \nabla_{x}\log P_{data}(x)$  
      
  
## How?  
  
- $\{x_{1}, x_{2}, \cdot\cdot\cdot, x_{n}\} \sim P_{data}(x)$  
      
    - $\downarrow$ noise  
          
- $\{\tilde{x}_{1}, \tilde{x}_{2}, \cdot\cdot\cdot, \tilde{x}_{n}\} \sim q_{\sigma}(\tilde{x})$  
      
    - $\tilde{x}_{i} \sim q_{\sigma}(\tilde{x}_{i}|x_{i})$  
          
- Estimate denoising score matching loss  
      
- $\frac{1}{2n}\sum_{i=1}^{n}[||S_{\theta}(\tilde{x}_{i}) - \nabla_{\tilde{x}}\log q_{\sigma}(\tilde{x}_{i}|x_{i})||_{2}^{2}]$  
      
    - ↳ substitution  
          
- $\frac{1}{2n}\sum_{i=1}^{n}[||S_{\theta}(\tilde{x}_{i}) + \frac{\tilde{x}_{i}-x_{i}}{\sigma^{2}}||_{2}^{2}]$  
      
- SGD.  
      
- $\Rightarrow$ 하지만, noise free를 원해요...  
      
  
## Pitfall  
  
- ① Small $\sigma$를 해야하나...  
      
- ② Loss variance가 $\sigma \rightarrow 0$ 이면 너무 커져 training 어렵다.  
      
- 즉, trade-off가 있다 $\rightarrow$ **Sliced score matching**  
      
    - ($\sigma \rightarrow 0$으로 보내면... 문제가 생길 수 있음)  
          
- $J = \frac{1}{2}E_{x \sim p_{data}}E_{z \sim \mathcal{N}(0, I)}[||S_\theta(x+\sigma z) + \frac{z}{\sigma}||_{2}^{2}]$  
      
    - $\tilde{x} = x + \sigma z$  
          
- $= \frac{1}{2}E_{x \sim p_{data}}E_{z \sim \mathcal{N}(0, I)}[||S_{\theta}(x+\sigma z)||_{2}^{2} + 2S_{\theta}(x+\sigma z)^{\top}\frac{z}{\sigma} + \frac{||z||_{2}^{2}}{\sigma^{2}}]$  
      
    - $\sigma \rightarrow 0$  
          
    - $Var(\frac{z}{\sigma}) \rightarrow \infty$  
          
  
# Sampling  
  
## How to sample new data?  
  
- [Drawing of data points converging to a manifold]  
      
- $S_{\theta}(x) \approx \nabla_{x}\log P_{data}(x)$  
      
- **Assume**: 그냥 score function 따라가면... 하나로 collapse  
      
- $\tilde{x}_{t+1} \leftarrow \tilde{x}_{t} + \frac{\epsilon}{2}S_{\theta}(\tilde{x}_{t})$ in data space.  
      
  
## Langevin dynamics  
  
- ↳ Follow noisy version of score function!  
      
- $\tilde{x}_{t+1} \leftarrow \tilde{x}_{t} + \frac{\epsilon}{2}S_{\theta}(\tilde{x}_{t}) + \sqrt{\epsilon}z_t$ where $z_t \sim \mathcal{N}(0,I)$  
      
  
### Procedure:  
  
1. $x^{0} \sim \Pi(x)$  
      
2. $t \leftarrow 1, 2, \cdot\cdot\cdot, T$  
      
    - $z^{t} \sim \mathcal{N}(0,I)$  
          
3. $x^{t} \leftarrow x^{t-1} + \frac{\epsilon}{2}\nabla_{x}\log P(x^{t-1}) + \sqrt{\epsilon}z^{t}$  
      
    - New pos $\leftarrow$ Current pos + Score function + Gaussian noise  
          
  
- $\epsilon \rightarrow 0$, $T \rightarrow \infty$이면 $X \sim P(x)$이다.  
      
- $S_{\theta}(x) \approx \nabla_{x}\log P(x)$  
      
  
# Score matching + Langevin dynamics not working....  
  
- Accurate vs Inaccurate regions  
      
- $\Rightarrow$ ① Low-density: not enough samples.  
      
- ② Weight 불가능  
      
- ③ Manifold hypothesis  
      
- $\rightarrow$ **Gaussian perturbation.**  
      
- Noise 크게해서 Langevin dynamics guide 하기.  
      
- $\sigma$  
      
    - ↳ 작게 해야 $p_{\theta} \approx q$ 이므로 이후 $\sigma$ 줄여야함.  
          
  
|**Noise**|**High**|**Low**|  
|---|---|---|  
|Sample quality|$\downarrow$|$\uparrow$|  
|Score est.|$\uparrow$|$\downarrow$|  
  
- 즉, **multi-scale (Cascade)** 해야한다.  
      
- $\sigma_1 > \sigma_2 > \dots > \sigma_L$  
      
- Guide 위해 noise 첨가 $\rightarrow$ Sampling quality 위해 제거  
      
  
# Annealed Langevin dynamics  
  
- $\mathcal{N}_{\sigma_1} \rightarrow \mathcal{N}_{\sigma_2} \rightarrow \cdot\cdot\cdot \rightarrow \mathcal{N}_{\sigma_L}$  
      
- (Cool down)  
      
- Sample 뽑고, $\hat{x}_{t} \leftarrow \hat{x}_{t-1} + \frac{\alpha_{i}}{2}S_{\theta}(\tilde{x}_{t-1}, \sigma_{i}) + \sqrt{\alpha}_{i}z_{t}$  
      
    - $\epsilon$ scheduling.  
          
- ↳ 그러면 매 noise level 마다 Score function 정의?  
      
- $\Rightarrow$ **Conditional score model (NCSN)**  
      
    - ↳ $\sigma$를 $S_\theta(\cdot, \cdot)$도 input 처리하여 학습. (Jointly trained)  
          
  
## Loss Function  
  
- $\mathcal{L} = \frac{1}{L}\sum_{i=1}^{L} \lambda(\sigma_i) E_{p_{\sigma_i}} [||\nabla_{x}\log p_{\sigma_i}(x) - S_{\theta}(x, \sigma_i)||_{2}^{2}]$  
      
    - $S_\theta$: 모든 noise level 학습.  
          
    - $\lambda(\sigma_i)$: Noise level 별 weight.  
          
    - $\lambda(\sigma_i) = \sigma_i^{2}$  
          
  
## Practical recommendations  
  
1. $\sigma_{1} < \sigma_{2} < ... < \sigma_{L}$  
      
    - $\sigma_1$: 충분히 작아야함  
          
    - $\sigma_L$: Max pairwise distance 급이어야함.  
          
    - $L \approx 100 \sim 1000$  
          
2. $S_\theta(x, \sigma_i)$: U-Net, Skip connection.  
      
    - 이정도 noise