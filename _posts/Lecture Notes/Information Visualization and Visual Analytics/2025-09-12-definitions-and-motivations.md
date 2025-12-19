---  
tags:  
  - info-vis  
  - visualization  
share: "true"  
github_title: 2025-09-12-definitions-and-motivations  
title: 2. Definitions and Motivations  
date: 2025-09-12  
categories:  
  - Lecture Notes  
  - Information Visualization and Visual Analytics  
---  
## SciVis vs. InfoVis  
  
### SciVis  
  
- Spatial representations are given or have to be designed.  
  
## Big Picture  
  
- VIS is suitable when there is a need to `augment human capabilities`  
- Design visual representation to help people perform their `tasks` more effectively.  
- Design space is huge  
- Resource limitations  
- Three-part analysis framework  
  
## Why have Human in the loop?  
  
human in the loop: 인간의 상호작용이 필요한 모델  
  
Fully manual — (human in the loop) —→ Fully automated (e.g. transcripting)  
  
시각화는 사람들로 하여금 ‘그들이 뭘 물어봐야할지 모를 때’ 데이터를 분석할 수 있게 해준다.  
  
즉, 시각화는 아래와 같은 때 적절하다.  
  
- 결국 목적이 “사람들의 능력을 augment하는 것”일 때  
- 문제 자체가 ill-specified할 때 (어떻게 접근해야하는지 자체를 모를 때)  
  
### Transitional Use  
  
work itself out of a job  
  
- 순수히 computational한 작업을 만들 때까지 디자이너를 도와줌  
- computational solution이 자리잡고 나면, 시각화는 retire  
  
1. VIS tool in early stage of transition (highly exploratory)  
    - Gain a clearer understanding of user’s task and analysis requirements  
        - 유저의 태스크가 무엇인지 이해하기  
        - 계산 모델이나 알고리즘을 개발하기 전  
2. Vis tool in middle stage of transition  
    - For designers of a purely computational solutions  
    - e.g. tuning parameters of trading, tuning hyperparametes.  
    - 문제 해결이나 태스크 자체는 자동화되었고, 디자이너가 그것을 골라주기만 하면 됨  
3. VIS tool in late stages of transition  
    - help end-users make deployment decisions of whether the automatic system is doing the right thing.  
    - Dashboard can be abandoned after decision is made… or play with long-term use to monitor a pattern  
  
## Long-lasting use  
  
### Exploration Visualization tools  
  
- 많은 분석 문제들은 ill-specified 되어있다. 그들은 문제를 어떻게 접근해야하는지조차 모른다! (심지어 문제를 모를 때도 있다.)  
- 과학적인 분석을 도와줄 수 있다.  
- 그들이 가설을 만들고 검증할 수 있는 것을 도와준다. (대시보드도 이런 것 같다)  
  
### Presentation  
  
- 상사에게 보고하거나, 사람들에게 의미를 전달할때 도구로써 사용한다.  
- 이미 내가 알고있는 무언가를 설명할때 사용한다.  
- narrative가 중요하고 storytelling이 중요하다.  
  
→ 결국 내가 대시보드를 분류하고 분석했던 내용은 대시보드만의 특별한 특징이 아니라, 시각화이기에 갖는 특성들이었을 뿐이다.  
  
---  
  
## Then, why have a COMPUTER in a loop?  
  
사람이 다 하면 되는거 아님?  
  
- The scope of what people able to do is strongly limited by their `attention span`  
- Scalability & Generalizability. (하나의 task를 비슷하게 다른 작업에 대해 시각화하려면, 다시 처음부터 해야하는데 컴퓨터가 하면 그러지 않아도 된다.)  
- Dynamically changing datasets  
  
---  
  
### Working memory  
  
- Register set  
- Access in chunks  
    - Task dependent construct  
    - 7 +- 2 (by Mller), Chunk단위 working memory  
  
Working memory DECAYS  
  
- Content dependent (자극적일수록 오래감)  
- Limited attention span  
    - 5초 뒤에는 대부분 까먹음  
- Long-term memory에 commit하거나  
- paper note등 external tool에 기록해야함  
  
→ external memory를 통해, 우리의 cognition과 memory의 한계를 뛰어넘을 수 있음.  
  
Visualization for perceptual inference (사람들의 시각화를 통해 지각적 추론을 할 때..)  
  
- Organized information by spatial location (position이 channel 1위)  
- Recall << Recognition  
- Accelerating both search and recognition by grouping items.  
  
---  
  
## Why depend on VISION  
  
why not sonification or tastification (…) ?  
  
1. Very high bandwidth channel to brain  
2. Preattentive processing (popout)  
  
## Why use Interactivity  
  
- We cannot show all at once for a LARGE dataset.  
- Interactivity for handling complexity and volume  
  
## Why Design Space is Huge?  
  
### Visualization Idioms (=Charts)  
  
- Direct approach to creating and manipulating visual representations  
- Framework for thinking about the space of vis design idioms systemically  
- There are soooo many ways to create a visual encoding of data  
- Also, we can `link together` multiple charts through interaction. → More design choices  
  
## Why Focus on Tasks?  
  
- 하나의 task에 잘 동작하는 도구는 다른 태스크에 대해서는 안 좋을 수 있다. (dataset이 같더라도)  
- Reframing the users’ task from domain-specific → abstract form  
    - e.g. 두 그룹간 비교  
    - task abstraction을 통해 비슷하지만 서로 다른 두 도메인에 적용 가능  
- VIS Analysis framework provides generic words to describe WHY  
  
## Why Focus on Effectiveness?  
  
효과적인 시각화란 뭘까.  
  
→ 시각화에 담긴 정보가 더 손쉽게 눈에 인지될 때.  
  
결국, 시각화는 사용자의 task를 도와주기 위함이다. → effectiveness  
  
- Correctness, accuracy, and truth  
  
예쁜 것만을 만드는게 우선순위가 아니라는 뜻이다.  
  
---  
  
### Most design is ineffective…due to huge design space  
  
Not to optimize…but consider multiple alternatives in parallel  
  
---  
  
## Why Validation difficult?  
  
- So many questions that you could ask!  
- better, faster, insightful, engagement…. (HCI things)  
  
---  
  
## Why Are There Resource Limitations?  
  
1. Computational capacity  
2. Human perceptual and cognitive capacity (working memory)  
3. Display capacity (screenspace)