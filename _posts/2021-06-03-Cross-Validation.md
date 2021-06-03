---
title : 교차검증 (Cross-Validation)

tags:
    - python
    - datascience
    - pandas
    - sklearn
categories:
    - pandas
    - sklearn
date: '2021-06-03'

---

# 소개
머신러닝은 반복적인 과정입니다.

우리는 사용할 예측 변수, 사용할 모델 유형, 해당 모델에 제공 할 파라미터 등에 대한 선택을 해야합니다. 지금까지 유효성 검사를 통해 모델 품질을 측정하여 데이터 중심 방식으로 이러한 선택을했습니다.

그러나 이런 접근방식은 몇가지 단점이 있습니다.
이를 확인하기 위해 5000개의 행이 있는 데이터가 있다고 가정합시다. 일반적으로 데이터의 약 20%를 유효성 검사 데이터로 유지합니다. 그러나 이것은 모델의 점수를 결정할 때 임의의 기회를 남깁니다. 즉, 모델이 다른 1000개 행에서 정확하지 않더라도 한 세트의 1000 개 행에서 잘 수행 될 수 있습니다.

일반적으로 검증 세트가 클수록 모델 품질 측정에 무작위성 ( "노이즈"라고도 함)이 적고 더 신뢰할 수 있습니다. 불행히도 우리는 훈련 데이터에서 행을 제거해야만 큰 유효성 검사 세트를 얻을 수 있으며, 훈련 데이터 세트가 작을수록 모델이 더 나빠집니다.

# Cross-Validation?
**교차검증(cross-validation)**은 여러 데이터 하위 집합에서 모델링 프로세스를 실행하여 여러 모델 품질 측정 값을 얻습니다.  예를 들어 데이터를 전체 데이터 세트의 각각 20 % 씩 5 개로 나눌 수 있습니다. 이 경우 데이터를 5 개의 "**folds(폴드)**"로 나눴다고합니다.

![tut5_crossval](https://i.imgur.com/9k60cVA.png)
 
 각 fold에 대해 하나의 실험을 실행합니다. 
- 실험 1에서는 첫 번째 fold를 유효성 검사 세트(또는 hold out)로 사용하고 나머지는 모두 학습 데이터로 사용합니다. 이를 통해 20 % hold out세트를 기반으로 모델 품질 측정 값을 얻을 수 있습니다. 
- 실험 2에서는 두 번째 fold를 hold out하고 나머지 fold를 모두 학습 데이터로 사용합니다. 그런 다음 두 번째 fold를 사용하여 모델 품질의 두 번째 추정치를 얻습니다.
- 모든 fold를 홀드 아웃 세트로 한 번씩 사용하여 이 프로세스를 반복합니다. 이를 종합하면 데이터의 100 %가 어느 시점에서 홀드 아웃으로 사용되며 데이터 세트의 모든 행을 기반으로하는 모델 품질 측정 값이됩니다. (모든 행을 동시에 사용하지 않더라도)

# 교차검증은 언제 사용해야 할까?

교차 검증은 모델 품질에 대해 정확한 측정을 제공하며 이는 많은 모델링 결정을 내릴 때 특히 중요합니다. 그러나 여러 모델(폴드마다 하나씩)을 추정하기 때문에 실행하는 데 더 오래 걸릴 수 있습니다.

다음의 상황일때 교차검증에 대한 사용을 고려해보자.
- 추가 계산 부담이 크지 않은 소규모 데이터 세트의 경우 교차검증을 사용.
- 더 큰 데이터 세트의 경우 단일 검증 세트로 충분. 코드가 더 빠르게 실행되고 홀드 아웃을 위해 일부를 재사용 할 필요가 거의없는 충분한 데이터일수 있다.

큰 데이터 세트와 작은 데이터 세트를 구분하는 것에 대한 단순한 임계 값은 없다. 그러나 모델을 실행하는 데 몇 분 미만이 소요되는 경우 교차 검증으로 전환하는 것이 좋다.

또한 교차 검증을 실행하고 각 실험의 점수가 비슷해 보이는지 확인하여 각 실험에서 동일한 결과가 나오면 단일 검증 세트로 충분합니다.

# 예제
사용 데이터 세트 [[Melbourne Housing Snapshot | Kaggle]](https://www.kaggle.com/dansbecker/melbourne-housing-snapshot/home)

```python
import pandas as pd
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import cross_val_score

# Read the data
data = pd.read_csv('../input/melbourne-housing-snapshot/melb_data.csv')

# Select subset of predictors
cols_to_use = ['Rooms', 'Distance', 'Landsize']
X = data[cols_to_use]

# Select target
y = data.Price

# RandomForest model
rf = RandomForestRegressor(n_estimators=50, random_state=0)

# Multiply by -1 since sklearn calculates *negative* MAE
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
scoring='neg_mean_absolute_error')

print("MAE scores:\n", scores)
```

```python
MAE scores:
 [346792.93730159 339070.53509097 323728.58272487 258306.48632984
 284431.25752138]
```

