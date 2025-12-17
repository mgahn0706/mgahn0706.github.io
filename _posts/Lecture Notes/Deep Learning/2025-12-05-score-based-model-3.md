---  
tags:  
  - score-based  
  - deep-learning  
  - diffusion  
share: "true"  
github_title: 2025-12-05-score-based-model-3  
title: 15. Score-based Model 3  
date: 2025-12-05  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# Controlling the Generation Process  
  
- Can we control the generation process?  
      
- $P(x)$ $\downarrow$  
      
- **Inverse distribution**: $P(x|y)$  
      
- Bayes' Rule:  
      
    - $p(x|y) = \frac{p(x) \cdot p(y|x)}{p(y)}$  
          
- **Score function decomposition**:  
      
    - $\nabla_x \log P(x|y) = \nabla_x \log P(x) + \nabla_x \log P(y|x)$  
          
    - $= \nabla_x \log P(x) + \nabla_x \log P(y|x)$  
          
        - $\approx S_\theta(x)$ (Unconditional Score)  
              
        - Classifier term  
              
- $\Rightarrow$ $p(y|x)$지만 learn 하면 되는데, 이건 사실 image classifier이다.  
      
- $p(y)$는 training 없이 specify 될 수 있다. 그냥 하면 됨.  
      
- **Conclusion**: Score-based gen model 하나면 다 된다.  
      
    - Classifier + unconditional gen model $P(x)$ (inverse problem)  
          
  
# Classifier Guidance  
  
- $P(x)$  
      
    - ↳ GAN 성능을 위해 classifier 강화 필요  
          
- DDPM은 unconditional gen만 됨. label 같이 줘도 X.  
      
    - ↳ Adversarial 하지 않으면서 discriminator를 만들자.  
          
- $\nabla_x \log P(y|x)$ 가 그 역할을 하겠다!  
      
  
## Basic Idea  
  
- **Goal**: $\nabla_{x_t} \log P(x_t|y)$ 를 learn하자. (원래는 $\nabla_{x} \log P(x_t) \approx S_\theta(x_t, t)$)  
      
    - ↳ $\nabla \log P(x_t|y) = \nabla \log (\frac{P(y|x_t) \cdot P(x_t)}{P(y)})$  
          
    - $\rightarrow$ Classifier guide  
          
    - $= \nabla_x \log P(x_t) + \nabla \log P(y|x_t)$  
          
    - 그림: 같은 방향으로 guide  
          
  
## Training & Sampling  
  
- **Note**: $\nabla \log P(x_t|y) = \nabla \log P(x_t) + \nabla \log P(y|x_t)$  
      
- **Training**:  
      
    - ① Score of unconditional diffusion model  
          
    - ② Classifier takes $X_t \rightarrow$ predicts $y$  
          
- **Sampling**:  
      
    - ↳ Unconditional score function + Gradient of noisy classifier  
          
    - $P(\cdot)$는 share 할 수 있고, $P_\phi(y|x_t, t)$ 로 처리가능  
          
  
## Guidance Scale  
  
- ↳ Hyper parameter ($\gamma$)  
      
- $\nabla \log P_\gamma(x_t|y) = \nabla \log P(x_t) + \gamma \nabla \log P(y|x_t)$  
      
    - $\gamma=0$: $y$ 무시.  
          
    - $\gamma \rightarrow \infty$: $y$와 강력히 연결. (Quality $\uparrow$ Diversity $\downarrow$)  
          
  
## How?  
  
- Train classifier (noise 추가된 거)  
      
  
## Limitation  
  
- Noise-aware classifier (Standard classifier X)  
      
- Unstable gradients  
      
- Computational cost.  
      
  
# Classifier-Free Guidance (CFG)  
  
- ↳ CFG uses a single diffusion model  
      
- **Recall**: $\nabla \log p(x_t|y) = \nabla \log P(x_t) + \nabla \log p(y|x_t)$  
      
- **Implicit classifier**:  
      
    - $\nabla \log p(y|x_t) = \nabla \log P(x_t|y) - \nabla \log P(x_t)$  
          
    - ↳ Conditioning dropout.  
          
- **Formula**:  
      
    - $\nabla \log p_\gamma(x_t|y) = \gamma \nabla \log p(x_t|y) + (1-\gamma) \nabla \log p(x_t)$  
          
    - ↳ Unconditional diffusion conditioning drop out  
          
  
## Conditioning Dropout  
  
- $P(x|y)$를 학습하자. (Conditioning dropout)  
      
    - ↳ $y$를 가끔 없앰 (10~20%.)  
          
    - ↳ $\emptyset$로 대체됨  
          
- $P(x|y)$와 $P(x)$가 모두 기능함.  
      
  
## Guidance Scale Analysis  
  
- $\nabla \log p_\gamma(x_t|y) = \gamma \nabla \log p(x_t|y) + (1-\gamma) \nabla \log p(x_t)$  
      
    - $[\gamma=0]$: Unconditional generation  
          
    - $[\gamma=1]$: Standard generation  
          
    - $[\gamma>1]$: Unconditional score 방향 반대로 이동.  
          
        - Reduce the probs of generating samples that do not use conditioning info.  
              
        - (ex. GLIDE)  
              
  
## Steps in CFG  
  
1. **Prepare**: A collection of (image, caption)  
      
2. **Training**:  
      
    - Train a unified model $\epsilon_\theta(x_t, c)$  
          
    - ↳ Random caption dropping (10%)  
          
    - ↳ Caption kept (90%)  
          
3. **Sample**:  
      
    - $X_T$를 뽑고  
          
    - (a) Unconditional $\epsilon_\theta(x_t, \emptyset)$: Baseline prediction  
          
    - (b) Conditional $\epsilon_\theta(x_t, c)$: Conditioning  
          
    - (c) Apply $\gamma$: $\hat{\epsilon}_\theta(x_t) = \epsilon_{uncond} + \gamma(\epsilon_{cond} - \epsilon_{uncond})$  
          
        - (고양이 쪽 noise) - (noise 없) $\rightarrow$ 고양이 벡터  
              
  
# Modern Architecture  
  
## Latent Diffusion Model (LDM)  
  
- ↳ Latent space에서 하기. 대부분의 bits는 perceptual detail임.  
      
- **Structure**:  
      
    - $x \rightarrow E \mapsto z \rightarrow \text{Diff} \longrightarrow Z_T$  
          
    - $z \rightarrow D \rightarrow x$  
          
    - U-Net uses Condition.  
          
- **Advantage**:  
      
    - ① Simple denoising + Faster synthesis (Normal distribution 과 유사)  
          
    - ② Expressive design  
          
    - ③ Autoencoder 사용가능.  
          
  
## Diffusion Transformer (DiT)  
  
- ↳ U-Net을 Transformer로 대체.  
      
- 확산 model forward SDE.  
      
- Reverse 에서의 PF-ODE 가능이 증명.  
      
  
# Advanced Models  
  
## DDIM  
  
- ↳ Deterministic sampling.  
      
- **Predicted**:  
      
    - $X_{t-1} = \sqrt{\bar{\alpha}_{t-1}} \hat{X}_0 + \sqrt{1-\bar{\alpha}_{t-1}} \epsilon$  
          
    - (Note: Formula in note approximates to deterministic update)  
          
- **Comparison**:  
      
    - 원래는 $X_{t-1} = \mu_\theta(x_t, t) + \beta_t \cdot \epsilon$  
          
- **Benefits**:  
      
    - ① Higher quality  
          
    - ② Consistency  
          
  
## Consistency Models  
  
- ↳ DDIM 보다 빠르게.  
      
- **Concept**:  
      
    - All points on latent space $\rightarrow$ same point in data space.  
          
    - $f_\theta(x_t, t) \longrightarrow X_0$ for $\forall t$  
          
    - ODE trajectory ($X_T \rightarrow X_0$)  
          
- **Training**:  
      
    - ① Directly train $f_\theta$  
          
    - ② Consistency distillation  
          
        - Teacher: Multi-step  
              
        - $\downarrow$  
              
        - Student: Consistency  
              
  
## Flow Matching  
  
- (바로 ODE를 배우기)  
      
- ↳ Learning velocity!  
      
- $\Rightarrow$ Encourages straighter, simpler path: Faster sampling  
      
- **How**:  
      
    - Noise $\leftrightarrow$ Data  
          
    - Learn Score  
          
- **Example**: Rectified flow  
      
  
## Examples  
  
- **Stable Diffusion 3**: MMDiT + Rectified flow  
      
- **Flux**: Parallel Transformer  
      
- **Nano Banana**: Autoregressive