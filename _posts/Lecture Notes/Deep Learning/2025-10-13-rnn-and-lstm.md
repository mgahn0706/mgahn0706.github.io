---  
tags:  
  - deep-learning  
  - rnn  
  - parameter-sharing  
  - lstm  
  - state  
share: "true"  
github_title: 2025-10-13-rnn-and-lstm  
title: 6. RNN and LSTM  
date: 2025-10-13  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# 1. RNN (Recurrent Neural Networks)  
  
- **RNN**  
      
    - $\hookrightarrow$ A family of neural networks for processing sequential data.  
          
    - $x^{(1)}, \dots, x^{(\tau)}$  
          
    - **Dynamical system**.  
          
        1. $s^{(t)} = f_{\theta}(s^{(t-1)})$  
              
    - $\hookrightarrow$ **Parameter sharing** (same weight & bias) $\rightarrow$ better generalization.  
          
        - Parameter # $\downarrow \downarrow$.  
              
    - $s^{(t)} = f_{\theta}(s^{(t-1)}, x^{(t)})$  
          
- **General RNN formulation**  
      
    - $h^{(t)} = f_{\theta}(h^{(t-1)}, x^{(t)})$  
          
        - $h^{(t)}$: new state  
              
        - $h^{(t-1)}$: old state  
              
        - $x^{(t)}$: input  
              
    - **Parameter sharing**: same $f$, same $\theta$.  
          
    - $\hookrightarrow$ **Output layers**: read info out of $h$.  
          
        - $y^{(t)} = softmax(W h^{(t)} + b)$  
              
    - **Role of hidden units**: Lossy summary of task-relevant aspects of $x^{(1)} \dots$.  
          
- **Simple RNN**  
      
    - $h^{(t)} = f_{\theta}(h^{(t-1)}, x^{(t)})$  
          
        - $= \tanh(W_{hh}h^{(t-1)} + W_{hx}x^{(t)} + b_h)$  
              
    - $h$: 다 저장할 수 없으니 $h_t$에 저장 (Can't store everything, so store in $h_t$).  
          
    - [Equation diagram]  
          
    - $y^{(t)} = softmax(W_{yh} h^{(t)} + b_y)$  
          
  
---  
  
### **RNN Training**  
  
- $\hookrightarrow$ Same parameters ($W_{hx}, W_{hh}, W_{yh}, b_h, b_y$).  
      
- Loss: $\prod_t P(y^{(t)} | x^{(1)} \dots x^{(t)})$.  
      
- $L = - \sum_{t} \log P(y^{(t)} | x^{(1)} \dots x^{(t)})$.  
      
- **BPTT (Backpropagation Through Time)**  
      
    - $\hookrightarrow$ Run forward for time $\tau$.  
          
    - $\hookrightarrow$ Run backward for time $\tau$.  
          
    - **Problem**: Gradient Vanishing / Exploding.  
          
        - $h^{(t)} = W h^{(t-1)}$.  
              
        - If $W$ has spectral radius $\rho < 1$: Decay $\rightarrow$ **Vanishing**.  
              
            - (Short-term dependency only).  
                  
        - If $\rho > 1$: Explode $\rightarrow$ **Exploding**.  
              
            - (Gradient clipping needed).  
                  
- **Truncated BPTT**  
      
    - Run forward / backward for $k$ steps.  
          
    - Carry hidden state, but stop gradient.  
          
  
---  
  
### **RNN Types**  
  
**(1) One-to-One**  
  
- Vanilla Neural Networks.  
      
  
**(2) One-to-Many**  
  
- Image Captioning.  
      
- (Image $\rightarrow$ Sequence of words).  
      
  
**(3) Many-to-One**  
  
- Sentiment Classification.  
      
- (Sequence of words $\rightarrow$ Sentiment).  
      
  
**(4) Many-to-Many**  
  
- Machine Translation.  
      
- (Seq $\rightarrow$ Seq).  
      
- Video classification (Frame level).  
      
  
**(5) Bidirectional RNN**  
  
- $y^{(t)}$ depends on whole input sequence.  
      
- Forward RNN + Backward RNN.  
      
- Concatenate hidden states.  
      
  
**(6) Deep RNN (Multi-layer)**  
  
- Stack hidden layers.  
      
- Higher level representation.  
      
  
---  
  
# 2. LSTM (Long Short-Term Memory)  
  
- **Motivation**  
      
    - $\hookrightarrow$ Fight vanishing gradient.  
          
    - Can learn long-term dependencies.  
          
    - Easy to pass information unchanged.  
          
    - **Idea**: $C^{(t)} = C^{(t-1)} + \Delta C^{(t)}$  
          
        - (ResNet-like structure).  
              
        - $\hookrightarrow$ Gradient flows well ($1 + \dots$).  
              
- **Structure**  
      
    - **Hidden state ($h^{(t)}$)**: Short-term memory.  
          
    - **Cell state ($C^{(t)}$)**: Long-term memory.  
          
        - $\hookrightarrow$ 고속도로 (Highway).  
              
    - $\tanh$: $-1 \sim 1$. 정보가 계속 급변하는 것을 막음 (Prevents information from changing too rapidly).  
          
        - (+ backward compatibility as RNN).  
              
- **Gates**  
      
    - $\hookrightarrow$ A sigmoid neural net.  
          
    - $\hookrightarrow$ Element-wise multiplication.  
          
    - [Gate logic diagram: $0.2 \times 1 \rightarrow \dots$]  
          
    - $\Rightarrow$ 얼마나 통과할지 결정 (Decide how much to pass).  
          
    - $0 \le output \le 1$.  
          
    - $\hookrightarrow$ LSTM has 3 gates (forget, input, output).  
          
  
### **LSTM Steps**  
  
**(1) Decide what info to throw away from cell state (Forget Gate)**  
  
- For $C^{(t-1)}$, looks at $h^{(t-1)}$ and $x^{(t)}$.  
      
- $f^{(t)} = \sigma(W_f [h^{(t-1)}, x^{(t)}] + b_f)$  
      
- $0 \le f \le 1$ (Gate).  
      
  
**(2) Decide new information to store (Input Gate)**  
  
- (i) A sigmoid layer decides which value to update (**Input Gate**).  
      
    - $i^{(t)} = \sigma(W_i [h^{(t-1)}, x^{(t)}] + b_i)$  
          
- (ii) A tanh layer creates a vector of candidate values (**Candidate Cell State**).  
      
    - $\tilde{C}^{(t)} = \tanh(W_C [h^{(t-1)}, x^{(t)}] + b_C)$  
          
  
**(3) Update old cell state $C^{(t-1)} \rightarrow C^{(t)}$**  
  
- $C^{(t)} = f^{(t)} \odot C^{(t-1)} + i^{(t)} \odot \tilde{C}^{(t)}$  
      
- Note: $f + i \neq 1$ necessarily.  
      
  
**(4) Decide what to output (Output Gate)**  
  
- (i) Run a sigmoid to decide what parts to output (**Output Gate**).  
      
    - $o^{(t)} = \sigma(W_o [h^{(t-1)}, x^{(t)}] + b_o)$  
          
- (ii) Cell state through tanh, multiply it.  
      
    - $h^{(t)} = o^{(t)} \odot \tanh(C^{(t)})$  
          
  
### **Gradient Flow in LSTM**  
  
- $\hookrightarrow$ For training.  
      
- Backpropagation path along $C^{(t)}$ allows gradient to flow uninterrupted (Additive update).  
      
- Only element-wise multiplication by forget gate.  
      
  
---  
  
# 3. GRU (Gated Recurrent Unit)  
  
- **Concept**  
      
    - Simplify LSTM.  
          
    - Combine forget & input gates into **Update Gate**.  
          
    - Merge cell state & hidden state.  
          
- **Equations**  
      
    - **Update Gate ($z$)**: $z_t = \sigma(W_z \cdot [h_{t-1}, x_t])$  
          
    - **Reset Gate ($r$)**: $r_t = \sigma(W_r \cdot [h_{t-1}, x_t])$  
          
    - **New Memory Content**: $\tilde{h}_t = \tanh(W \cdot [r_t \odot h_{t-1}, x_t])$  
          
    - **Final Memory**: $h_t = (1-z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$  
          
        - (If $z_t \approx 1$, ignore old memory).  
              
        - (If $z_t \approx 0$, keep old memory).