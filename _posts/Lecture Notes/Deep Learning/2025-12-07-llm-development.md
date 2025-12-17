---  
tags:  
  - LLM  
  - deep-learning  
  - fine-tuning  
share: "true"  
github_title: 2025-12-07-llm-development  
title: 17. LLM Development  
date: 2025-12-07  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# Pretraining  
  
- Text $\rightarrow$ Text model  
      
- 1~3% unstructured data  
      
- **Transformer 사용방법**  
      
    - ↳ Encoder  
          
    - ↳ Decoder  
          
    - ↳ Encoder-Decoder  
          
  
## (1) Encoder-only model (Autoencoding)  
  
- [Mask]  
      
- **Goal**: Reconstruct text (Bidirectional)  
      
- **Good at**: Sentiment analysis.  
      
- **Ex**: BERT, RoBERTa  
      
  
## (2) Decoder-only (Autoregressive)  
  
- [Mask] (Forward masking)  
      
- **Goal**: Predict next token (Unidirectional)  
      
- ↳ Emergent behavior  
      
- **Ex**: GPT, BLOOM  
      
  
## (3) Encoder-Decoder model (Seq-to-Seq model)  
  
- ↳ Recon span.  
      
- **Ex**: T5, BART  
      
  
# LLM Development  
  
## (1) Prompt Engineering  
  
- **① Direct prompting (Zero shot)**  
      
    - ↳ No ex. Just instruction  
          
- **② One shot**  
      
    - ↳ One clear example  
          
- **③ Few- / Multi-shot prompting**  
      
    - Better at complex task  
          
    - But, LLM can not do complex task prompting alone.  
          
    - Revise the prompt $\rightarrow$ Chain-of-Thought Prompting  
          
- **Chain-of-Thought Prompting**  
      
    - ↳ Encourage LM to reasoning  
          
    - $\Rightarrow$ 내 사고 과정을 보여주자. (Example 없이도 되나?)  
          
    - Add instruction, feature, architecture, objective prompt.  
          
  
## (2) Instruction Tuning  
  
- **Motive**: Base LLM are not aligned with users' intent.  
      
    - ↳ We need alignment to bridge the gap!  
          
- **Approaches**  
      
    - **① Zero-/Few-shot prompting for in-context learning** (Due to emergent ability)  
          
        - ↳ Tuning-free  
              
        - ↳ Limit to what you fit in context-length  
              
    - **② SFT (Tuning-based alignment)**  
          
        - Gradient updates  
              
  
# Instruction Tuning Process  
  
- Unsupervised Pretrained Base LLM (GPT) $\xrightarrow{\text{Supervised}}$ Fine-tuned LLM.  
      
- **Instruction tuning (First fine-tuning)**  
      
    - Instructional prompt + LLM Output $\rightarrow$ Outputs  
          
    - $\Rightarrow$ 하나만 해서는 안되고, in-general 해야 함  
          
- **Process**:  
      
    - Prompt $\rightarrow$ Pre-trained LLM $\rightarrow$ Label  
          
    - Loss: CE (Cross Entropy)  
          
    - Supervised Learning.  
          
- **Catastrophic forgetting**  
      
    - ↳ 하나만 학습시키면 멍청해짐.  
          
    - Fine-tune on multiple tasks  
          
    - ↳ **Multi-task instruction tuning.**  
          
  
## Parameter-efficient Fine tuning (PEFT) Comparison  
  
- **① Supervised (SFT, BERT, T5)**: Base LM $\rightarrow$ Fine-tune on A, A  
      
- **② Prompting for in-context learning (GPT-3)**: Base LM  
      
- **③ Instruction tuning (FLAN)**:  
      
    - Tasks A, B, C, D $\rightarrow$ Base LM  
          
    - Inference of unseen.  
          
  
# FLAN & Human Preference  
  
- **FLAN**  
      
    - ↳ Set of instruction for instruction tuning.  
          
    - Pretraining의 dessert 느낌.  
          
- **Limitation**  
      
    - ① Expensive to collect truth data  
          
    - ② Some tasks has no answer  
          
    - ③ Human generates suboptimal  
          
- **Optimizing Human Preference (Second fine tuning)**  
      
    - LM objective $\ne$ Human preference  
          
- **Align with human preference**  
      
    - ↳ Helpful, Honest, Harmless  
          
    - : Instruction tuning + Preference tuning  
          
  
## RLHF (Reinforcement Learning from Human Feedback)  
  
- Instruction $\rightarrow$ Human feedback $\rightarrow$ Human-aligned  
      
- **Reinforcement Learning**  
      
    - ↳ Train an agent to make seq. to decision maximizing a cumulative reward.  
          
- **Steps in RLHF**  
      
    - ① Supervised fine tuning (SFT)  
          
    - ② Human feedback + Reward model  
          
        - By rank  
              
        - ↳ RM predicts by score  
              
    - ③ Fine-tuning with RL  
          
        - ↳ Using RL algorithm (PPO)  
              
  
# RLHF Details  
  
## (1) Supervised fine-tuning (SFT)  
  
- ① Sampled from a prompt dataset  
      
- ② Human labeler writes response  
      
- ③ Fine-tune LLM $\rightarrow$ Instruct LLM  
      
  
## (2) Reward Model  
  
- ① Human labeler ranks outputs  
      
- ② Train RM  
      
- **Bradley-Terry (BT) preference model**  
      
    - ↳ Pairwise comparisons  
          
    - $P(i>j) = \frac{\exp(\beta_i)}{\exp(\beta_i) + \exp(\beta_j)} = \frac{1}{1 + e^{-(\beta_i - \beta_j)}}$  
          
    - (Softmax $\rightarrow$ Sigmoid)  
          
    - $= \sigma(\beta_i - \beta_j)$  
          
    - $\therefore \mathcal{L} = -\log \sigma(\beta_i - \beta_j)$  
          
    - ↳ Pairwise comparison for n-completion.  
          
    - $nC_2 \rightarrow$ Change $(x, y_w, y_l)$  
          
        - $(x, y_w) \rightarrow (RM) \rightarrow r_\phi(x, y_w) = r_w$  
              
        - $(x, y_l) \rightarrow (RM) \rightarrow r_\phi(x, y_l) = r_l$  
              
        - Loss: $-\log \sigma(r_w - r_l)$  
              
    - Gradient update  
          
  
## (3) Fine-tuning  
  
- Optimize policy with PPO.  
      
- Updated LLM is Instruct LLM.  
      
- ② Updates LLM by RL (PPO)  
      
    - GPT uses PPO (Proximal Policy Optimization) RL.  
          
  
# Other Optimization Methods  
  
- **DPO (Direct Preference Optimization)** (Not RL)  
      
    - Tunes LLM without RL  
          
    - $\mathcal{L}_{DPO} = -\log \sigma(score(y_w) - score(y_l))$ : Binary cross entropy loss  
          
- **GRPO**  
      
    - ↳ Reasoning fine-tuning.  
          
    - $\Rightarrow$ Can use **RLVR (RL w. verifiable rewards)** by PPO.  
          
    - (No additional value neural net)  
          
    - ↳ Sample $k$ response $y_1, \cdot\cdot\cdot, y_k \sim \Pi_\theta(\cdot|x)$  
          
    - $r_i = R(x, y_i)$  
          
    - ↳ Compute relative advantage  
          
  
# Parameter-efficient fine tuning (PEFT)  
  
- ↳ Fine tune LLM with a minimal parameter  
      
- **Methods**:  
      
    - ① Selective: Trainable layers  
          
    - ② Reparameterization (LoRA): Model updated.  
          
    - ③ Additive (Adapters, Prompt tuning): Prompt engineering (In-context)  
          
  
## LoRA (Low-Rank Adaptation)  
  
- Low-rank matrices  
      
- $W_{dec} = W + \Delta W$  
      
- $W_{enc}$  
      
- Structure: $x \rightarrow W \rightarrow h$, plus path $x \rightarrow A \rightarrow r \rightarrow B \rightarrow +$  
      
- **Example**:  
      
    - $W \in \mathbb{R}^{d \times k}$ where $d=512, k=64$  
          
    - LoRA with rank $r=8$  
          
    - $B = 512 \times 8$  
          
    - $A = 8 \times 64$  
          
- **Reduction**:  
      
    - $\frac{512 \times 8 + 8 \times 64}{512 \times 64} = \frac{1}{8}$  
          
    - : 87.5% reduction  
          
  
## Prompt tuning  
  
- ↳ 추가 Token을 주기 (매 Task 마다 X)  
      
  
# RAG (Retrieval-Augmented Generation)  
  
- Knowledge cut-offs  
      
- Hybrid approach in LLM  
      
- **Flow**:  
      
    - Prompt $\rightarrow$ Query Encoder $\rightarrow$ Vector Database (Retrieved Info) $\rightarrow$ [R | x] $\rightarrow$ LLM  
          
    - Non-parametric knowledge (R) + Parametric (LLM)  
          
- **Process**:  
      
    - **(1) Indexing**  
          
        - ① Document chunk size $C$.  
              
        - ② Embed & store each chunk to vector embedding. Size $V$.  
              
    - **(2) Retrieval**  
          
        - For every query ($h \rightarrow C \times V$)  
              
        - ① Embed query: $Q \rightarrow$ Vector  
              
        - ② Retrieve Context  
              
            - Use ANN to find closest vectors  
                  
            - $K$-chunks 가져옴.  
                  
        - $\{ C \times K, Q \} \rightarrow \text{LLM} \rightarrow \text{Final Answer}$  
              
        - [Original Chunks $\times K$] + [Original Query]  
              
  
# RAG vs Fine-tuning  
  
| **Feature**  | **RAG**            | **Fine-tuning** |  
| ------------ | ------------------ | --------------- |  
| Knowledge    | External knowledge | New skill       |  
| Cost         | Easy, Cheap        | Expensive       |  
| Transparency | Highly verifiable  | Opaque          |