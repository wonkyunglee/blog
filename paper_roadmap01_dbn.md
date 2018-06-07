# A Fast Learning Algorithm for Deep Belief Nets

## 저자
- Geoffrey E. Hinton, Simon Osindero, Yee-Whye

## 특징
1. 2006년, 최초로 Convolution 연산 없이 심층 구조 상에서 학습을 성공시켰다.
1. RBM 단위 블록을 여러번 쌓아서 깊은 신경망을 구성하는 딥 러닝 모델이다.
1. RBM 은 주어진 입력과 똑같은 출력을 생성하도록 하는 오토인코딩 과제를 수행하는 모델이다.
1. CNN 은 Deterministic Nodes 를 갖고, DBN 은 Stochastic Nodes 를 갖는다.
1. Related works 와 Background 가 없다.


## Backgrounds
이 논문은 딥러닝 마일스톤 논문임에도 불구하고, 요즘 나오는 논문들보다 훨씬 읽기가 어렵다.
Traditional 머신러닝에 대한 이해가 상당하지 않으면 한 줄도 편히 넘어갈 수 없기 때문이다.
내가 생각하는 필요한 선험지식은 다음과 같다. 카테고리의 상하 관계는 고려하지 않고 알아야하는 키워드만을 나열해보았다.
1. Supervised vs Unsupervised
1. Discriminative vs Generative
1. Bayes' Rule
1. Probabilistic Graphical Model
1. Maximum Likelihood
1. Variational Methods
1. Gibbs Sampling
1. Contrastive Divergence
1. Bayesian Estimator
1. Markov Chain
1. Markov Chain Monte Carlo
1. Stationary Distribution
1. Equilibrium Distribution
1. Complementary Prior
1. Explaining away effect
1. Gaussian Processes
1. Boltzmann Machine, Restricted Boltzmann Machine
1. Conjugate Prior
1. Associative Memory
1. Dynamic Programming

이들을 모두 이 글에서 다루지는 못하지만 시간 나는대로 각각을 설명하는 글을 따로 써서 설명을 보충할 예정이다.

## 정리
이 논문은 DBN 을 설명했다기 보다는 DBN 을 빠르게 학습시킬 수 있는 알고리즘을 소개하는 논문이다.
Abstract 의 첫 문장에는 이렇게 쓰여있다.
> 우리는 *Complementary Priors* 를 사용해서 hiden layer 가 많은 densely connected belief nets 에서 추론을 힘들게 만드는 *Explaining away effect* 를 없앨 수 있는 방법을 설명한다.

세상에 이게 무슨말인가. 밑에서 하나하나 알아보도록 하자. 일단 초록을 조금 더 읽어보면, 다음과 같은 이야기가 나온다.
> Complementary Priors 를 사용하여, deep, directed belief networks 를 한 층씩 학습할 수 있는 빠른 greedy algorithm 을 유도해냈다. 이 알고리즘은 weights 를 초기화하고...

딥러닝을 하면서도 항상 헷갈렸던 개념이, 레이어를 쌓는 행위를 probabilistic graphical model 을 만드는 것으로 볼 수 있는가 였다.  probabilistic graphical model 의 고수 힌튼 교수도 이런 고민을 했었는지 모르겠다. 이 논문에서는 많은 가정들과 개념들을 가져와서 이런 일이 가능하다고 우리에게 알려주고 있다.

## Structure
DBN 의 구조부터 살펴보자. 저자들은 DBN 의 상위 두 hidden layers 는 undirected associative memory 로, 나머지 hidden layers 는 directed acyclic graph 로 모델링하였다. 여기서 나머지 레이어들은 상위 두 레이어에서 얻은 representations 를 observable variables(pixel 같은 것들) 로 바꾸는 역할을 해준다.

이 문장을 이해하기 위해 먼저 Associative memory 를 간단히 알아보자. 말그대로 연관 검색을 할 수 있는 메모라는 뜻으로 이해하면 좋을 것 같다. 본래 컴퓨터에서 사용하는 대부분의 기억장치는 메모리의 주소를 입력하여 입려된 주소에 저장되어 있는 내용에 접근한다. 하지만 Associative memory 에서는 저장되어있는 내용으로부터 주소를 유추할 수 있기에 내용으로 검색을 할 수 있다. 아주 쉽게 예를 들면, Associative memory 를 사용하면 푸들과 시베리안허스키의 메모리 주소는 비슷하도록, 그리고 비행기나 자동차의 메모리 주소는 이에 비해 멀리 떨어져있도록 데이터를 저장한다. 아무래도 이 논문에서 상위 두 레이어를 Associative memory 라고 표현한 것은, 비슷한 데이터가 입력되면 그것들을 비슷한 표현 벡터 (representation) 으로 표현하기 때문이 아닌가 싶다.
> reference : http://www.aistudy.co.kr/neural/associative_memory.htm

나머지 hidden layers 는 단지 representation 으로부터 pixel 등의 variable 로의 단방향성 mapping 이라고 할 수 있을 것 같다.
이런 구조를 갖는 것의 장점을 introduction 에 나열해 놓았다.
1. greedy algorithm 을 적용해서 수 백만개의 딥 뉴럴 넷의 좋은 파라미터를 빠르게 찾을 수 있다.
1. 학습 알고리즘을 레이블과 데이터 모두를 생성하게 하여 지도학습과 비지도학습 모두에 적용할 수 있다.
1. generative model 을 완벽하게 배운 weights을 fine tuning 하여 discriminative task 결과도 기존보다 더 좋게 만들 수 있다.
1. generative model 이 생성하 representations 를 해석할 수 있다.
1. inference 가 빠르고 정확하다.
1. 학습 알고리즘이 지엽적이다(local).
1. neuron 끼리의 통신이 간단하다. 그들의 stochastic binary states 와만 통신하면 된다.


## Complementary Priors
설명 링크 : http://www.iro.umontreal.ca/~lisa/twiki/pub/Public/DeepLearningWorkshopNIPS2007/deep_learning_teh.pdf


## Explaining Away Effect
설명 링크: https://stats.stackexchange.com/questions/54849/why-does-explaining-away-make-intuitive-sense


## 
