---  
tags:  
  - deep-learning  
  - generative-model  
  - vae  
  - diffusion  
  - autoencoder  
  - LLM  
share: "true"  
github_title: 2025-10-31-generative-models  
title: 10. Generative Models  
date: 2025-10-31  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. Introduction  
  
- **Discriminative vs. Generative models**  
      
    - **Goal**: Learn function $f$ to map $x \rightarrow y$.  
          
    - **Discriminative**: Directly estimate $P(y|x)$.  
          
        - $f(x) = \arg\max_{y} P(y|x)$.  
              
        - Decision boundary.  
              
    - **Generative**: Estimate $P(x|y)$ and $P(y)$, then deduce $P(y|x)$.  
          
        - $P(y|x) = \frac{P(x|y)P(y)}{P(x)}$.  
              
        - For unsupervised learning...  
              
- **Fundamental Challenge**  
      
    1. **Density estimation**: Probability distribution of data.  
          
    2. **Sample generation**: Generate new samples from the same distribution.  
          
        - Train data $\sim P_{data}(x)$.  
              
        - $P_{model}(x) \rightarrow$ Sample.  
              
      
    - **How to understand complex input distributions?**  
          
        - Real images occupy a negligible proportion of volume of space.  
              
- **Why study generative models?**  
      
    - Trained with missing data.  
          
    - Inference of latent representations.  
          
    - Provide solutions to inverse problems.  
          
  
### **Inverse Problems**  
  
**(1) Forward problem: $P(y|x)$**  
  
- $x$를 주면 $y$를 predict 하는 모델 (Model that predicts $y$ given $x$).  
      
- e.g., Supervised classification.  
      
  
**(2) Inverse problem: $P(x|y)$**  
  
- $\leftarrow$ Generative models.  
      
- $y$를 주면 그 $y$가 나왔을 만한 parameter/input 추론 (Given $y$, infer parameters/input that likely produced it).  
      
- **Why difficult?**  
      
    1. **Ill-posed nature**: No unique solution, need regularization.  
          
    2. **High-dim spaces**: Data reside on complex manifolds.  
          
  
### **Challenges in Generative Modeling**  
  
**(1) Representation**  
  
- 어떻게 Random variable들을 join 할 것인가 (How to join random variables).  
      
- Compact representation이 필요 (Need compact representation).  
      
  
**(2) Learning**  
  
- How to estimate parameters?  
      
- MLE?  
      
  
**(3) Inference**  
  
- How to infer latent variables?  
      
  
---  
  
# 2. Latent Variable Models  
  
- **Latent Variable**  
      
    - Hidden variables that explain the observed data.  
          
    - $z \sim P(z)$ (Prior).  
          
    - $x \sim P(x|z)$ (Likelihood).  
          
    - $P(x) = \int P(x|z)P(z) dz$ (Marginal).  
          
  
### **Autoencoders (AE)**  
  
- **Goal**: Learn efficient coding of input data.  
      
- **Encoder**: $z = f(x)$.  
      
- **Decoder**: $\hat{x} = g(z)$.  
      
- **Loss**: $L(x, \hat{x}) = ||x - \hat{x}||^2$.  
      
- **Manifold Learning**: $z$ lives in lower dimension.  
      
- **Deterministic**: $z$ is a fixed vector.  
      
  
### **Variational Autoencoders (VAE)**  
  
- **Probabilistic spin** on AE.  
      
- **Encoder**: Outputs parameters of distribution $Q(z|x)$ (e.g., $\mu, \sigma$).  
      
    - $z \sim \mathcal{N}(\mu, \sigma^2 I)$.  
          
- **Decoder**: $P(x|z)$.  
      
- **Goal**: Maximize marginal likelihood $P(x)$.  
      
    - Intractable integral.  
          
  
**Evidence Lower Bound (ELBO)**  
  
- $\log P(x) \ge E_{z \sim Q}[\log P(x|z)] - D_{KL}(Q(z|x) || P(z))$  
      
    - **Term 1**: Reconstruction quality (Negative reconstruction error).  
          
    - **Term 2**: Regularization (Keep $Q$ close to Prior $P(z)$).  
          
    - **Maximize ELBO** $\Rightarrow$ Maximize $\log P(x)$.  
          
  
**Reparameterization Trick**  
  
- Problem: Cannot backpropagate through random sampling ($z \sim \mathcal{N}(\mu, \sigma)$).  
      
- Solution: Move randomness to input $\epsilon$.  
      
    - $z = \mu + \sigma \odot \epsilon$, where $\epsilon \sim \mathcal{N}(0, I)$.  
          
    - Now differentiable w.r.t. $\mu, \sigma$.  
          
  
---  
  
# 3. Generative Adversarial Networks (GAN)  
  
- **Concept**  
      
    - **Generator ($G$)**: Tries to fool $D$. (Create fake data).  
          
    - **Discriminator ($D$)**: Tries to distinguish real vs. fake.  
          
    - **Adversarial Game**: Minimax game.  
          
- **Objective Function**  
      
    - $\min_{G} \max_{D} V(D, G) = E_{x \sim P_{data}}[\log D(x)] + E_{z \sim P_{z}}[\log(1 - D(G(z)))]$  
          
    - **Discriminator**: Maximize correct classification.  
          
        - $D(x) \rightarrow 1$, $D(G(z)) \rightarrow 0$.  
              
    - **Generator**: Minimize $D$'s success (or maximize $D(G(z))$).  
          
- **Optimality**  
      
    - Optimal $D^*(x) = \frac{P_{data}(x)}{P_{data}(x) + P_{g}(x)}$.  
          
    - Global optimum: $P_{g} = P_{data}$.  
          
        - Value becomes $-\log 4$.  
              
        - Jensen-Shannon Divergence minimized.  
              
- **Issues in Training**  
      
    1. **Mode Collapse**: Generator produces limited variety of samples (decides on one "safe" output).  
          
    2. **Oscillations**: Parameters oscillate, don't converge.  
          
    3. **Vanishing Gradients**: If $D$ is too perfect, $G$ learns nothing.  
          
- **Variants**  
      
    - **DCGAN**: Deep Convolutional GAN. Guidelines for stable architecture (Batch Norm, Leaky ReLU, etc.).  
          
    - **WGAN (Wasserstein GAN)**: Uses Earth Mover's Distance. Smoother gradients.  
          
  
---  
  
# 4. Flow-based Models  
  
- **Normalizing Flows**  
      
    - Transform simple distribution (Gaussian) into complex data distribution via sequence of invertible mappings.  
          
    - $z \sim P(z)$ (Simple).  
          
    - $x = f(z)$, where $f$ is invertible ($z = f^{-1}(x)$).  
          
- **Change of Variables Formula**  
      
    - $P_x(x) = P_z(z) \left| \det \left( \frac{\partial f^{-1}(x)}{\partial x} \right) \right|$  
          
    - Log-likelihood:  
          
        - $\log P_x(x) = \log P_z(z) + \log | \det J |$  
              
    - **Exact Likelihood Estimation** possible!  
          
- **Characteristics**  
      
    - Invertible $f$.  
          
    - Jacobian determinant must be easy to compute. (e.g., Triangular matrix).  
          
  
---  
  
# 5. Diffusion Models  
  
- **Idea**  
      
    - **Forward process**: Gradually add noise until data becomes pure noise.  
          
        - $x_0 \rightarrow x_1 \rightarrow \dots \rightarrow x_T \sim \mathcal{N}(0, I)$.  
              
    - **Reverse process**: Learn to denoise step-by-step.  
          
        - $x_T \rightarrow \dots \rightarrow x_0$.  
              
- **Denoising Diffusion Probabilistic Models (DDPM)**  
      
    - Train a neural net to predict the noise $\epsilon_\theta(x_t, t)$ added at each step.  
          
    - Sampling: Iterative refinement.  
          
- **Score-based Generative Models**  
      
    - **Score Matching with Langevin Dynamics (SMLD)**.  
          
    - Estimate score function $\nabla_x \log P(x)$.  
          
    - Use Langevin dynamics to move towards high density regions.  
          
  
---  
  
# 6. Comparison of Models  
  
1. **GAN**: High quality samples, fast sampling. **Cons**: Unstable training, mode collapse, no explicit density.  
      
2. **VAE**: Fast sampling, explicit density (approx). **Cons**: Blurry samples (MSE loss issues).  
      
3. **Flow-based**: Exact likelihood, reversible. **Cons**: High computational cost, restricted architecture (invertible).  
      
4. **Diffusion**: High quality samples, diverse. **Cons**: Slow sampling (thousands of steps).  
      
  
---  
  
# 7. Autoregressive Models  
  
- **Explicit Density Models**  
      
    - Output depends on its own previous values.  
          
    - $P(x) = \prod_{i=1}^{d} P(x_i | x_{<i})$.  
          
    - Maximize Likelihood!  
          
- **Pros & Cons**  
      
    - **Pros**: Powerful (can model complex dependencies), stable training (MLE).  
          
    - **Cons**: Sequential generation $\rightarrow$ Slow (not parallelizable for sampling).  
          
- **Examples**  
      
    - **PixelRNN**: $x_i$ depends on left/top pixels. Sequential.  
          
    - **PixelCNN**: Use masked convolutions to enforce dependencies. Parallelizable training, but sequential generation.