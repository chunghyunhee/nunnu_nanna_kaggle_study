## [ 전처리 ]
1. PCA 사용 
- 2D-> 2D를 사용하고, 차원축소를 위해 사용하지 않음
- NYC를 rotate함으로써 축과 정렬시킨다. 
- tree base model을 사용할 때 분석의 효율성을 높인다. 

2. latitude, longitude로 위치가 주어져 있는 경우 
- harversine distance, manhatten distance를 사용하여 거리 계산

3. datetime으로 시간이 주어져 있는 경우 (YYYY-MM-DD-Time)
- month, weekofyear, weekday, hour로 데이터를 분리하여 데이터 각각 확인 

4. traffic data
- 60min을 기준으로 traffic을 계산하여 새로운 column을 생성

5. cluster
- 각 trip을 clustering하여 information을 합친다. 
- 60min마다 cluster가 몇개씩 들어가는지를 확인한다. 

### (Q1) 왜 clustering을 사용하는 이유?
- 여행의 중심좌표를 clustering하면 시계열 기반으로 한 평균 속도 및 중심 클러스터 수와 같은 유사한 집계 수를 만들 수가 있다. 

### (Q2) record 데이터의 사용 이유?

### (Q3) PCA에서 차원축소가 아니라 다른 용도로 사용하는 이유?
- 차원을 줄이지 않더라도 상관관계가 높은 데이터를 axis를 기준으로 회전하게 되면 각 데이터의 variance를 높일 수가 있으므로, 이를 기반으로 모델링에 사용할 경우엔 performance를 높일 수가 있다. 
- 데이터를 rotate하여 사용함으로써 tree 기반의 모델에 사용할 때 prunting시 효율성을 높이기 위함. 

## [ modeling ]
1. base XGBoost model 
2. simple 2-layer stacking models 
- 1st layer : 4개의 aggregated model에 XGB, a RandomForest, a ExtraTrees DecisionTree and a Linear Regression을 각각 적용하여 총 20개의 모델을 적용한다. 
- 2nd layer : finally apply XGB and tuned XGB 
