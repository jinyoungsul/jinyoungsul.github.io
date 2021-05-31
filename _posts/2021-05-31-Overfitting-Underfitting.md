---
title : 오버피팅 and 언더피팅

tags:
    - python
    - datascience
    - pandas
    - sklearn
categories:
    - pandas
    - sklearn
date: '2021-05-31'

---
# 오버피팅(Overfitting) and 언더피팅(Underfitting)

![Depth 2 Tree](http://i.imgur.com/R3ywQsR.png)

scikit-learn의 [문서](http://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html)에서 트리 기반의 모델에 많은 옵션이 있음을 알 수 있습니다. 가장 중요한 옵션은 트리의 깊이를 결정하는 것입니다. 트리의 깊이는 얼마나 많은 분할을 하는지에 대한 척도입니다. 위 그림은 비교적 얕은 트리입니다. 트리에 1개의 분할만 있는 경우 데이터를 2개의 그룹으로 나누며, 각 그룹이 분할되면 4그룹을 얻습니다. 각 레벨에서 더 많은 분할을 추가하여 그룹 수를 계속 2배로 늘리면 10레벨에 도달 할때는 1024개의 잎입니다. 매우 많은 잎은 모델이 훈련 데이터와 거의 완벽하게 일치하지만 유효성 검사 및 새 데이터에서는 제대로 작동하지 않는 **과적합**(overfitting)현상을 나타낼 수 있습니다.

반대로 극단적으로 나무를 2개 또는 4개로 나누어서 모델이 데이터에서 중요한 구별과 패턴을 잡아내지 못해서 훈련 데이터에서도 성능이 저하되는 경우 이를 **과소적합**(Underfitting)이라고 합니다.

![underfitting_overfitting](http://i.imgur.com/2q85n9s.png)

우리는 검증 데이터에서 추정하는 새 데이터의 정확성에 관심이 있으므로 과소적합과 과적합 사이의 최적점을 찾아햐 합니다. (빨간 곡선의 낮은 지점)

max_leaf_nodes 인수는 과적합과 과소적합을 제어하는 매우 합리적인 방법을 제공합니다. 모델이 만들 수 있는 잎이 많을수록 위 그래프에서 과소적합 영역에서 과적합 영역으로 더 많이 이동합니다.

# 예제
사용 데이터 세트 [[Melbourne Housing Snapshot | Kaggle]](https://www.kaggle.com/dansbecker/melbourne-housing-snapshot/home)

```python
from sklearn.metrics import mean_absolute_error
from sklearn.tree import DecisionTreeRegressor

def get_mae(max_leaf_nodes, train_X, val_X, train_y, val_y):
    model = DecisionTreeRegressor(max_leaf_nodes=max_leaf_nodes, random_state=0)
    model.fit(train_X, train_y)
    preds_val = model.predict(val_X)
    mae = mean_absolute_error(val_y, preds_val)
    return(mae)
```

```python
# Data Loading Code Runs At This Point
import pandas as pd
    
# Load data
melbourne_file_path = '../input/melbourne-housing-snapshot/melb_data.csv'
melbourne_data = pd.read_csv(melbourne_file_path) 
# Filter rows with missing values
filtered_melbourne_data = melbourne_data.dropna(axis=0)
# Choose target and features
y = filtered_melbourne_data.Price
melbourne_features = ['Rooms', 'Bathroom', 'Landsize', 'BuildingArea', 
                        'YearBuilt', 'Lattitude', 'Longtitude']
X = filtered_melbourne_data[melbourne_features]

from sklearn.model_selection import train_test_split

# split data into training and validation data, for both features and target
train_X, val_X, train_y, val_y = train_test_split(X, y,random_state = 0)
```

```python
# compare MAE with differing values of max_leaf_nodes
for max_leaf_nodes in [5, 50, 500, 5000]:
    my_mae = get_mae(max_leaf_nodes, train_X, val_X, train_y, val_y)
    print("Max leaf nodes: %d  \t\t Mean Absolute Error:  %d" %(max_leaf_nodes, my_mae))
```
```
Max leaf nodes: 5  		 Mean Absolute Error:  347380
Max leaf nodes: 50  		 Mean Absolute Error:  258171
Max leaf nodes: 500  		 Mean Absolute Error:  243495
Max leaf nodes: 5000  		 Mean Absolute Error:  254983
```
나열된 옵션 중 500이 최적의 잎 수이다.

# 결론
모델은 과소적합이나 과적합을 겪을 수 있습니다.  모델 학습에 사용되지 않는 검증 데이터를 사용하여 후보 모델의 정확도를 측정합니다. 이를 통해 많은 후보 모델을 시도하고 최상의 모델을 유지할 수 있습니다.
