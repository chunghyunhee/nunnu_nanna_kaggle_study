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

## 3. other improvements &  Discussion 
