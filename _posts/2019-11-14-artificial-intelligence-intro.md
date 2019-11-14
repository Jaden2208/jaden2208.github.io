---
layout: post
title: "0. Introduction to AI"
categories:
  - Artificial Intelligence
tags:
  - machine learning
  - representation learning
last_modified_at: 2019-11-14T
---
# 0. Introduction to AI

### 기계 학습
기계가 날것의 데이터에서 패턴을 추출하여 자신의 지식으로 습득하는 학습 방법.

### 표현 학습(Representation Learning)
- 딥러닝의 기초가 되는 것.
- 기계 학습 알고리즘의 성능은 주어진 데이터 의 표현에 크게 좌우된다.
- 표현 학습 예) 산모가 왔을 때 제왕절개를 해야하는지 여부를 판단하기 위한 AI 시스템을 만들기 위해서, 기계는 사람의 정보를 수치(numeric value)로 표현한다. 예를 들어 자궁에 상처가 있는 지 없는 지 등이 있다.
- 이때 ‘자궁 상태’를 “feature”라고 한다. (feature ← 반드시 기억해야 할 용어)
- logistic regression(로지스틱 회귀 분석)? 이런건 몰라도 된다. 이 알고리즘의 결과가 “feature” 이다.
- 이 feature과 제왕절개를 할지말지 사이에는 상관관계가 존재한다(correlate).
- logistic regression은 환자의 이러한 특징들이 다양한 결과와 어떻게 상호 연관되는 지를 배운다.
- 많은 AI task들이 이런 작업에 대해 올바른 특징 set을 뽑아내고 그걸(특징 set) AI에 적용한다.

#### 표현 학습의 목적 : 어떤 결정을 해야하는가에 대해서 올바른 특징을 뽑아내는 것.
- 하지만 많은 tasks들에 대해서, 어떤 특징을 추출해야 하는지를 알아내는 것은 어렵다.
- 이 문제에 대한 한가지 해결책은 기계 학습을 사용하여 표현에서 출력까지의 매핑뿐만 아니라 표현 그 자체까지도 발견하는 것이다.
- 이러한 접근을 표현 학습(representation learning)이라고 한다.
- 전통적인 머신러닝은 이런 한계가 있었지만 딥러닝을 통해 한계를 극복했다.
- 전형적인 머신러닝 알고리즘은 데이터(사진 등)를 통해 특징을 찾아낸다.
#### 표현학습에는 두가지가 있다.
- hand-designed representation 와 learned representation.
- 과거 전통적인 딥러닝 알고리즘과 최근의 딥러닝 알고리즘의 차이이다.
- Learned representations는 hand-designed representation에서 얻을 수 있는 것 보다 훨씬 더 좋은 결과를 가져오는 경우가 많다.
- Learned representations는 또한 AI 시스템이 최소한의 인간의 개입으로 new tasks에 빠르게 적응할 수 있도록 해준다.
- 표현 학습 알고리즘은 간단한 작업을 위한 좋은 특징 set을 몇 분 안에, 또는 복잡한 작업을 몇 시간에서 몇 달 안에 발견할 수 있다.
- 복잡한 작업을 위한 기능을 수동으로 설계하려면 많은 시간과 노력이 필요하다.

*good representation learning → good Model
representation learning의 역할 : 데이터로부터 특징을 찾는 것.*

#### 데이터를 어떻게 표현(representation)하는 지에 따라서 작업하는 방식이 달라진다.
- Cartesian coordinates(데카르트 좌표), Polar coordinate(극 좌표)
![thisisneverthat](/images/coordinates.png)


- 데이터 범주 사이에 한 직선을 그어서 두 범주를 분리한다고 할 때 Cartesian coordinates 에서는 그것이 불가능하다.

### 딥러닝

- 딥러닝은 다른 단순한 representation을 도입해 representation learning의 이러한 중심 문제를 해결한다.
- 딥러닝은 컴퓨터가 더 단순한 개념으로 복잡한 개념을 만들도록 한다.

<center> <img src="/images/deeplearning.png" width="50%" height="50%"></img> </center>

- 딥러닝은 복잡한 mapping을 여러 hidden layers로 쪼갠다.
- 왜 hidden 이냐고? 이러한 layers는 그 값이 데이터에 주어지지 않기 때문이다.
- 대신에 모델은 관찰된 데이터의 관계를 설명하기 위해 어떤 개념이 유용할지 결정해야 한다.
- 위의 이미지는 각각의 hidden unit으로 표현되는 특징의 종류의 시각화이다.
- edge → corners and contours → object : 가장 아래에서 점점 복잡한 것으로.

edge : 주어진 픽셀에서, 인접 픽셀들의 밝기를 비교해 edge를 구한다.
corners and contours : 주어진 edge를 가지고 corners와 확장된 contours(윤곽)을 구한다.
object : 구체적인 object에 대한 전체 parts를 감지한다.
마지막으로 이미지에 포함된 object 부분들에 대한 설명(description)을 이용해 이미지에 있는 object를 인식한다.

포함관계 : 딥러닝 < 표현학습 < 기계학습 < 인공지능
<center> <img src="/images/airelation.png" width="50%" height="50%"></img> </center>
- 기계학습은 복잡한 real-world 환경에 대해서 작동할 수 있는 AI 시스템을 구축하는 접근법이다.
- 딥러닝은 world를 표현하는 것을 학습함으로써 큰 힘과 유연성을 달성하는 특정한 종류의 기계 학습이다.

<center> <img src="/images/ai1.png" width="50%" height="50%"></img> </center>


*Rule-based systems : 전통적인 머신러닝 시스템(알고리즘)*
 *- 어떤 특징을 뽑겠다고 미리 정해놓고 뽑음.*

*딥러닝의 변화는?*
 *- 입력이 있을 때, 미리 정해 놓은게 아닌, 특징을 학습에 의해서 추출함(by learning).*

#### 딥러닝 시스템의 역사적 특징
- 딥러닝은 이용 가능한 훈련 데이터의 양이 증가함에 따라 더욱 유용해졌다.
- 딥러닝 모델은 딥러닝을 위한 컴퓨터 인프라(하드웨어와 소프트웨어 모두)가 개선되면서 시간이 지남에 따라 크기가 커졌다.
- 딥러닝은 시간이 지남에 따라 정확도가 높아지면서 점점 복잡해지는 응용 분야를 해결했다.

#### 딥러닝의 개발 트렌드
- 딥러닝은 성능을 높이는 방향으로 개발되어왔다.
- 어떤 시스템을 설계하면 그 시스템이 성능이 높아지는 걸로 끝인 방향으로.
- 처음에는 모델 아키텍쳐를 가지고 와서 모델을 만든다.
- 그 모델의 성능을 높이기 위해 learning을 한다.
- 그러면 성능이 잘 나온다. 왜 잘 나오는지는 모른다. 그래도 no problem으로 끝냈다.
- 즉, 설명이 안됐다.
- 그래서 한 2년 전부터 interpretable, 설명 가능한 모델을 만들자는게 트렌드로 나왔다.
- neural 신경망을 설명하는 것이 가능한 모델.

#### 증가하는 datasets
- 시간이 지남에 따라 데이터 사이즈가 늘어났다.
- ‘빅 데이터’ 시대는 통계적 추정의 핵심 부담이 덜어지면서 기계 학습을 훨씬 쉽게 해주었다.
 → 적은 양의 데이터를 관찰해 새로운 데이터로 잘 일반화할 수 있다.
머신러닝이란 건 훈련데이터로 쓰이지 않은 데이터에 대해서 성능이 잘 나와야 한다.
 *- Generalization(일반화)*

#### 모델 사이즈의 증가
- 처음에 인공 신경망에서 뉴런 당 connection 수는 하드웨어의 능력으로 인해 제한되었다.
- 어떤 인공신경망은 고양이 정도의 뉴런 당 connection 수를 가지고 있으며, 다른 신경망은 쥐 같은 작은 포유류 정도의 뉴런당 connection 수를 가지고 있다.
- hidden units가 도입된 이후 인공신경망은 2.4년 마다 대략 두배씩 크기가 증가했다.

#### 모델 사이즈 증가의 이유
- 더 빠른 GPU의 가용성.
- 네트워크 연결 속도 향상.
- 분산 컴퓨팅을 위한 더 나은 소프트웨어 인프라.

#### 증가하는 정확성과 복잡성
- ImageNet Large Scale Visual Recognition Challenge에서 경쟁하기 위해 필요한 만큼의 규모로 deep network가 도달했기 때문에.
- 그들은 매년 꾸준히 이 대회에서 우승했고, 매번 더 낮은 오차를 낳았다.
- 이러한 복잡성 증가 추세는 메모리 셀에서 읽고 메모리 셀에 임의의 내용을 쓰는 것을 배우는 Neural Turing Machines의 도입으로 논리적 결론에 도달했다.(pushed to its logical conclusion).
- 그러한 신경망은 원하는 행동의 예로부터 간단한 프로그램을 배울 수 있다.
- 이 자체 프로그래밍 기술(self-programming technology)은 초기 단계에 있지만, 미래에는 원칙적으로 거의 모든 작업에 적용될 수 있다.

<center> <img src="/images/ai2.png" width="50%" height="50%"></img> </center>

- 위에서 언급한 LSTM 시퀀스 모델과 같은 Recurrent Neural Networks(RNN : 반복 신경망)은 이제 단순히 고정된 입력보다는 시퀀스와 다른 시퀀스 간의 관계를 모델링하는 데 사용된다.
- 이러한 sequence-to-sequence 학습은 기계 번역의 또 다른 응용 분야에 혁신을 일으키고 있다.
- RNN에 대한 상세한 설명은 다음 강의에서….
- 딥러닝의 또 다른 가장 큰 성과는 강화 학습의 영역까지 확장한 것이다.
- 강화 학습의 맥락에서, 자율 대리인(autonomous agent)는 human operator의 어떠한 guidance 없이 시행착오에 의해 task를 수행하는 법을 배워야 한다.

### 강화 학습(Reinforcement Learning)
- 환경(environment)과의 상호작용을 바탕으로 성능을 향상시키는 시스템(agent)을 개발하는 것이 목표다.
- ground truth label을 사용하는 대신 reward function을 사용한다.
 → action이 얼마나 잘 이루어지는지 측정
- 환경과의 상호작용을 통해, 에이전트는 탐구적인 시행착오(trial-and-error)를 통해 reward를 극대화하는 일련의 행동들을 배울 수 있다.

<center> <img src="/images/ai3.png" width="50%" height="50%"></img> </center>

- “DeepMind는 딥러닝을 기반으로 한 강화 학습 시스템이 Atari video games를 배울 수 있다는 것을 증명하여, 많은 작업을 수행하는 것에 대해서 human-level 에 도달했다.”
- “딥러닝은 로봇 공학을 위한 강화 학습의 성과도 크게 향상시켰다.
- 강화 학습은 추후 강의에서 자세히 설명할 것이다….

#### Atari Games
> - Objective : 게임을 높은 점수로 완료하기.
> - State : 게임 state의 날것의 픽셀 입력
> - Action : 게임 컨트롤 e.g. Left, Right, Up, Down
> - Reward : 각 time step 마다의 점수 증/감.


- 이러한 딥 러닝의 많은 응용은 매우 수익성이 높다.
- 딥러닝은 현재 구글, 마이크로소프트, 페이스북, IBM, 바이두, 애플, 어도비, 넷플릭스, NVIDIA, NEC을 포함한 많은 최고의 기술 회사들이 사용하고 있다.
요약
- 딥러닝은 기계학습에 대한 접근법으로서, 인간의 뇌, 통계학, 응용수학에 대한 우리의 지식에 큰 영향을 끼쳤다.
- 최근 몇 년간, 딥러닝은 그것의 인기와 유용성에있어서 엄청난 성장을 해왔다.
 → GPU와 같은 더욱 강력한 컴퓨터
 → 더 큰 datasets
 → 더 깊은 네트워크를 train 하는 기술.
