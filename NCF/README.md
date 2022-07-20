# NCF(NeuralCollaborativeFiltering)
# 1. 배경 및 정의


<img width='700' src='..img/NCF/NCFlimit.png'>

- 위 그림 처럼 Matrix Factorization의 선형적인 한계를 지적한 모델입니다.
- 위 그림처럼 p1과 p2 사이의 관계를 거리로 나타낼 수 있습니다. 하지만,   
p1과 p2 관계를 좌표상에 나타낸 후 p3를 p1과 관계를 나타내게 되면 좌표상에 표시는 가능하지만
p3는 p2와의 관계를 표현하기가 어려워집니다. 이처럼 여러 vector간의 관계를 거리로 나타내게 되면 태생적으로 선형적으로 좌표공간에 나타내기가 애매해집니다.(low dimension)   
이를 보완한 모델이 NMF모델입니다.

- 신경망 기반의 Collaborative Filtering입니다.
- 1.MF의 선형적인 연산을 모사하고 신경망으로 보완한 GMF(Generalize Matrix Factorization)과 2.퍼셉트론을 사용하여 비선형성을 반영한 MLP(Multi Layer Perceptron)   
두 모델을 선형성과 비선형성을 모두 반영한 NCF(Neural Collaborative Filtering)을 제안하였습니다.
- 또한 GMF, MLP, NMF는 각각 독립적으로 학습 및 이용이 가능합니다.

# 2. Objection

<img width='700' src='..img/NCF/Projectionpredict.png'>

- M과 N은 User와 Item 수로 rating이 아니라 0과 1데이터로 표현한다.
- 논문은 0과 1을 선호, 비선호를 나타내는 분류가 아니라 interaction이 있는 지 implict한 예측이라고 표현한다.

<img width='700' src='..img/NCF/ObjectFunction.png'>

- 0과 1 확률 값을 예측하는 것이기 때문에 MLE 함수와 Min(loss) 함수 모두 사용 가능하다.

# 4. Mechanism

<img width='700' src='..img/NCF/GeneralFramework.png'>

- 위 그림처럼 기본적으로 User, Item을 각기 One-Hot vector로 만들어 input 한다.
- 이를 Dense Vector로 맵핑하고 User,Item의 interation을 학습하게 된다.

<img width='700' src='..img/NCF/Fusion.png'>

- GMF와 MLP를 합친 것이 NMF 이다.
- GMF는 P(uservector)와Q(itemvector)를 입력받으며 이를 내적한 vetor를 가지고 W을 곱하고 ActivationFunction 처리를 한 값을 output으로 받는다.
- MLP는 GMF와는 달리 P(uservector)와 Q(itemvector)를 concat(이어붙이기) 형태로 MLP 학습이 진행된다.

- 마지막으로 GMF와 MLP 연산한 것을 concat(이어붙이기)를 통해 0과 1 interation을 학습하게 된다.

# 5. 결론

- General Framework NCF 즉, GMF,MLP,NMF를 제안하였다.
- MF의 선형적인 한계를 NN로 해결하였다.
- 전반적으로 CF기반 Ranking 문제의 성능 향상에 기여하였다.
- raning 문제로 변형할 수 도 있으며 다양한 변형들이 존재한다.
- MF와는 다르지만 MF의 선형적인 특징을 모사한 GMF를 제안하였다. 가장 큰 차이점은 GMF는 P(Uservector),Q(ItmeVector) 자체를 학습하는 것이 아닌 W을 학습함으로 써 이를 대체하였으며 기존 MF의 K-Factor를 W의 크기를 조절하여 MF의 특징을 반영하도록 노력하였다. 또한, 마지막에 ActivationFunction 사용하여 어느정도 선형적인 한계를 보완하였다는 점에서 차이점이 있다.


# 6. 소스코드 두가지

- 1. NCF를 이용하여 rating을 예측하는 모델
- 2. NCF를 이용하여 interation을 예측하는 모델
- 두가지 코드를 모두 활용하여 NCF 공부하였습니다.

- 출처: https://github.com/LeeHyeJin91/Neural_CF
- 출처: **[딥러닝을 활용한 추천시스템 구현 올인원 패키지 Online](https://fastcampus.co.kr/data_online_rs)**