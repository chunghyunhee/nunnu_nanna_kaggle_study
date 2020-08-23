# Home Credit Default Risk


## 0. 대회개요 
소외된 사람들이 긍정적인 대출 경험을 갖도록하기 위해 Home Credit은 통신 및 거래 정보를 포함한 다양한 대체 데이터를 사용하여 고객의 상환 능력을 예측한다. 

## 1. datasets
- HomeCredit_columns_description
- POS_CASH_balance.csv
- application_test.csv
- application_train.csv
- bureau.csv
- bureau_balance.csv
- credit_card_balanace.csv
- installments_payments.csv
- prvious_application.csv
- sample_submission.csv

## 2. idea of the leaderboard notebooks
- category의 수에 따라 다른 encoding방법을 사용한 것이 인상적이었음. label encoding이나 one-hot encoding이외에도 다양한 인코딩 방법이 있는데 이에 따라 다양하게 융합하여 사용하는 방법을 생각해볼 필요가 있다고 생각함 + align 필수
- pair plot을 사용하면 단일 feature의 dist'n와 각 feature간의 관계까지 볼 수 있어 eda과정에서 많이 사용함 

## 3. other improvements
- 대부분 tabular데이터에서 많이 사용하는 NN + XGB + LGB를 앙상블 하여 사용하는 방법으로 모델링 하면 lb값이 훨씬 높지 않을까 싶음
- augmentation방법으로는 unsupervised learning(일단 GAN, autoencoder)후, supervised learning을 사용하는 방법을 시도해보고 싶음. 
- 마지막으로, 다양한 데이터가 given되어 있는데 이를 활용할 수 있는 방안들(왜 kernel에서는 하나만 썼는지..)
