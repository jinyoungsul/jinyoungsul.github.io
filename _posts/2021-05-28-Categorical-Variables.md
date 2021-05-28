---
title: Categorical variables
tags: 
  - python
  - datascience
  - pandas
categories: 
  - pandas
  - 
date: '2021-05-28'

---

# Categorical variables

범주형 변수는 제한된 수의 값만 사용한다.

- 아침 식사 빈도를 묻는 설문 조사에서 "안함", "거의 안함", "대부분", "매일"의 네 가지 옵션을 제공한다고 생각해봅시다. 이 경우 응답이 고정된 범주 집합에 속하기 때문에 데이터는 범주형입니다.
- 사람들이 자신이 소유한 자동차 브랜드에 대한 설문 조사에 응답한 경우 "기아", "현대, "쌍용"와 같은 범주로 분류됩니다. 이 경우 데이터도 범주형입니다.

이러한 범주형 변수를 먼저 사전 처리하지 않고 Python의 대부분의 머신러닝 모델에 연결하려고 하면 오류가 발생합니다.

범주형 변수를 전처리하는데 사용할 수 있는 세 가지 접근 방식을 비교해보겠습니다.

# 세 가지 접근법

### 1) 변수 제거
범주형 변수를 처리하는 가장 쉬운 방법은 단순히 데이터 세트에서 제거하는 것입니다. 이 방식은 열에 유용한 정보가 포함되지 않은 경우에만 잘 작동합니다.

### 2) 레이블 인코딩 Label Encoding
레이블 인코딩은 각 고유 값을 다른 정수로 할당하는 방식입니다.

![tut3_labelencode](https://i.imgur.com/tEogUAr.png)

이 접근 방식은 "Never"(0) < "Rarely"(1) < "Most days"(2) < "Every day"(3) 카테고리의 순서를 가정합니다. 이 가정은 카테고리에 명백한 순위가 있기 때문에 의미가 있습니다. 모든 범주형 변수가 값의 순서가 명확한 것은 아니지만 **ordinal variables**를 참조합니다. 트리 기반 모델의 경우 레이블 인코딩이 순서형 변수와 잘 작동 할 것으로 예상 할 수 있습니다.

### 3) 원-핫-인코딩 One-Hot Encoding 
원-핫 인코딩은 원본 데이터에서 가능한 각 값의 존재를 나타내는 새 열을 만듭니다.

![tut3_onehot](https://i.imgur.com/TW5m0aJ.png)

원래 데이터 세트에서 "Color"는 "Red", "Yellow", "Green"의 세 가지가 범주가 있는 변수입니다. 가능한 각 값에 대해 하나의 열과 원래 데이터 세트의 각 행에 대해 하나의 행이 포함됩니다. 원래 값이 "Red"이면 "Red"열에 1을 넣고, 원래 값이 "Yellow"이면 "Yellow"열에 1을 넣고, 원래 값이 "Green"이면 "Green"열에 1을 넣는 식입니다.

레이블 인코딩과 달리 원-핫 인코딩은 범주의 순서를 가정하지 않습니다. 따라서 범주형 데이터에 명확한 순서가 없는 경우 이 접근 방식이 잘 작동 할 것으로 기대할 수 있습니다. (예: "Red"는 "Yellow"보다 크거나 작지 않음). 내재 순위가 없는 범주형 변수를 **nominal variables**라고 합니다.
일반적으로 범주형 변수가 많은 수의 값을 사용하는 경우 원-핫 인코딩이 제대로 수행되지 않습니다. (일반적으로 15개 이상의 서로 다른 값을 갖는 변수에는 사용하지 않음)

# 예제
사용 데이터 세트
<a href="https://www.kaggle.com/dansbecker/melbourne-housing-snapshot/home" target="_blank"> [Melbourne Housing Snapshot | Kaggle] </a>

```python
import pandas as pd
from sklearn.model_selection import train_test_split

# Read the data
data = pd.read_csv('../input/melbourne-housing-snapshot/melb_data.csv')

# Separate target from predictors
y = data.Price
X = data.drop(['Price'], axis=1)

# Divide data into training and validation subsets
X_train_full, X_valid_full, y_train, y_valid = train_test_split(X, y, train_size=0.8, test_size=0.2,
                                                                random_state=0)

# Drop columns with missing values (simplest approach)
cols_with_missing = [col for col in X_train_full.columns if X_train_full[col].isnull().any()] 
X_train_full.drop(cols_with_missing, axis=1, inplace=True)
X_valid_full.drop(cols_with_missing, axis=1, inplace=True)

# "Cardinality" means the number of unique values in a column
# Select categorical columns with relatively low cardinality (convenient but arbitrary)
low_cardinality_cols = [cname for cname in X_train_full.columns if X_train_full[cname].nunique() < 10 and 
                        X_train_full[cname].dtype == "object"]

# Select numerical columns
numerical_cols = [cname for cname in X_train_full.columns if X_train_full[cname].dtype in ['int64', 'float64']]

# Keep selected columns only
my_cols = low_cardinality_cols + numerical_cols
X_train = X_train_full[my_cols].copy()
X_valid = X_valid_full[my_cols].copy()
```

```
X_train.head()
```

![X_train.head](https://i.imgur.com/g6V6rQe.png)

데이터 유형을 통해 범주형 변수 확인하기

```python
s = (X_train.dtypes == 'object')
object_cols = list(s[s].index)

print("Categorical variables:")
print(object_cols)
```
```
Categorical variables:
['Type', 'Method', 'Regionname']
```

### 각 접근 방식의 품질을 측정하는 함수 정의

범주형 변수를 처리하는 세 가지 다른 접근 방식을 비교하기 위해 함수를 정의합니다. 이 함수는 random forest model에서 [MAE](https://en.wikipedia.org/wiki/Mean_absolute_error)를 통해 측정하고 MAE값이 가능한 낮기를 원합니다.

```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

# Function for comparing different approaches
def score_dataset(X_train, X_valid, y_train, y_valid):
    model = RandomForestRegressor(n_estimators=100, random_state=0)
    model.fit(X_train, y_train)
    preds = model.predict(X_valid)
    return mean_absolute_error(y_valid, preds)
```
### 접근방식1 (범주형 변수 삭제)

```python
drop_X_train = X_train.select_dtypes(exclude=['object'])
drop_X_valid = X_valid.select_dtypes(exclude=['object'])

print("MAE from Approach 1 (Drop categorical variables):")
print(score_dataset(drop_X_train, drop_X_valid, y_train, y_valid))
```
```
MAE from Approach 1 (Drop categorical variables):
175703.48185157913
```

### 접근방식2 (레이블 인코딩)
Scikit_learn에는 레이블 인코딩을 가져 오는 데 사용할 수 있는 LabelEncoder 클래스가 있습니다. 범주형 변수를 반복하여 레이블 인코더를 각 열에 개별적으로 적용합니다. 

```python
from sklearn.preprocessing import LabelEncoder

# Make copy to avoid changing original data 
label_X_train = X_train.copy()
label_X_valid = X_valid.copy()

# Apply label encoder to each column with categorical data
label_encoder = LabelEncoder()
for col in object_cols:
    label_X_train[col] = label_encoder.fit_transform(X_train[col])
    label_X_valid[col] = label_encoder.transform(X_valid[col])

print("MAE from Approach 2 (Label Encoding):") 
print(score_dataset(label_X_train, label_X_valid, y_train, y_valid))
```
```
MAE from Approach 2 (Label Encoding):
165936.40548390493
```

위의 코드는 각 열에 대해 각 고유 값을 정수로 무작위로 할당합니다. 이것은 사용자가 지정 레이블을 제공하는 것보다 더 간단한 일반적인 접근 방식입니다. 그러나 모든 순서 형 변수에 대해 더 나은 레이블을 제공하면 성능이 추가로 향상 될 수 있는 가능성이 있습니다.

```python
# 예) map을 이용해서 사용자가 직접 레이블 인코딩
# 사용자가 원하는 레이블을 만들어 재할당 한다
X_train.Type = X_train.Type.map({'h':0, 'u':1, 't':2})
```

### 접근방식3 (원-핫 인코딩)
scikit-learn의 OneHotEncoder 클래스에서 여러 매개 변수를 사용하여 원-핫 인코딩을 얻습니다.
- valid 데이터에 train데이터에 표시되지 않은 클래스가 포함되어 있을 때 오류를 방지하기 위해 handle_unkown = 'ignore'를 설정합니다.
- sparse = False를 설정하면 인코딩된 열이 희소 행렬 대신 numpy 배열로 반환됩니다.

```python
from sklearn.preprocessing import OneHotEncoder

# Apply one-hot encoder to each column with categorical data
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

# One-hot encoding removed index; put it back
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

# Remove categorical columns (will replace with one-hot encoding)
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)

# Add one-hot encoded columns to numerical features
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

print("MAE from Approach 3 (One-Hot Encoding):") 
print(score_dataset(OH_X_train, OH_X_valid, y_train, y_valid))
```
```
MAE from Approach 3 (One-Hot Encoding):
166089.4893009678
```
<br>
또는, Pandas의 get_dummies() 메소드를 사용해서 원-핫 인코딩 데이터프레임을 얻을 수 있습니다.

```python
# 기존 데이터프레임과 합친 후 기존 범주형 변수 삭제해야 함
pd.get_dummies(X_train[object_cols])
```
![get_dummies](https://i.imgur.com/hy9eYMk.png)

# 베스트 접근 방식은?
범주형 변수를 삭제한 접근방식1이 최악의 결과를 얻었으며 접근방식2와 접근방식3은 점수의 가치가 너무 가깝기 때문에 서로간에 의미있는 이점이 없는 것으로 보입니다.

일반적으로 원-핫 인코딩이 최상의 성능을 발휘하고 범주형 변수 삭제가 최악의 성능을 보이지만 사례별로 다르기 때문에 각각의 접근방식을 비교해봐야 합니다.


