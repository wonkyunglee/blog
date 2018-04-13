# Universal Approximation Theorem
딥러닝을 공부하다보면 맨날 나오는 Universal Approximation Theorem 에 대해서 살짝 알아봅시다.  

## Linear vs Non linear model
입력 feature 로부터 출력으로의 매핑이 선형적(linear) 인 데이터와 비선형적(nonlinear)인 데이터가 있습니다.  
매핑이 선형적이라는 것은 매핑이 superposition 한 속성을 만족한다는 것입니다.
반대로 매핑이 비선형적 이라는 것은 매핑이 선형적이지 않은 모든 관계를 말합니다.

매핑이 만약 선형적이라면, objective function 이 convex 하게 되기 때문에 학습이 매우 쉽다는 장점이 있습니다.
하지만 우리가 모사하고싶은 관계는 보통 nonlinear 함수일 가능성이 높습니다.

## References
deeplearningbook 6.4.1




큰 흐름
1. 리니어 매핑은 convex라서 학습하기 쉽다.
2. 난리니어 매핑은 학습하기 쉽지 않다.
3. 대부분의 데이터는 난리니어 관계를 갖는다.
4. 1989년 Hornik et al 가 feedforward networks with hidden layers 는 universal approximation framework 를 제공한다고 증명했다. 특히 hidden layer 한층 + any squashing activation functionn 만 있으면 any Boral measurable function 을 desired nonzero amount of error 로 approximate 할 수 있다고 주장했다.  
5. 1990년 hornik et al 가 function 의 derivatives 또한 feedforward network 의 derivatives 로 approximate 할 수 있다고 증명했다.
6. 기존 이론에서는 양옆으로 saturation 되는 activation function 만 된다고 주장했었지만, 1993년 Leshno et al 이 relu 같은 wider class of activation function 을 써도 UAT 가 성립한다고 증명했다.
7. 결국 UAT 는 어떤 함수든 상관없이 MLP 로는 다 이 함수를 표현할 수 있다는 것. 하지만 그렇다고해서 training algorithm이 완벽하게 학습할 수 있다는 것이 보장되어있지는 않다. 두 가지 이유에서 학습이 불가능할 수 있는데, 첫째는 학습 알고리즘이 parameter 를 못 찾을 수 있다는 것이고, 둘쨰는 overfitting 때문에 틀린 함수를 찾을 수 있다는 것이다.
8. 한마디로 MLP가 universal function 을 모사할 수 있다는 말이지, 그런 최적의 파라미터들을 학습을 통해 찾을 수 있느냐는 다른 이야기라는 것. "There is no universal procedure for examining a training set of specific examples and choosing a function that will generalize to points not in the training set. - Ian Goodfellow"
9. UAT 에서, 충분히 네트워크가 크면 원하는 정확도를 얻을 수 있다고 하는데, 얼마나 커야 하는지에 대한 정보는 없다. 1993년 Barron 이 board class of function 을 approximate 하기 위한 바운드를 제공했다. worse case 에서는 exponential 수 만큼의 히든 유닛이 필요하다.   
10. 요약하자면, FN with single layer면 어떤 함수든 표현하기에 충분하다. 하지만 레이어가 엄청 담을수 없을만큼 커지거나 학습에 실패하고 generalize 되지 않을 수가 있다. 그런데, model 을 deep 하게 만드는 것이 함수를 표현하는데 필요한 유닛의 개수와 generalization error 를 줄일 수 있게 된다.    
11. depth 와 efficiency 에 관한 연구는 2013년 Pascanu et al 과 2014년 Montufar et al 에서 찾아볼 수 있다. deep rectifier net 으로 표현가능한 함수는 exponetial number of hidden units 을 갖는 shallow(one hidden ) network 로 표현가능하다고 한다. 더 정확히는, 피스와이스 리니어 네트워크는 depth 에 exponential 한 구역들을 표현할 수 있다. folding operation 을 조합해서 exponentially large number of piecewise linear regions 를 얻을 수 있다고 한다.
12. 딥 모델을 선호하는 두번째 이유는 statistical reason 이다. 우리가 머신러닝으로 어떤 함수를 모사하고 싶을 때 보통 우리의 선험적 지식을 활용하여 어떤 종류의 함수일 것이다 정도는 정해주고 들어가는 경우가 많은데, 딥러닝 모델을 사용한다는 것은 그런 점에서 매우 General 한 선택이다. 딥모델을 선택하는 것은 타겟 함수가 매우 간단한 몇몇 함수들의 조합으로 이루어져있다는 general belief 를 담고있는 것이다.
13. 이는 representation learning 의 관점에서, 학습 문제가 factors of variation 의 셋을 찾는것이고 그 변화의 팩터들은 또 다른 더 심플한 variation 의 팩터들로 설명될 수 있다는 것을 배우는 것이라고 설명할 수 있는 것이다.
14. 여튼 여러 연구에서의 경험으로 Wide variety of tasks 에서 더 깊을 수록 더 좋은 generalization 을 얻는 다는 것을 알 수 있었다고 한다.
   
