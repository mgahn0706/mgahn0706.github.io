---  
tags:  
  - regularization  
  - overfitting  
  - batch  
  - adversarial-training  
  - dropout  
  - deep-learning  
share: "true"  
github_title: 2025-10-11-regularization  
title: 4. Regularization  
date: 2025-10-11  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. Regularization  
  
Noise, ...  
  
we cannot model  
  
$\hookrightarrow$ overfitting, less generalization  
  
**Overfitting**  
  
- $\Rightarrow$ fitting the data more. $E_{train}$ alone is not a good guide.  
      
- $E_{train} \neq E_{test}$  
      
- Observed when model is complex.  
      
    - $\hookrightarrow$ use additional DOF (Degrees of Freedom) to fit noise in data.  
          
  
**Regularization**  
  
- $\rightarrow$ 빨리 못따라가게 구속하여 high frequency 학습 X (Constrain to prevent learning high frequency noise quickly)  
      
  
**Augmented Error**  
  
- $\hookrightarrow$ ex. 도메인 지식으로 $E_{test}$ $\uparrow$ (Use domain knowledge).  
      
- $\hookrightarrow$ Comb. of $E_{train}$ and $\Omega$ (penalty of model complexity).  
      
- $E_{aug}(w) = E_{train}(w) + \lambda \Omega(w)$  
      
    - $\rightarrow$ 왜 $N$인가? $\Omega(\theta)$? (Why N? Omega?)  
          
    - 학습 data 수 (Number of training data).  
          
  
**Ex. Weight decay regularization**  
  
- $E_{aug}(w) = E_{train}(w) + \frac{\lambda}{N} w^T w$ ($\frac{1}{2}$ often used).  
      
  
**Neural nets bias regularization**  
  
- $N \rightarrow \infty$ 이면 regularizer 필요 X (If N is infinite, regularizer not needed).  
      
- $||w||^2$: 크기가 클수록 벌을 준다 (Penalize larger weights).  
      
  
**Early Stopping**  
  
- $\hookrightarrow$ $E_{dev}$  
      
- **Best model** = Stop when $E_{dev}$ is low. Then $E_{test}$ will likely be good too.  
      
- A large model that has been regularized.  
      
- Extreme large data: regularization not necessary.  
      
  
---  
  
# 2. Batch Norm and Variants  
  
**Batch Norm (BN)**  
  
- $\hookrightarrow$ regularization + better training  
      
- **Idea**: Explicitly force the activation.  
      
- **Possible?**: Normalization is differentiable (Can be back-propagated).  
      
- FC/Conv $\rightarrow$ BN layer $\rightarrow$ non-linear.  
      
- $\rightarrow$ BN: Preprocessing at every layer of the net.  
      
  
**BN Operation #1: Normalization**  
  
- $\hookrightarrow$ Normalize each scalar (without decorrelation).  
      
- Example:  
      
    - Feature $x_1 \dots x_d$  
          
    - Mini-batch $\mathcal{B} = \{x^{(1)} \dots x^{(m)}\}$  
          
    - Normalize $\hat{x}^{(k)}$  
          
    - $\mu_k = \frac{1}{m} \sum_{i=1}^{m} x_k^{(i)}$  
          
    - $\sigma_k^2 = \frac{1}{m} \sum_{i=1}^{m} (x_k^{(i)} - \mu_k)^2$  
          
    - $\hat{x}_k^{(i)} = \frac{x_k^{(i)} - \mu_k}{\sqrt{\sigma_k^2 + \epsilon}}$  
          
  
**BN Operation #2: Linear Transform**  
  
- $k$-th feature 대해 (For k-th feature).  
      
- $\hookrightarrow$ **Simple normalization**: reduce the representation power.  
      
    - $\rightarrow$ hidden units always have $\mu_k=0, \sigma_k=1$.  
          
- **Restore representation power**:  
      
    - $y_k^{(i)} = \gamma_k \hat{x}_k^{(i)} + \beta_k \equiv BN_{\gamma, \beta}(x_k^{(i)})$  
          
    - $\gamma, \beta$: learned by SGD.  
          
- **Effects**:  
      
    - Simplify learning dynamics.  
          
    - Cut high-order interactions.  
          
    - Fix distribution of network.  
          
  
---  
  
### **BN and its Variants (Diagrams)**  
  
**(1) Batch Norm**  
  
- [Cube Diagram: N, C, H, W]  
      
- Data 1개 (Depends on batch statistics).  
      
  
**(2) Layer Norm**  
  
- [Cube Diagram sliced by N]  
      
- Used often in RNN/Transformer.  
      
  
**(3) Instance Norm**  
  
- [Cube Diagram sliced by N and C]  
      
- $\Rightarrow$ Data 마다 (Any-size, 크기 달라도 됨, 시계열) (Per data sample. Can be any size, time-series).  
      
- Instance-specific features preserved (e.g., Image style transfer).  
      
  
**(4) Group Norm**  
  
- $LN (G=1) \leftrightarrow IN (G=C)$  
      
- Split channels into groups: $G = \frac{C}{2}$ etc.  
      
- ex. Tiny batch training in CV.  
      
  
---  
  
# 3. Regularization Techniques  
  
**Immunizing a model by noise/constraint injection**  
  
- **Input**: Data augmentation, adversarial training.  
      
- **Hidden units**: Dropout.  
      
- **Weights**: Imposing penalty ($L_1, L_2$).  
      
- **Output targets**: Label smoothing.  
      
- **Knowledge**: Knowledge distillation.  
      
  
### **Vector Norms**  
  
- $L_p$ norm: $||x||_p = (\sum_{i=1}^{n} |x_i|^p)^{1/p}$  
      
- $L_\infty$ norm: $||x||_\infty = \max_i |x_i|$  
      
  
Norm Penalty (Weight Injection)  
  
(1) $L_1$ Regularizer (Lasso)  
  
- $\Omega(w) = ||w||_1 = \sum_q |w_q|$  
      
- [Graph: Diamond shape tangent to line]  
      
- $\rightarrow$ $w_1 = 0$ (Sparse solution). 일부만 살아남음 (Only some survive).  
      
  
**(2) $L_2$ Regularizer (Weight Decay)**  
  
- $\Omega(w) = ||w||_2^2 = w^T w = \sum_q w_q^2$  
      
- [Graph: Circle shape tangent to line]  
      
- $\rightarrow$ Variable shrinkage only (No selection).  
      
  
**(3) Elastic-net Penalty**  
  
- $\Omega(w) = \sum_q \{ \alpha |w_q| + \frac{1}{2}(1-\alpha)w_q^2 \}$  
      
  
---  
  
# 4. Noise Injection  
  
**Data Augmentation**  
  
- $\hookrightarrow$ Create fake data and add it to training set.  
      
- Issue: Difficulty of creating valid data.  
      
- $\hookrightarrow$ **Auto Augment**: RL-based technique. Learns augmentation policies.  
      
  
**Mixup and its Variants**  
  
- **Linear interpolations** of feature vectors = targets.  
      
- Favor simple linear behavior.  
      
- **Mixup Formula**:  
      
    - $\tilde{x} = \lambda x_i + (1-\lambda) x_j$  
          
    - $\tilde{y} = \lambda y_i + (1-\lambda) y_j$  
          
- **Variants**: Cutout, CutMix, PixMix. (Dream-like images).  
      
  
**Adversarial Training**  
  
- Adversarial attack by adding imperceptibly small perturbations.  
      
- **Attack!** $\rightarrow$ Train on these to improve robustness.  
      
  
**Dropout (Hidden Layers)**  
  
- Exploits adversarial training robustness.  
      
- $\hookrightarrow$ Model should spread out weights. Shrink weights (norm penalty).  
      
- $\rightarrow$ Making noise applied to **hidden units**.  
      
  
**Label Smoothing (Output Targets)**  
  
- Neural nets often overconfident (Overfit).  
      
- Label smoothing encourages a model to be **less confident**.  
      
- **Formula**:  
      
    - One-hot: $(y_1, y_2, \dots, y_k)$  
          
    - $y_k^{LS} = y_k(1-\alpha) + \alpha / K$  
          
- **Example** (Cross-entropy loss):  
      
    - $K=3, \alpha=0.1$  
          
    - $\begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \rightarrow \begin{bmatrix} 0.9 + 0.033 \\ 0.033 \\ 0.033 \end{bmatrix} = \begin{bmatrix} 0.93 \\ 0.03 \\ 0.03 \end{bmatrix}$  
          
    - 국물 나눠주기 (Sharing the soup/probability).  
          
  
---  
  
# 5. Knowledge Distillation  
  
**Teacher Network ($T$)**  
  
- Excellent performance.  
      
- Computationally expensive.  
      
- **Soft label** of $T$ (Dark Knowledge).  
      
  
**Student Network ($S$)**  
  
- Lower performance than $T$.  
      
- Fast inference.  
      
- Limited environment.  
      
  
**Training**  
  
- $L_S = (1-\alpha) \cdot L_{CE} (Ground Truth) + \alpha \cdot L_{distill} (Teacher's Soft Label)$