---  
tags:  
  - deep-learning  
  - transformer  
  - attention  
  - decoder  
  - encoder  
share: "true"  
github_title: 2025-10-17-transformer-basic  
title: 8. Transformer Basic  
date: 2025-10-17  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. Introduction  
  
- **RNN and LSTM era**  
      
    - Fixed size context vector forced to summarize long sequences.  
          
    - Vanishing/Exploding gradient.  
          
- **Attention**  
      
    - $\hookrightarrow$ Selectively focus on relevant parts.  
          
- **Introducing the Transformer**  
      
    - $\hookrightarrow$ "Attention is all you need".  
          
    - Enable massive parallelism (in training).  
          
    - (1) Compute path length.  
          
- **Transformer: A Seq-to-Seq model**  
      
    - Encoder $\rightarrow$ Decoder.  
          
    - [Stack of Encoders] $\rightarrow$ [Stack of Decoders].  
          
    - Input (I am a student) $\rightarrow$ Output (Je suis étudiant).  
          
  
---  
  
# 2. Encoder  
  
- **All identical in structure (do not share weights)**.  
      
- **Structure**:  
      
    1. **Self-Attention**: Help encoder look at other words in the input sentence as it encodes a specific word. (Short-term memory).  
          
    2. **Feed Forward Neural Network**: Non-linear. The exact same feed-forward net is independently applied to each position. (Long-term memory).  
          
- **Preprocessing**  
      
    - **Tokenization**: Text $\rightarrow$ Token.  
          
    - **Word Embedding**: Token $\rightarrow$ Vector.  
          
        - Uses a real-valued dense vector to represent each word.  
              
        - (Learned separately from Transformer).  
              
        - 기존에는 Count 기반이라 너무 sparse (Previously count-based, too sparse).  
              
        - Allows words with a similar meaning have a similar representation.  
              
        - (e.g., King-Man+Woman = Queen).  
              
    - Applied for first encoder only.  
          
- **Flow**:  
      
    - Input $\rightarrow$ Word Embedding $\rightarrow$ [Self-Attention $\rightarrow$ Z (Contextual part) $\rightarrow$ FFNN] $\rightarrow$ Output.  
          
  
---  
  
# 3. Contextualizing with Self-Attention  
  
- **Goal**: Embed a vector for each word.  
      
- **Self-Attention**:  
      
    - "The animal didn't cross the street because **it** was too tired."  
          
    - $\hookrightarrow$ "it" is associated with "animal".  
          
- **Process**:  
      
    1. **Create 3 vectors**: Query ($q$), Key ($k$), Value ($v$).  
          
        - Multiply input embedding $X$ by weight matrices $W^Q, W^K, W^V$.  
              
    2. **Calculate Score**:  
          
        - $q \cdot k$ (Dot product).  
              
        - Score determines focus.  
              
    3. **Divide by $\sqrt{d_k}$**:  
          
        - To have stable gradients. (Scale).  
              
    4. **Softmax**:  
          
        - Normalize scores to probability distribution.  
              
    5. **Multiply by Value ($v$)**:  
          
        - Keep intact values of focused words, drown-out irrelevant words.  
              
    6. **Sum**:  
          
        - $Z = \sum v \times softmax(\dots)$.  
              
  
**Matrix Calculation of Self-Attention**  
  
- $Z = Softmax(\frac{Q \cdot K^T}{\sqrt{d_k}}) \cdot V$  
      
  
---  
  
# 4. Multi-Head Attention  
  
- **Motivation**:  
      
    1. Expand model's ability to focus on different positions.  
          
    2. Give attention layer multiple "representation subspaces".  
          
- **Mechanism**:  
      
    - Have multiple sets of Query/Key/Value weight matrices ($W_0, \dots, W_7$).  
          
    - Calculate $Z_0, \dots, Z_7$ separately.  
          
    - **Concatenate** all $Z$ matrices.  
          
    - Multiply by an additional weights matrix $W^O$.  
          
    - Result: Final $Z$ matrix captures information from all heads.  
          
  
**Positional Encoding**  
  
- Transformer doesn't use recurrence/convolution $\rightarrow$ No notion of order.  
      
- **Solution**: Add vector to each input embedding.  
      
- **Formula**:  
      
    - $PE_{(pos, 2i)} = \sin(pos / 10000^{2i/d_{model}})$  
          
    - $PE_{(pos, 2i+1)} = \cos(pos / 10000^{2i/d_{model}})$  
          
- **Residual Connection & Layer Normalization**:  
      
    - Each sub-layer (Self-attention, FFNN) has residual connection around it, followed by Layer Norm.  
          
    - $LayerNorm(x + Sublayer(x))$.  
          
  
---  
  
# 5. Decoder  
  
- **Structure**:  
      
    1. **Masked Multi-Head Attention**: Self-attention on decoder output. Mask future positions.  
          
    2. **Encoder-Decoder Attention** (Cross-Attention): Query from Decoder, Key/Value from Encoder.  
          
    3. **Feed Forward**.  
          
- **Masked Self-Attention**:  
      
    - Prevent positions from attending to subsequent positions.  
          
    - "Illegal connection" masked out (set to $-\infty$ before softmax).  
          
- **Final Linear and Softmax Layer**  
      
    - Decoder output (float vector) $\rightarrow$ Word probability.  
          
    - **Linear**: Project to logits (size of vocab).  
          
    - **Softmax**: Logits $\rightarrow$ Probabilities.  
          
  
---  
  
# 6. Inference (Decoding Strategies)  
  
- **(1) Greedy Decoding**  
      
    - Pick the single word with highest probability at each step.  
          
- **(2) Beam Search**  
      
    - Keep track of $k$ (beam size) most promising sentences.  
          
    - Example ($k=2$):  
          
        - Step 1: Select top 2 words ("I", "The").  
              
        - Step 2: For each, expand next possible words, keep top 2 total paths.  
              
    - Note: $k=1$ is Greedy decoding.  
          
- **(3) Stochastic Decoding**  
      
    - **Top-k Sampling**: Sample from top-k most probable words.  
          
        - Avoids repetition/loops.  
              
    - **Top-p Sampling (Nucleus)**: Sample from smallest set of words whose cumulative probability exceeds $p$.  
          
        - Dynamic $k$.  
              
- **Training vs Inference**  
      
    - **Training**: Parallelizable (Teacher Forcing).  
          
        - Use ground truth as input to decoder.  
              
    - **Inference**: Sequential (Auto-regressive).  
          
        - Output of step $t$ becomes input of step $t+1$.