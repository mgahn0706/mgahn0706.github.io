---  
tags:  
  - deep-learning  
  - loss-function  
  - machine-learning  
  - generalization  
share: "true"  
github_title: 2025-09-13-introduction  
title: 1. Introduction  
date: 2025-09-13  
categories:  
  - Lecture Notes  
  - Deep Learning  
---  
# I. intro.  
  
### **AI Venn Diagram**  
  
- **AI**: Create a machine that can think like humans.  
      
    - (Contains) **Machine learning**  
          
        - (Contains) **Representation learning**  
              
            - (Contains) **Deep learning**  
                  
  
---  
  
### **Comparison**  
  
**(1) Rule-based systems**  
  
- Input $\rightarrow$ **Hand-designed program** $\rightarrow$ Output  
      
  
**(2) Classic machine learning**  
  
- Input $\rightarrow$ **Hand-designed features** $\rightarrow$ Mapping $\rightarrow$ Output  
      
    - _human selects feature_  
          
  
**(3) Representation learning**  
  
- Input $\rightarrow$ **Features** $\rightarrow$ Mapping $\rightarrow$ Output  
      
    - _: able to learn from data_  
          
    - $Input \rightarrow Features \rightarrow Mapping \rightarrow Output$  
          
  
**(3.1) Deep learning**  
  
- Input $\rightarrow$ **Simple features** $\rightarrow$ additional layers of more **abstract features** $\rightarrow$ Mapping $\rightarrow$ Output  
      
    - $\hookrightarrow$ end-to-end 자동화  
          
  
---  
  
### **Three waves**  
  
**(1) Cybernetics**  
  
- **Perceptron**: $g(x) = Sign(\sum_{i=1}^{d} w_{i}x_{i} + b)$  
      
- **$\delta$-rule**: $w \leftarrow w + \eta \cdot \epsilon \cdot x$  
      
    - 오차계산 후 $\epsilon$에 따라 반영. (Reflect based on $\epsilon$ after calculating error)  
          
- **Stochastic gradient descent**  
      
    - : mini-batch 만보고 경사하강. (Gradient descent looking only at mini-batch)  
          
    - Randomly descent  
          
  
**(2) Connectionism**  
  
- Neural nets: hierarchical MLP  
      
- Distributed representation  
      
- Back propagation  
      
    - not one hot encoding (e.g., apple = [0.85, 0.2, ...])  
          
    - Can be generalized  
          
    - : algorithm for MLP $\delta$-rule. (chain rule)  
          
  
**(3) Status quo**  
  
- Minimize loss function.  
      
    1. **Subhuman**: general intelligence  
          
    2. **Human-level**: perception tasks  
          
    3. **Superhuman**: domains with structured big data  
          
  
---  
  
# I. Review  
  
- **Machine learning**  
      
- Learning from data.  
      
  
### **[Flowchart Transcription]**  
  
1. **Unknown target distribution**: $P(y|x)$ (annotated: 정답)  
      
2. **Unknown input distribution**: $P(x)$ (annotated: input)  
      
    - $\downarrow$ generates $x_1, ..., x_N$  
          
3. **Training examples**: $(x_1, y_1) \dots (x_N, y_N)$  
      
    - $\downarrow$  
          
4. **Learning algorithm $\mathcal{A}$**  
      
    - $\uparrow$ takes input from **Hypothesis set $\mathcal{H}$**  
          
    - $\rightarrow$ outputs  
          
5. **Final hypothesis $g$**: $g(x) \approx f(x)$  
      
  
---  
  
### **Tasks in ML**  
  
- Described in terms of how to process an example  
      
- Collection of features: $x \in \mathbb{R}^n$  
      
    - $x_i$: a feature  
          
  
### **Performance measure**  
  
- Task dependent  
      
    - **Classification**: error rate $E$  
          
- Evaluated using datasets  
      
    - **Training**: $E_{train}$  
          
    - **Density estimation**: avg. log-probability the model assigns to examples  
          
        - likelihood가 높을 수록 좋은데, (Higher likelihood is better,)  
              
        - $L(\theta) = \prod_{i=1}^{N} p_{\theta}(x^{(i)})$  
              
        - $\sum \log L(\theta)$  
              
    - **Dev**: $E_{dev}$  
          
    - **Test**: $E_{test}$  
          
  
**Challenges**  
  
1. Frequent? Large?  
      
2. What to measure?  
      
3. Measurement is hard  
      
  
### **Data sets**  
  
- **Test**: $E_{test} \approx E_{gen} = E_{out}$ (for generalization)  
      
- **Val**: $E_{val}$ ($E_{dev}$) (for model selection or hyperparameter tuning)  
      
- **Train**: $E_{train}$ (for model fitting)  
      
  
**e.g., k-fold cross validation**  
  
- Diagram: [Splits data into k parts]  
      
- assume: 3개의 data 분포가 동일 (assume: 3 data distributions are identical)  
      
- k번 계산량 늘지만, 나누는 것의 penalty 줄고 더 많은 양이 train 된다. (Calculation increases k times, but penalty of splitting decreases and more amount is trained.)  
      
  
---  
  
# 1. Theory of Generalization  
  
### **Capacity of model**  
  
- $C =$ model fit various functions  
      
- **Underfitting**: Capacity $\downarrow$  
      
- **Overfitting**: Capacity $\uparrow$  
      
- Appropriate  
      
  
### **Choosing a model**  
  
- $\hookrightarrow$ **Parsimony**, choose Simplest one!  
      
  
### **VC generalization bound**  
  
- For any $\epsilon > 0$, $N > 0$  
      
- $|P[|E_{train}(g) - E_{test}(g)| > \epsilon] \le (2N)^{d_{VC}} \cdot e^{-\frac{1}{8}\epsilon^{2}N}$  
      
    - $\hookrightarrow$ bad event 확률 (probability of bad event)  
          
  
### **Central Challenge**  
  
- $E_{gen} \approx 0$  
      
    - $\downarrow$ (VC bound)  
          
- $E_{test} \approx 0$  
      
    - $\downarrow$  
          
- **Underfitting vs Overfitting**  
      
  
**Analysis of Error**  
  
1. **Generalization gap**: $E_{test} \approx E_{train}$  
      
    - gap이 얼마나 적은가 (How small is the gap)  
          
    - If not: **Overfitting** (due to variance)  
          
    - $\rightarrow$ Regularization, less complex model, more data  
          
2. **Approximation ($E_{train}$)**  
      
    - 모델이 충분히 복잡해야한다. (Model must be sufficiently complex.)  
          
    - If not: **Underfitting** (due to bias)  
          
    - $\rightarrow$ Better optimization, more complex model  
          
  
**Augmented Error**  
  
- $E_{aug}(\theta) = E_{train}(\theta) + \lambda \cdot \Omega(\theta)$  
      
    - $\Omega(\theta)$: Regularizer  
          
  
---  
  
### **Choosing a Model (Continued)**  
  
- Complex model + big data + effective regularizer  
      
- $\Rightarrow$ Hinges on **double descent phenomena**  
      
  
**[Graph: Model Complexity vs Error]**  
  
- $E_{test}$ (U-shaped curve) - annotated "modeled noise"  
      
- $E_{train}$ (Decreasing curve) - annotated "unmodeled data"  
      
- X-axis: Model Complexity ($\lambda^{-1}$)  
      
  
### **Linear models**  
  
**Advantages**  
  
1. **Simplicity**  
      
2. **Generalization**: $E_{out} \approx E_{train}$  
      
3. **Extension**: Can solve classification, regression, probability estimation  
      
  
**Formalize binary classification**  
  
- $\mathcal{X} = \mathbb{R}^d$ ($x \in \mathcal{X}: x = (x_1, x_2, \dots, x_d)$ input)  
      
- $\mathcal{Y} = \{+1, -1\}$ output space  
      
- Note: $f: \mathcal{X} \rightarrow \mathcal{Y}$ ideal approval formula (target function)  
      
- $g: \mathcal{X} \rightarrow \mathcal{Y}$: hypothesis  
      
  
**Decision making**  
  
- $\sum_{i=1}^{d} w_i x_i > threshold$ (approve)  
      
    - (Weighted coordinate)  
          
  
---  
  
### **Perceptron (compact ver.)**  
  
- $g(x) = Sign[(\sum_{i=1}^{d} w_i x_i) - threshold]$  
      
    - $= Sign((\sum_{i=1}^{d} w_i x_i) + b)$  
          
    - $= Sign(w^T x + b)$  
          
- where $b$ is called "bias"  
      
- Parameters $\theta := (w_1, w_2, \dots, w_d, b)$  
      
    - $\hookrightarrow$ yield different hyperplanes  
          
  
### **Optimization**  
  
- $\nabla E_{train}(w) = 0$  
      
  
### **Loss functions**  
  
1. **0-1 Loss**: 다르면 1 (1 if different)  
      
2. **BCE (Binary Cross Entropy)**  
      
    - y: label (정답)  
          
    - $\hat{y}$: model output  
          
    - def: $-y \log \hat{y} - (1-y) \log (1-\hat{y})$  
          
3. **Logistic**: $\log(1 + e^{-y\hat{y}})$  
      
  
**Optimization Example (Linear Regression / Least Squares)**  
  
- Problem: $\min ||y - (w^T x)||^2$  
      
- Logistic regression uses Sigmoid: $G(z) = \frac{1}{1+e^{-z}}$  
      
- Solving $\nabla E_{train}(w) = 0$:  
      
    - $J(w) = \sum_{i=1}^{d} (y_i - w_i x_i)^2$  
          
    - $\frac{dJ}{dw} = \sum_{i=1}^{d} 2(y_i - w_i x_i) \cdot (-x_i)$  
          
    - $= -2 \sum_{i=1}^{d} (x_i y_i - w_i x_i^2) = 0$  
          
    - $\therefore w_i = \frac{\sum x_i y_i}{\sum x_i^2}$  
          
  
---  
  
### **Why BCE?**  
  
- $H(p, q) = -\sum p_i \log q_i$ (= Cross Entropy)  
      
    - $C=\dots$ 예측했을때 P 설명하는 비용 (Cost of explaining P when predicting...)  
          
- If $y \in \{0, 1\}$:  
      
    - $p \in [y, 1-y]$  
          
    - $q \in [\hat{y}, 1-\hat{y}]$  
          
- $H(p, q) = -y \log \hat{y} - (1-y) \log(1-\hat{y})$  
      
  
**Loss for multiclass**  
  
- Model $\rightarrow$ Softmax $\rightarrow$ Cross Entropy Loss  
      
- $J_{CE}(y, \hat{y}) \triangleq -\sum_{i=1}^{k} y_i \log \hat{y}_i = -y_{answer} \cdot \log \hat{y}_{answer}$  
      
  
### **Activation functions**  
  
- **ReLU**  
      
- **Leaky ReLU**  
      
- **GELU**  
      
  
---  
  
# Elements of neural nets  
  
### **Basic Unit**  
  
- $X \rightarrow$ **Weighted Sum** (Linear) $\rightarrow$ **Activation Function** (Possibly non-linear) $\rightarrow$ Output  
      
    - (Feedback loop marked as "feed back")  
          
- **MLP**: $w^T X + b$  
      
- **CNN**: $w * X$  
      
  
### **Encoder, Decoder**  
  
- $x$ $\rightarrow$ **Encoder** (input summarizer) $\rightarrow$ $h$ (efficient repre) $\rightarrow$ **Decoder** (output generator) $\rightarrow$ $y$