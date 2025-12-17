---  
tags:  
  - deep-learning  
  - kv-cache  
  - cache  
  - attention  
  - transformer  
share: "true"  
github_title: 2025-10-18-transformer-updates  
title: 9. Transformer Updates  
date: 2025-10-18  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. Attention Bottleneck & Solutions  
  
- **Attention bottleneck**  
      
    - $\hookrightarrow$ computationally expensive.  
          
    - masked self-attention & autoregressive decoding.  
          
    - **Overcome $O(N^{2})$ bottleneck!**  
          
    - $\hookrightarrow$ $n \times n$ matrix of attention scores.  
          
  
**Strategies to Overcome:**  
  
1. **Sparse/Local Attention**  
      
2. **Linear Attention**: Kernel approximation of softmax.  
      
3. **Hashing/Clustering**  
      
4. **IO-aware Acceleration**  
      
  
---  
  
### **(1) Sparse Attention**  
  
- Tokens limit the context.  
      
- **Ex) Big Bird**  
      
    - Random attention.  
          
    - Self-attention.  
          
- **Ex) GPT-3 Sparse Attention**  
      
    - Global attention (few fully connected tokens).  
          
    - Local attention.  
          
  
**Diagram: Transformer Block**  
  
- [Feed F] $\rightarrow$ [Layer Norm] $\rightarrow$ (+)  
      
- $\uparrow$  
      
- (+) $\leftarrow$ [MHA Self-Att] $\leftarrow$ [Layer Norm]  
      
  
---  
  
### **(2) Linear Attention**  
  
- $\hookrightarrow$ Note: $(AB)C = A(BC)$  
      
- **Original**: $(Q K^{T}) \cdot V \Rightarrow O(n \cdot d \cdot n + n \cdot n \cdot d) = O(n^{2})$  
      
    - ($n \times d$) ($d \times n$) ($n \times d$)  
          
- **Linear**: $Q(K^{T}V) \rightarrow O(n \cdot d \cdot d + d \cdot n \cdot d) = O(n)$  
      
    - ($n \times d$) ($d \times n$) ($n \times d$)  
          
- **Barrier**: Softmax is the barrier.  
      
    - $Attention(Q,K,V) = Softmax(\frac{Q K^{T}}{\sqrt{d_{k}}})V$  
          
    - $\approx \exp[Q K^{T}]V$  
          
    - $\approx (\phi(Q)\phi(K)^{T})V$  
          
    - $= \phi(Q) \{ \phi(K)^{T} \cdot V \} \rightarrow O(n)$  
          
- **Proof**:  
      
    - $Softmax(Q K^{T})_{ij} = \frac{\exp(q_{i}^{T}k_{j})}{\sum_{j'} \exp(q_{i}^{T}k_{j'})}$  
          
    - $\exp(q_{i}^{T}k_{j}) \simeq <\phi(q_{i}), \phi(k_{j})>$  
          
    - where $\phi: \mathbb{R}^{d} \mapsto \mathbb{R}^{d'}$  
          
    - $d' \rightarrow \infty$ 이면 등호 성립 (Equality holds if $d' \rightarrow \infty$).  
          
  
---  
  
### **(3) Grouping Similar Tokens (Hashing/Clustering)**  
  
**Locality-Sensitive Hashing (LSH)**  
  
- Vectors $\rightarrow$ Hash code.  
      
- $\hookrightarrow$ **Reformer**  
      
    - Hashes Q, K into bucket based on similarity.  
          
    - Attention on within each bucket.  
          
    - $O(n \log n)$ for sorting.  
          
  
**Routing Attention**  
  
- $\hookrightarrow$ Semantic grouping.  
      
- Tokens are assigned to different clusters.  
      
- $O(nk)$ complexity.  
      
  
**Sparse Sinkhorn Attention**  
  
- $\hookrightarrow$ Broken down input.  
      
- k-means.  
      
- A neural net learns permutation $P$.  
      
- $\hookrightarrow$ $O(n \log n)$  
      
  
---  
  
### **(4) Flash Attention (IO-Ware)**  
  
- $\hookrightarrow$ Significant speed up.  
      
- **Hardware**: GPU, SRAM, HBM.  
      
- **Concept**: Optimize what values are loaded and moved.  
      
  
---  
  
# 2. KV Caching  
  
- **KV Caching**  
      
    - $\hookrightarrow$ Two basic facts:  
          
        1. Generates one token at a time.  
              
        2. Output token is appended to the prompt (redundant).  
              
    - Enhance autoregressive text gen.  
          
    - Caches the key-value matrices of previous tokens.  
          
- **Usage**  
      
    - $\hookrightarrow$ Primarily and most crucially used for **masked self-attention for decoding**.  
          
    - Cross-attention.  
          
    - $\rightarrow$ but **NOT USED** for non-masked self attention (encoder).  
          
        - $\hookrightarrow$ Only computed once.  
              
- **KV-Cache Bottleneck**  
      
    - $\hookrightarrow$ Read from VRAM for every single new token.  
          
    - **Bandwidth bottleneck (HBM)**.  
          
    - Goal: Reduce KV cache size!  
          
  
---  
  
### **Mitigating KV Cache Bottleneck**  
  
- $\hookrightarrow$ Auto-regressive decoding K, V for all tokens.  
      
  
**Standard MHA (Multi-Head Attention)**  
  
- $\hookrightarrow$ Own KV matrices for every attention head.  
      
- $d \times d_{h}$ where $d = d_{h} \times \# \text{of head}$.  
      
- $W^{Q}, W^{K}, W^{V}$. ($W^{Q}$ cache X).  
      
  
**Multi-Query and Grouped-Query Attention**  
  
- $\hookrightarrow$ KV cache size는 결국 K/V 관계 크기와 head 수 (KV cache size depends on K/V relation size and # of heads).  
      
  
**Diagrams:**  
  
- **Grouped (GQA)**: $V, K$ shared by groups of $Q$.  
      
- **Multi-query (MQA)**: $V, K$ shared by all $Q$.  
      
- **Multi-Query Attention (MQA)**  
      
    - cf) Multi-head attention: Head 마다 QKV 다름.  
          
    - **Shares K, V matrix**.  
          
- **Grouped-Query Attention (GQA)**  
      
    - $\hookrightarrow$ Model size가 늘면, MQA의 성능 $\downarrow$ (If model size increases, MQA performance decreases).  
          
  
---  
  
### **Multi-Head Latent Attention (MLA)**  
  
- $\hookrightarrow$ Jointly compresses keys-values into latent vector.  
      
- Dramatically shrinks the data in KV Cache.  
      
  
**Note:**  
  
- $d = d_{model}$ (embedding size).  
      
- $x \in \mathbb{R}^{1 \times d}$: single new token.  
      
- $H$: Head 개수 (# of heads).  
      
- $d_{h} = d_{k} = d_{v} = d_{q}$ ($d$ per head).  
      
- $d_{c}$: Compressed $d$.  
      
- $n$: Sequence length.  
      
- Assume heads are concatenated.  
      
  
**Operation (Standard MHA)**  
  
1. **Query Projection**: $q = x \cdot W^{Q}$ ($1 \times d$).  
      
2. **Key, Value Projection**:  
      
    - $K = X \cdot W^{K}$ ($n \times d$)  
          
    - $V = X \cdot W^{V}$ ($n \times d$)  
          
3. **Cache Update**:  
      
    - $K \rightarrow K_{cache}$ ($n \times d$)  
          
    - $V \rightarrow V_{cache}$ ($n \times d$)  
          
4. **Attention Scores**:  
      
    - $s = q \cdot K_{cache}^{T}$ ($1 \times n$)  
          
5. **Head Outputs**:  
      
    - $a = Softmax(s / \sqrt{d_{h}})$ ($1 \times n$)  
          
    - $O_{concat} = a \cdot V_{cache}$ ($1 \times d$)  
          
6. **Final Output**:  
      
    - $O_{final} = O_{concat} \cdot W^{O}$ ($1 \times d$)  
          
  
**MLA Mechanism**  
  
- Maintain expressiveness ($d_{h} = d/H$).  
      
- $\Rightarrow Key \leftrightarrow Query$.  
      
  
**MLA: Low-rank KV Joint Compression**  
  
- $\hookrightarrow$ Head-aware decompression. Expressive maintained.  
      
  
**(1) Compression**  
  
- Basic: $K = x W^{K}, V = x W^{V}$  
      
- **MLA: Latent KV**  
      
    - $C_{KV} = X \cdot W_{D}^{KV}$  
          
    - $d$차원 $\rightarrow$ $d_{c}$차원 ($1 \times d_{c}$).  
          
    - (Why? K, V originate from a single encoder vector!)  
          
    - $dim(C_{KV}) = d_{c} \ll H(d_{k} + d_{v}) = 2d$  
          
  
**(2) Decompression**  
  
- $\hookrightarrow$ MLA recovers full K, V.  
      
- $K_{cache} = [K_{1}, \dots, K_{H}] = C_{KV} \cdot W_{U}^{K}$ ($n \times d$).  
      
- $V_{cache} = [V_{1}, \dots, V_{H}] = C_{KV} \cdot W_{U}^{V}$ ($n \times d$).  
      
    - $\rightarrow$ Learned up-projection matrix.  
          
- $\Rightarrow$ 매번 Decompress 하면 $O(n^2)$임. 즉, implicitly up-projection을 이용함 (**Weight-absorption trick**).  
      
  
---  
  
### **Weight Absorption Trick**  
  
- Original Output Calculation:  
      
    - $O_{final} = Softmax(\frac{1}{\sqrt{d_{h}}} \cdot x W^{Q} \cdot (C_{KV} \cdot W_{U}^{K})^{T}) (C_{KV} W_{U}^{V}) W^{O}$  
          
- Rearranging:  
      
    - $= Softmax(\frac{1}{\sqrt{d_{h}}} \cdot x \cdot (W^{Q} \cdot W_{U}^{K^{T}}) \cdot C_{KV}^{T}) \cdot C_{KV} \cdot (W_{U}^{V} W^{O})$  
          
- **Absorbed Weights**:  
      
    - $W_{new}^{Q} = W^{Q} \cdot W_{U}^{K^{T}}$  
          
    - $W_{new}^{O} = W_{U}^{V} \cdot W^{O}$  
          
- **Simplified**:  
      
    - $= Softmax(\frac{1}{\sqrt{d_{h}}} \cdot (x W_{new}^{Q}) \cdot C_{KV}^{T}) \cdot C_{KV} \cdot W_{new}^{O}$  
          
    - Latent space에서 Attention을 구한다 (Calculate attention in latent space).  
          
  
---  
  
# 3. Positional Embeddings  
  
### **Absolute Positional Embedding (APE)**  
  
- Fixed positional representation.  
      
- $E = X + P$ (Fixed Embedding or Learned Embedding).  
      
- **Sinusoidal Embedding**:  
      
    - Simple, effective.  
          
    - Compatible with KV Caching.  
          
    - 길면 성능 $\downarrow$ (Performance drops if sequence is long).  
          
  
### **Relative Positional Embedding (RPE)**  
  
- $\hookrightarrow$ Relative ($i-j$) depend.  
      
- $q_{i} \cdot (k_{j} + r_{i-j})$  
      
- Bias.  
      
- $\hookrightarrow$ More semantically relevant in language.  
      
- $\hookrightarrow$ Better generalization.  
      
- **Cons**:  
      
    - Complex & Slow: Pairwise.  
          
    - Information loss.  
          
    - Incompatibility with KV Caching.  
          
  
### **RoPE (Rotary Positional Embedding)**  
  
- **Rotation Matrix $R_{\theta}$**:  
      
    - $R_{\theta} = \begin{bmatrix} \cos(m\theta) & -\sin(m\theta) \\ \sin(m\theta) & \cos(m\theta) \end{bmatrix}$  
          
- **Application**:  
      
    - $\tilde{q}_{i} = q_{i} R_{i}$  
          
    - $\tilde{k}_{j} = k_{j} R_{j}$  
          
- **Attention Score**:  
      
    - $(\tilde{i}, \tilde{j}) = \tilde{q}_{i} \cdot \tilde{k}_{j}^{T}$  
          
    - $= q_{i} R_{i} \cdot (k_{j} \cdot R_{j})^{T}$  
          
    - $= q_{i} (R_{i} \cdot R_{j}^{T}) k_{j}^{T}$  
          
    - $= q_{i} R_{i-j} \cdot k_{j}^{T}$  
          
    - $\hookrightarrow$ **Relative distance**.  
          
    - $\Rightarrow$ $R_{p}$는 Parameter-free.  
          
  
**RoPE Matrix Structure**:  
  
- $\Theta = \{ \theta_{i} = 10000^{-2(i-1)/d} \}$  
      
- Block diagonal matrix with rotation blocks.  
      
    - $\begin{bmatrix} \cos m\theta_{1} & -\sin m\theta_{1} & 0 & 0 \\ \sin m\theta_{1} & \cos m\theta_{1} & 0 & 0 \\ 0 & 0 & \ddots & \\ 0 & 0 & & \end{bmatrix}$  
          
- $m$: Token position index.  
      
  
---  
  
# 4. Modern Transformer Updates  
  
### **Transformer Block Updates**  
  
**Diagram**:  
  
- [FF]  
      
- $\uparrow$  
      
- [RMS Norm]  
      
- $\uparrow$  
      
- [Self-Attention]  
      
- $\uparrow$  
      
- [RMS Norm]  
      
    - $\hookrightarrow$ Layer Norm 변형 (Variant of Layer Norm).  
          
  
**Pre-normalization**  
  
- Pre-layer norm.  
      
- Gradients at init + No warm-up required.  
      
- (+ stability and efficiency).  
      
- Performance가 낮아지긴 하나... (Performance might drop slightly...).  
      
  
**RMS Norm (Root Mean Square Normalization)**  
  
- $\hookrightarrow$ LayerNorm 변형 (Layer 마다 계산).  
      
- Data 1개마다 (Per single data).  
      
- $\bar{x}_{norm} = \frac{x}{RMS(x) + \epsilon} \odot g$  
      
- $RMS(x) = \sqrt{\frac{1}{n} \sum_{i=1}^{n} x_{i}^{2}}$  
      
  
**SwiGLU Activation Function**  
  
- Linear $\odot$ Swish.  
      
- Non-linear, Differentiable.  
      
  
### **Multi-token Prediction**  
  
- $\hookrightarrow$ Train LLM to predict future token $\hat{x}_{t+1}, \hat{x}_{t+2}, \dots$  
      
- Structure:  
      
    - $h_{4} \rightarrow$ [Head 1] $\rightarrow \hat{x}_{5}$  
          
    - $h_{4} \rightarrow$ [Head 2] $\rightarrow \hat{x}_{6}$  
          
    - $h_{4} \rightarrow$ [Head 3] $\rightarrow \hat{x}_{7}$  
          
- In serial $\rightarrow$ DeepSeek.