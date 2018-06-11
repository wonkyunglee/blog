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
1. Latent Variable model
1. Markov Random Field
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
1. Hopfield Network
1. Conjugate Prior
1. Associative Memory
1. Dynamic Programming

이들을 모두 이 글에서 다루지는 못하지만 시간 나는대로 각각을 설명하는 글을 따로 써서 설명을 보충할 예정이다.


## 정리
이 논문은 DBN 을 설명했다기 보다는 DBN 을 빠르게 학습시킬 수 있는 알고리즘을 소개하는 논문이다.
Abstract 의 첫 문장에는 이렇게 쓰여있다.
> 우리는 *Complementary Priors* 를 사용해서 hiden layer 가 많은 densely connected belief nets 에서 추론을 힘들게 만드는 *Explaining away effect* 를 없앨 수 있는 방법을 설명한다.

세상에 이게 무슨말인가. 밑에서 하나하나 알아보도록 하자. 일단 초록을 조금 더 읽어보면, 다음과 같은 이야기가 나온다.
> Complementary Priors 를 사용하여, deep directed belief networks 를 한 층씩 학습할 수 있는 빠른 greedy algorithm 을 유도해냈다. 이 알고리즘은 weights 를 초기화하고...

딥러닝을 하면서도 항상 헷갈렸던 개념이, 레이어를 쌓는 행위를 probabilistic graphical model 을 만드는 것으로 볼 수 있는가 였다.  probabilistic graphical model 의 고수 힌튼 교수도 이런 고민을 했었는지 모르겠다. 이 논문에서는 많은 가정들과 개념들을 가져와서 어떤 조건 하에서는 이런 일이 가능하다고 우리에게 알려주고 있다.


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

일단 여기서 말하는 greedy algorithm 은 하나의 레이어를 먼저 학습 시킨 후 그 레이어를 고정시키고 그 다음 레이어를 학습시키고 를 계속 반복한다는 이야기이다. 전체 태스크의 최적 파라미터를 찾는 것이 아니라 태스크를 찾는 것이다.


## Restricted Boltzmann Machine
DBN 을 이루고 있는 RBM 을 먼저 알아보자. 위키피디아의 RBM에 대한 정의를 그대로 인용해보면 다음과 같다.
> A restricted Boltzmann machine (RBM) is a generative stochastic artificial neural network that can learn a probability distribution over its set of inputs.

번역해보면 RBM은 인풋의 집합에 대한 확률 분포를 학습할 수 있는 생성 확률적 신경망이라고 한다. (이건 또 무슨 말일까...)
통계 물리학에서 거시상태와 미시상태에 대한 설명을 할 때 등장한다고 하는데, 자세한 것은 알지 못하지만 짚고 넘어가야 할 개념이 있다.
에너지와 확률의 관계가 그것인데, 에너지 값이 낮을 수록 가능성 있는 상태가 된다는 것이다. 즉, 에너지가 낮을 수록 사건이 일어날 확률이 높다. 이는 섀넌의 정보이론에 등장하는 엔트로피의 개념과도 일맥상통하는 부분으로 언젠간 따로 다뤄볼 것이다.

여하튼, RBM 은 문자 그대로 Boltzmann Machine 의 제한(Restricted) 버젼이다. 볼쯔만 머신은 Visible layer와 hidden layer 두 층으로 이루어져 있는 확률 그래피컬 모델(PGM) 이다. 확률 그래피컬 모델은 자세히 공부하려면 매우 복잡하지만, 간단하게 확률 변수들의 의존 관계를 그래프 형식으로 나타내는 방법이라고 생각하면 된다.

RBM 은 볼쯔만 머신에 각 레이어의 유닛들이 서로 연결되지 않는다는 제한을 준 모델이다. 이런 그래프 모양을 Bipartite graph 라고 하긴 하는데 용어는 몰라도 상관없다. 다만 이렇게 하는 이유는 Gradient-based Contrastive Divergence 알고리즘으로 학습할 때 제한된 버젼이 아닌 버젼보다 연산량이 적어서 훨씬 학습이 더 잘 되기 때문이라고 한다. 이는 곧 이전 레이어에 대해 레이어 유닛 들이 conditionally independent 라는 뜻이고, 이 사실은 추후 확률 분포 유도에서 큰 역할을 한다. (이 내용은 RBM에 관련된 논문을 더 찾아봐야 확실하게 이해할 수 있을 것 같다...) 이 학습 방법은 뒤에서 설명하기로 하자.

여기까지 보면 RBM 이나 단층 오토인코더나 생김새로 보아 별반 다르지 않아보인다. 하지만 두 모델은 아주 큰 차이점이 있다. 오토인코더는 이전 층에서 다음 층으로 넘어갈 때의 노드 값이 결정되어 바뀌지 않지만 RBM 에서는 각 노드의 값이 특정 확률 분포에서 샘플링되어 결정되므로 확률적이다.

RBM 에서는 Visible unit 과 Hidden unit 들이 0과 1의 바이너리 값을 갖는다고 보통 정의한다. (물론 후에 나열할 수식들을 상황에 맞게 유도해서 다른 값들을 갖도록 정의할 수도 있다.) RBM 자체가 확률 그래피컬 모델이기 때문에 어떤 확률 분포를 모델링 해야 하는데, 특이하게도 확률분포 대신 에너지 함수를 정의한다. 그리고 이 에너지 함수로부터 visible 벡터와 hidden 벡터의 joint probability distribution 를 유도할 수 있으니 사실 확률 분포를 정의한거나 마찬가지이다. 그리고 이 결합확률분포를 hidden units 로 마지널라이즈하면 visible variable 즉 데이터 셋에대한 확률 분포를 만들 수 있다. 따라서 RBM 은 데이터셋에 대한 생성 모델(Generative model) 이라고 볼 수 있다.


## Contrastive Divergence
설명 링크 : http://www.robots.ox.ac.uk/~ojw/files/NotesOnCD.pdf


## Complementary Priors
설명 링크 : http://www.iro.umontreal.ca/~lisa/twiki/pub/Public/DeepLearningWorkshopNIPS2007/deep_learning_teh.pdf

http://web.science.mq.edu.au/~mjohnson/papers/Johnson12IntroRBMtalk.pdf


## Explaining Away Effect
설명 링크 : https://stats.stackexchange.com/questions/54849/why-does-explaining-away-make-intuitive-sense


##
