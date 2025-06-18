---  
tags:  
  - hci  
  - human-factor  
  - psychology  
  - cognition  
  - language  
  - entropy  
  - LLM  
share: "true"  
github_title: 2025-04-03-human-factor-sensor-and-responder  
title: 8. Human Factor - Brain  
date: 2025-04-03  
categories:  
  - Lecture Notes  
  - Human Computer Interaction  
---  
## Brain  
  
Most complex structure known  
  
Sensor와 responder를 연결해주는 역할을 한다.  
  
→ 이 역할을 잘 못하는 disabled 환자도 있어서, accessibility가 중요하다.  
  
---  
  
## Human Uniqueness  
  
사람은 그들이 상호작용하는 기계보다 훨씬 대단하다. (sensory input에 대한 association, meaning 부여)  
  
> People excel at `perception` , at `creativity` , at the `ability to go beyond the information given` , making sense of otherwise chaotic event. We do this efficiently and effortlessly.  
  
AI는 결국 파워가 엄청나게 드는데 우리는 김치찌개 하나로 엄청난 성능을 낸다.  
  
---  
  
## Perception (지각)  
  
First stage of processing for sensory input  
  
`Association` 이 형성된다.  
  
- Visual: 익숙하군, 이상하군  
- Tactile: 차갑군, 뜨겁군  
- Auditory: 조화롭군, 이상하군  
  
등등…  
  
### Psychophysics  
  
심물리학..?  
  
Human perception과 physical phenomena 사이의 관계 연구  
  
실험 방법론  
  
- 두 개의 자극을 따로따로 (또는 동시에) 준다.  
- 각 자극은 물리적으로 다른 특성을 갖는다. 진동수, 세기 등  
- 차이를 랜덤하게 조정한다  
- 차이가 어느정도여야 ‘같다고’ 느끼고 어느정도 이상이어야 ‘다르다’고 느끼는지 관찰한다.  
- Just noticeable difference (threshold)  
  
### Ambiguity  
  
각 physical 한 정보들이 오는데 이러한 정보들은 모호하다.  
  
어디가 앞면인지…이게 뭔지..  
  
### Illusion  
  
잘못 지각될 수 있다. 실제로는 긴데 짧게 지각된다든지.  
  
이러한 illusion은 비단 visual 자극에만 국한되지 않는다.  
  
Auditory한 stimuli에서도 가능하다. (ex. shepard scale)  
  
---  
  
## Cognition  
  
의식적인 지적활동이다. (지각은 의식없이도 지각할 수 있다는 것인가)  
  
- Thinking, reasoning, deciding  
  
Sensory phenomena (perception-related): easy to experiment because they exist in `physical world`  
  
Cognitive phenomena → They happen within the human brain. WTF?!  
  
### Making decision  
  
결정을 내리는 것을 측정하리란 매우 어렵다.  
  
언제 측정할지, 어떻게 측정할지 아무도 모른다.  
  
무슨 인풋이 들어가서 무슨 아웃픗으로 나오는지도 명확하지 않다.  
  
[Sensory stimulus] → [Cognition(decision making)] → motor response  
  
|Operation|Typical Time|비고 (B-GO)|  
|---|---|---|  
|Sensory Reception|1~38|아주 빠름|  
|Sensor to brain|2~100|편차 심해|  
|Cognitive Processing|70~300|제일 오래걸림 (Convolution layer인듯 ㄷㄷ)|  
|Brain to muscle|10~20|얘도 빠름|  
|Muscle latency|30~70|모터 작동 지연시간|  
|Total|113~528|사람마다 편차가 심하다. (ex. 페이커 vs 나)|  
  
---  
  
## Memory  
  
이거 아님  
  
- Vast Repository  
- Long-term memory  
    - Declarative Explicit Area → 외부 세계의 자극과 사건들에 대한 기억을 저장해 놓은 곳 (Data segment)  
    - Procedural Implicit Area → 어떻게 물체를 사용하는지, 어떻게 활동을 하는지 저장해놓은 곳 (Code Segment)  
    - 이거 완전…  
- Short-term memory  
    - Working memory (집중, 연습 중으로 기를 수 있음)  
    - 일종의 cache.  
    - 7 +- 2 의 unit정도를 한번에 기억할 수 있다. 여기는 정보가 휘발되고, 사라지면 cache miss나고…  
  
### Chunking  
  
Unit in short-term memory may be record as a chunk  
  
Expands capacity of short term memory  
  
KBS, MBC 등 Abbr.도 여기에 속함  
  
## Language  
  
The mental faculty allows humans to communicate  
  
Speech는 누구나 가능  
  
Writing은 상당한 노력을 기울여야 가능  
  
HCI는 writing 대체, text creation에 노력을 기울이고 있다.  
  
→ 근데 지금은? LLM의 발전속도를 HCI가 못따라감. 이거 완전 블루오션 아니냐.. 걍 LLM해보고 ‘해봤더니 잘됩니다’하면 연구 하나 뚝딱  
  
> Humankind is defined by `language` ; but civilization is defined by `writing`  
  
### Corpus  
  
One way to characterise written text.  
  
> 코퍼스(corpus)는 **언어의 표본을 모아 놓은 자료**를 뜻하는 말로, 말뭉치라고도 합니다. 언어학 분야에서 특정 주제에 맞춰 낱말들을 모아 놓은 '언어 자료'라는 의미를 지닙니다.  
  
corpus를 분석해보자.  
  
### Part-of-speech-tagging (corpus 분석)  
  
Some corpora include POS tagging  
  
각 단어는 카테고리로 태깅된다. (명사, 동사, 형용사 등)  
  
단어 예측에서 사용되는데, 검색 공간을 줄이는데 큰 도움이 된다.  
  
### Statistics and Language  
  
LLM의 완전 기본 원리  
  
1. 우리는 생략된 곳을 예측할 수 있다.  
    - Ham and ____ sandwich (cheese: 90%, egg: 83%, vehicle: 0.3%)  
2. 우리는 다음에 뭐가 올지도 예측할 수 있다.  
    - A picture is worth a thousand (won: 80%, dollar: 78%..)  
3. 글자도 예측할 수 있다.  
    - Questio__ (n: 99%, r: 10%…)  
4. 전체 문이나 구도 예측 가능  
    - 죽느냐 사느냐 그것이 _____  
  
안써도 안다는 것은 확률로 예측이 가능하다는 것이다.  
  
### Redundancy and Language  
  
사람들은 언어에 몇글자가 빠져도 이해할 수 있다.  
  
즉, 몇개 빼도 이해 가능하다.  
  
ppl lk t d hc rsrch whl thy njy sm …  
  
→ 글자양은 줄어도 정보량은 비슷. 섀넌은 자연어의 정보가 엄청 중복되었다고 말함.  
  
그 외에도 shortened tag를 이용해 줄이는 방식이 있다.  
  
gr8, th@ 등 sound바탕으로 줄이는 것도 있고  
  
w, gf, x 등 새롭게 발명된 acronym들도 있다.  
  
→ 그만큼 중복된 것들이 많다는 것이지~  
  
---  
  
## Entropy in Language  
  
Redundancy: What we know  
  
Entropy : What we don’t know  
  
- 엔트로피는 다음에 올 단어, 글자 등의 `불확실성` 이다.  
- Shannon은 letter-guessing experiment를 통해 redundancy와 entropy에 대해 설명했다.  
    - - - - - OOM I - - S  
    - 빈칸은 엔트로피가 낮다(예측 성공), 답이 틀려서 공개되면 엔트로피가 높다.  
  
**실험 결과**  
  
- 첫 글자에서 에러가 가장 높다  
- 단어가 진행되면서 에러율이 줄어든다.  
- 구문이 진행되면서 더더욱 줄어든다  
  
→ 원래 문장과 실험결과 문장은 ‘동일한 정보’를 담고 있다.  
  
→ 좋은 확률 모델로, 원 문장을 복구할 수 있다. (LLM 아니냐~)  
  
→ reduced text만 보내도 충분하다! (이 당시가 1950년대인데, 모스부호를 최대한 짧게 써서 에러율 줄이려고 한거다)  
  
섀넌은 어떻게 엔트로피를 계산하는지도 알려줬다.  
  
영어에서의 엔트로피는…  
  
H = 4.25 bits/letter  
  
→ 이전 단어들을 얼마나 참고하는지에 따라 점점 더 내려갔다.  
  
→ 100글자를 참고하면 H = 1bit/letter  
  
Redundancy = 75%.  
  
Note: 4.25는 어떻게 나왔는데  
  
1. 모든 글자의 빈도수를 체크한다.  
2. 확률을 계산한다.  
3. p*log(1/p + 1)의 값을 계산한다. (엔트로피)  
4. 모두 더한다.  
  
→ 정보를 나타내는데 필요한 최소 비트 수는 4.25이다.  
  
---  
  
## Human Brain.. All of them!  
  
performance, behavior, attention and error  
  
사람은 sensor, brain, and respond를 통해 그들의 목표를 향해 간다. 즉, 이 목표 수행능력을 평가해서 performance를 측정할 수 있다. (like IPC…)  
  
- Tying shoelace  
- Folding clothes…  
  
## Human Performance  
  
### Speed-accuracy Tradeoff  
  
- Fundamental property of Human Performance  
- 빠르게 수행하면, 에러율이 올라간다.  
- 천천히하면, 정확도가 올라간다.  
  
→ HCI의 새로운 인터페이스는 이 두 요소를 모두 고려해야한다.  
  
### Human Diversity  
  
사실 사람마다 너무 다르다.  
  
- Human differ  
- Environmental conditions affect performance  
- 보통 2가지 일을 동시에 해야하는 일이 생긴다.  
  
→ 그래서 보통 `distribution` 으로 나타내야 한다.  
  
### Reaction Time  
  
화학 그거 아님..  
  
- 가장 측정하기 쉬운 척도  
- 정의: 첫 고정된 자극의 발생 → 처음으로 응답하는 순간 (지정된 응답)  
  
ex) 빛이 나오면 버튼을 눌러요. : 빛 발생 시점 ~ 버튼이 처음 눌린 시점  
  
각 감각기관마다 반응 시간이 다다름  
  
- 청각이 제일 빠르고 (150ms)  
- 시각  
- 후각  
- 고통 순 (700ms)  
  
이는 matching experiment로 실험할 수 있는데~  
  
단어가 맞으면 J, 아니면 K를 누르게 하면 된다.  
  
실제로는 폰트를 다르게 해서 name만 맞으면 통과, class(구조)만 맞으면 통과로 했다.  
  
예상과 달리 name matching이 덜 걸렸다.  
  
Simple → name → physical (단순 글자) → class 순으로 빨랐다.  
  
그 외에도 visual search 실험이 있다.  
  
찾아야하는 것 개수가 늘어날수록 선형적으로 탐색 시간이 늘어나며, linear fitting이 가능하다.  
  
헉 O(N) search algorithm  
  
---  
  
## Skilled Behaviour  
  
다양한 작업에서, human performance는 연습하면 늘어남.  
  
얼마나 노력해야 성능이 올라가는지 연구하는 것에 중점을 둔다.  
  
Categories of skilled behavior  
  
- Sensory-motor (Dart, gaming…)  
- Mental skill (chess)  
- Task requires both (surgery…)  
  
---  
  
## Attention  
  
Attention is complex  
  
1. 두번째 작업으로 인해 분산될 수 있다.  
2. 어떤 작업은 집중을 요하고, 어떤 작업은 요하지 않는다.  
    1. 걸으면서 말할 수는 있어도  
    2. 글씨 쓰면서 말하기는 참 어렵다  
3. 어디까지 인간이 할 수 있는가. 애초에 집중이란 무엇인가.  
  
집중에는 2가지 카테고리가 있다.  
  
- Divided attention (attending to more than one task)  
- Selected attention (하나에게만 집중하고 나머지 요소는 배제하게되는 집중)  
  
---  
  
## Human Error  
  
사람이니까. 실수한다. 실수해도 괜찮아.  
  
에러는 우리는 보통 discrete level이라고 생각한다. (desire한 결과냐 아니냐, 그것 아닌가?)  
  
사실 연속적인 값이다. 애매하게 틀릴 수 있는 것이다.  
  
ex)  
  
quickly (정답) - quickyl (오답?) - qusisky (오답…?) - wdowdnnka (얜 뭐임 ㅋㅋ)  
  
### Accident  
  
대부분의 사고는 `human error` 로 부터 기인한다.  
  
하지만, 그 잘못은 design induced error에 있을지도 모른다.  
  
잘못된 버튼을 클릭하거나 잘못된 값을 입력하는 것은 가능한건 물론이고, 모든 디자인에서 있다고 가정되고 기대되야할 것이다. 이를 고려한 디자인이 필요하다.  
  
Note: False Affordance가 그 예이다.