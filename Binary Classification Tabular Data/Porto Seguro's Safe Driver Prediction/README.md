# Porto Seguro's Safe Driver Prediction
## 0. 대회개요 
- 브라질 보험회사 중 하나인 Porto Seguro가 운전자에 대한 보험료 청구 예측을 정확히 하기 위한 대회이다. 
- 이 대회에서는 운전자가 내년에 자동차 보험 청구를 시작할 가능성을 예측하는 모델을 구축해야 한다. 

## 1. datasets 
- sample_submission.csv
- test.csv
- train.csv

## 2. idea of leaderboard notebook
- data preparation & exploration
    0. 다양한 type의 feature로 구성되어 있는 경우에는 meta dataset을 만들어서 data extraction & analysis가 용이하게 한다는 점
    1. meta data dataframe을 설정하여 기초 통계량 확인하고, feature engineering 방법 선택한 점. 
    2. imbalanced data에 대하여 smoothing방법을 적용한 점
    3. 다양한 시각화 방법들
    4. feature selection 방법 중 sklearn 내장함수 사용한 점

- Proto Seguro Exploratory Analysis and Prediction
    - 총 4개의 basemodel을 stack하여 ensemble모델을 구축함. 
    - 3개의 basemodel은 hyperparameter만 다른 LGBM 이고, 나머지 basemodel은 XGBoost이다. 
    - 각 가중치는 학습시켜 optimize함. 
    - 4개 basemodel 중 3개의 모델을 같은 모델을 사용하는 것이 인상적임. 
    - automl을 사용하여 hpo를 하는 것보다 stacking하는 것이 더 의미있는지 궁금함. 

## 3. other improvements
- unsupervised learning 방법을 사용하여 노이즈에 강한 모델을 만들었다는 점
- overall : 6개의 모델을 사용 (1개의 lgbm, 5개의 neural network model을 사용한다.)
- feature : calc variable은 삭제하며, cat variable에 대해서는 one-hot encoding 방식을 사용
- tabular data에 unsupervised learning + supervised learning을 사용했다는 점
- unsupervised learning방법으로는 DAE(denoising autoencoder)를 사용하여 feature을 재구성할 수 있는 방법을 생각함
- featuer을 재구성하되, noise를 추가한 feature을 만들어, data augmentation 효과를 부여한다
- 결국 노이즈 데이터에 의한 학습이 되므로 이후에 supervised learning을 할 때, 더 다양한 data representation이 가능하므로, 학습하는데 큰 역할을 한 것으로 보임
- 6개 모델의 구조는 아래와 같다 
![image](https://user-images.githubusercontent.com/49298791/90318962-0a932200-df6f-11ea-8ef0-f2119d14f3c2.png)
- 기본적으로 cv = 5를 사용하며, stratification 방법은 사용하지 않았다. local validation에 대해 bassing 방법과 그 개선점에 대해선 다시 생각해 볼 것. 
- nn model에 대해서는 반드시 normalization layer를 추가
- DAE(Denoising Autoencoder)는 나중에 supervised learning을 할 때 데이터를 잘 표현한다. 
- 이 과정에서 중요한 점은 "swap noise"라는 noise 스키마를 작성하는 것이다. 
- "inputSwapNoise"기능 자체에서 샘플링하여 지정한 percent만큼 노이즈를 만들 수 있다
- 마지막으로 bottleneck 문제는 입력데이터 차원을 1k..10k범위로 날리면서 해결이 가능
