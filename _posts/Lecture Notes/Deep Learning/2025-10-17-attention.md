---  
tags:  
  - attention  
  - deep-learning  
  - inductive-bias  
  - context-vector  
share: "true"  
github_title: 2025-10-17-attention  
title: 7. Attention  
date: 2025-10-17  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. Attention  
  
- **Attention**  
      
    - $\hookrightarrow$ Iterative process.  
          
    - Backprop trainable (differentiable).  
          
    - **Ex) NLP**:  
          
        - KR: 나는 학생 이다.  
              
        - English: I am a student.  
              
        - $\rightarrow$ $O(m^2)$ of weights.  
              
        - 이 값을 learning을 통해 알아내자 (Let's learn these values through learning).  
              
- **Seq-to-Seq modeling**  
      
    - $\hookrightarrow$ Dimension of context $C$ maybe too small to summarize long seq.  
          
    - [Graph: Performance vs Sequence Length (drops for long seq)]  
          
    - **Solution**: Attention focuses on relevant input part.  
          
        - Make $C$ a variable-length sequence.  
              
        - Associate $c^{(t)} \leftrightarrow y^{(t)}$.  
              
  
---  
  
# 2. Constructing context with attention  
  
- **Example**:  
      
    - $t$: I am a student (output).  
          
    - $t'$: 나는 학생 이다 (input).  
          
    - $C^{(t)} = \alpha^{(t,1)}h^{(1)} + \alpha^{(t,2)}h^{(2)} + \dots$  
          
    - $C^{(t)} = \sum_{t'=1}^{n_x} \alpha^{(t,t')} \cdot h^{(t')}$  
          
- **How to compute attention weight $\alpha$?**  
      
    - $\alpha^{(t,t')} = \frac{\exp(e^{(t,t')})}{\sum_{k=1}^{n_x} \exp(e^{(t,k)})}$  
          
        - (Softmax normalized $e^{(t,t')}$).  
              
    - $e^{(t,t')} = f(h^{(t')}, s^{(t-1)})$  
          
        - (Score function).  
              
        - Content-based attention.  
              
- **Score Functions ($f$)**  
      
    1. **Dot**: $s^T h$.  
          
    2. **General**: $s^T W h$.  
          
    3. **Concat**: $v_a^T \tanh(W[s;h])$.  
          
    4. **Scaled Dot-Product**: $\frac{s^T h}{\sqrt{n}}$.  
          
        - (내적 시 유사도가 $\sim \sqrt{n}$. $\sqrt{n}$으로 나눠서 scale 조정 - Similarity scales with $\sqrt{n}$, so divide to adjust).  
              
        - $||Q|| \approx ||K||$.  
              
- **Query-Key-Value Description**  
      
    - **Query**: Decoder hidden state ($s$).  
          
    - **Key**: Encoder hidden state ($h$).  
          
    - **Value**: Encoder hidden state ($h$).  
          
    - **Context vector**: Weighted sum of values.  
          
    - Weight: Function of (Query, Key).  
          
  
---  
  
# 3. Attention Types  
  
**(1) Cross vs Self**  
  
- **Cross-Attention**: Works on different sequences.  
      
    - (e.g., Translation: Source $\leftrightarrow$ Target).  
          
- **Self-Attention**: Different positions of a single sequence.  
      
    - (e.g., "The animal didn't cross the street because **it** was too tired").  
          
    - "it" $\leftrightarrow$ "animal".  
          
  
**(2) Soft vs Hard**  
  
- **Soft Attention**:  
      
    - Continuous / probabilistic weights.  
          
    - Differentiable.  
          
    - High compute.  
          
    - Attention weights: all patches.  
          
    - $Context = \sum (\text{attention map} \times \text{img feature})$.  
          
- **Hard Attention**:  
      
    - Discrete / specific selection.  
          
    - Non-differentiable (Requires Reinforcement Learning / Variational Inference).  
          
    - $Context = \text{features randomly sampled from attention map}$.  
          
  
**(3) Global vs Local**  
  
- **Global**: Attend to all source tokens.  
      
- **Local**: Attend to a window of tokens.  
      
  
---  
  
# 4. Remarks  
  
- **Attention Pros and Cons**  
      
    - **Pros**:  
          
        - Global dependency handling.  
              
        - Handling long sequences.  
              
        - Parallelizable (Self-attention).  
              
        - Interpretable (Attention maps).  
              
    - **Cons**:  
          
        - Computational cost: $O(L^2)$ (Quadratic with sequence length).  
              
        - **Weak inductive bias**:  
              
            - Better expressive power but **less sample efficiency**.  
                  
            - (Needs more data to learn patterns than CNN/RNN).  
                  
            - [Diagram: CNN (Local) vs Attention (Global)].