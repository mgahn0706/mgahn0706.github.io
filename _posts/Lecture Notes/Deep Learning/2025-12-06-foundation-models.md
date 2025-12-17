---  
tags:  
  - foundation-model  
  - deep-learning  
  - LLM  
share: "true"  
github_title: 2025-12-06-foundation-models  
title: 16. Foundation Models  
date: 2025-12-06  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# Foundation Model  
  
- ↳ Trained on vast data (by self-supervised learning)  
      
- Adaptable to downstream task  
      
- **Ex) CLIP**  
      
    - Text encoder $\rightarrow$ [ ] $\leftarrow$ Image encoder  
          
- **Ex) OpenAI Whisper**  
      
    - : Speech to text  
          
    - Pretext: Contrast text image  
          
    - Downstream: Zero-shot classification tasks  
          
  
## Self-supervised Learning  
  
- ↳ Representation learning (unsupervised learning을 supervised 처럼)  
      
- **Structure**:  
      
    - Pretext task $\leftrightarrow$ Downstream task  
          
    - Predictor $\uparrow$ Predictor (fine-tune)  
          
    - Model $\uparrow$ Model  
          
    - Pre-training Data $\uparrow$ Task-specific Data  
          
- **Pretext tasks (Self-supervised learning tasks)**  
      
    - ① Self-prediction: "Intra-sample" prediction (pretends to be missing)  
          
    - ② Contrastive learning: "Inter-sample" prediction (관계?)  
          
  
# LLM History  
  
- GPT-1 $\rightarrow$ GPT-2 $\rightarrow$ GPT-3  
      
- BERT $\rightarrow$ XLNet  
      
  
## (1) BERT  
  
- ↳ Pre-train bidirectional representation  
      
- ↳ BERT can be fine-tuned with one layer  
      
- ↳ Denoising autoencoder for NLP.  
      
- **Training Process**:  
      
    - ① Unsupervised training  
          
        - Dataset $\rightarrow$ BERT $\rightarrow$ Masked word predict  
              
    - ② Supervised training with labeled dataset  
          
        - Dataset w. label $\rightarrow$ BERT $\rightarrow$ Classifier $\rightarrow$ Spam??  
              
  
### Defining a Prediction Goal  
  
- **Autoregressive model**:  
      
    - ↳ Predict next word  
          
- **BERT uses**:  
      
    - ① Masked language model  
          
    - ② Next sentence prediction  
          
  
### Masked LM  
  
- ↳ Noise 삽입 80% [mask]  
      
- 10% Random  
      
- 10% Original  
      
- Predict masked word based on non-masked words  
      
  
### NSP (Next Sentence Prediction)  
  
- ```  
    * Subsequent: 1  
    ```  
      
    - Random: 0 (X)  
          
- **Input pre-processing for NSP**:  
      
    - ① [CLS] token $\rightarrow$ 시작  
          
    - ② [SEP] token $\rightarrow$ 문장 구분  
          
    - Segment embedding  
          
    - Pos embedding  
          
  
## (2) GPT  
  
- ↳ Transformer-based; Unsupervised pre-training + Supervised fine-tuning  
      
- **Comparison**:  
      
    - **BERT**: Encoder only (Transformer)  
          
    - **GPT**: Decoder only (Transformer) + Masked self-attention  
          
- **Process**:  
      
    - Pre-training: Generative, Unsupervised  
          
    - $\downarrow$  
          
    - Fine-tuning: Discriminative, Supervised  
          
  
## (3) GPT-2  
  
- Scale up version  
      
- **In-context learning vs. Fine-tuning**  
      
    - $\downarrow$  
          
    - 추가 학습 X. Prompt only gradient 흘림.  
          
- **Zero-shot, One-shot, Few-shot.**  
      
  
## (4) XLNet  
  
- ↳ BERT 한계: Masked position 끼리의 dependency 무시  
      
    - Pretrain-finetune discrepancy.  
          
- **XLNet**: Generalized autoregressive method  
      
    - RNN + Transformer  
          
    - Considers all permutation.  
          
  
## (5) GPT-3  
  
- Scale-up... (Few-shot): No gradient update  
      
  
## (6) RoBERTa  
  
- ↳ BERT는 undertrained 되어있다.  
      
- XLNet 뛰어넘을 수 있다.  
      
- **Key changes**:  
      
    - Dynamic masking (Different mask for each epoch)  
          
    - No NSP pretraining  
          
  
## (7) BART  
  
- ↳ Denoising autoencoder (w. Transformer)  
      
- Encoder (BERT) $\leftrightarrow$ Decoder (Autoregressive)  
      
  
## (8) T5  
  
- ↳ Text-to-text format learning framework  
      
  
# Better LLM (Efficiency)  
  
- **Motive**: 명시적으로 안했는데 알아서 하는, emergent abilities.  
      
- LLM size를 줄여 training/inference Cost 줄여야함.  
      
  
## (1) DistilBERT  
  
- **Distillation loss**: $\mathcal{L}_{ce} = -\sum_{i}t_{i}\log(s_{i})$  
      
- **Cosine embedding loss**: $\mathcal{L}_{cos} = 1 - \cos(h_t, h_s)$  
      
    - Parameter-efficient.  
          
  
## (2) ALBERT  
  
- ↳ Parameter reduction  
      
- **① Factorized embedding parameterization (LoRA-like)**  
      
    - ex) $W = 5000 \times 4096 (\approx 20M)$  
          
    - $W = W_A \times W_B = (5000 \times 256) \times (256 \times 4096)$  
          
    - $\approx (1M + 0.6M)$  
          
- **② Cross-layer parameter sharing**: Set layer indep.  
      
- **③ SOP (Sentence Order Prediction)**  
      
    - ↳ NSP가 안좋았던 (RoBERTa) 이유는 MLM 보다 너무 쉬워서  
          
    - $\Rightarrow$ SOP 도입: (A, B)인지 (B, A)인지 맞추는 task  
          
  
## (3) ELECTRA  
  
- ↳ Discriminator (Encoder)  
      
- **New task**: Replaced token detection. (Sample efficient)  
      
    - Mask  
          
    - $\downarrow$  
          
    - MLM (Generator) $\rightarrow$ Synthetically generated  
          
    - $\downarrow$  
          
    - ELECTRA (Discriminator) $\rightarrow$ Real vs Fake?  
          
- **Benefit**: Training-efficient.