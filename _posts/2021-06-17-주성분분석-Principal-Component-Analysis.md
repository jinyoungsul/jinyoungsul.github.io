---
title: 주성분 분석 - PCA
tags: 
  - python
  - datascience
  - pandas
  - sklearn
categories: 
  - sklearn
date: '2021-06-17'

---

# 주성분 분석 (PCA)

PCA는 데이터에서 중요한 관계를 발견하는데 도움이되는 훌륭한 도구이며 더 많은 특성을 만드는데 사용할 수도 있습니다.

> PCA는 일반적으로 표준화 된 데이터에 적용합니다.

[*Abalone*](https://www.kaggle.com/rodolfomendes/abalone-dataset) 데이터 세트에는 수천개의 Tasmanian 전복에서 측정한 물리적인 특성이 있습니다.  (전복은 조개나 굴과 매우 흡사 한 바다 생물입니다.) 지금은 껍질의 `'높이'` 와 `'직경'` 의 몇 가지 특징을 살펴 보겠습니다.

이 데이터 안에 전복이 서로 다른 경향을 나타내는 '변이 축'이 있다고 상상할 수 있습니다.  그림에서 이러한 축은 데이터의 자연적인 치수를 따라 이어지는 수직선으로 나타나며 각 원본 특성에 대해 하나의 축이 있습니다.

![Image](https://i.imgur.com/rr8NCDy.png)

종종 이러한 변형 축에 이름을 부여 할 수 있습니다. 더 긴 축은 `'크기'` , 짧은 축은 `'모양'` 구성 요소라고 할 수 있습니다.  작은 높이와 작은 지름 (왼쪽 아래)은 큰 높이와 큰 지름(오른쪽 위)과 대조됩니다. 작은 높이와 큰 지름 => (평평한 모양)이 큰 높이와 작은 지름 => (둥근 모양)과 대조됩니다.

전복을 `'높이'`와 `'직경'`으로 설명하는 대신 `'크기'` 와 `'모양'` 으로 설명 할 수 있습니다. 사실 이것이 PCA의 전체 개념입니다. 원래 특성으로 데이터를 설명하는 대신 변형 축으로 데이터를 설명하고, 변형의 축이 새로운 특성이 됩니다.

![Image](https://i.imgur.com/XQlRD1q.png)

>주요 구성 요소는 특성 공간에서 데이터 세트의 회전에 의해 새로운 특성이 됩니다.

새로운 특성 PCA 구성은 실제로 원래 특성의 선형 조합(가중 합계)입니다. 

```
df["Size"] = 0.707 * X["Height"] + 0.707 * X["Diameter"]
df["Shape"] = 0.707 * X["Height"] - 0.707 * X["Diameter"]
```
이러한 새로운 특성을 데이터의 주요 구성 요소(principan components)라고합니다. 또한 가중치 자체를 `'로딩'`이라고합니다.

# PCA for Feature Engineering

Feature Engineering에 PCA를 사용할 수 있는 방법은 두 가지입니다. 

첫 번째 방법은 서술적 기법을 사용하는 것입니다. 구성요소가 변동에 대해 알려주기 때문에, 구성요소에 대한 MI 점수를 계산하고 어떤 종류의 변동이 목표를 가장 잘 예측하는지 확인할 수 있습니다. 이를 통해 생성 할 특성의 종류에 대한 아이디어를 얻을 수 있습니다. 예를 들어, `'크기'`가 중요한 경우 `'높이'`와 `'직경'`의 곱, `'모양'`이 중요한 경우 `'높이'`와 '`직경'`의 비율입니다. 점수가 높은 구성 요소 중 하나 이상에서 클러스터링을 시도 할 수도 있습니다. 

두 번째 방법은 구성 요소 자체를 특성으로 사용하는 것입니다. 구성 요소는 데이터의 변형 구조를 직접 노출하기 때문에 원래 특성보다 더 많은 정보를 제공 할 수 있습니다. 다음은 몇 가지 사용 사례입니다.

- 차원 축소 (Dimensionality reduction): 특성이 고도로 중복 된 경우 (특히 다중 공선성) PCA는 중복성을 하나 이상의 0에 가까운 분산 구성 요소로 분할합니다. 그러면 정보가 거의 또는 전혀 포함되지 않으므로 삭제 할 수 있습니다.
- 이상 탐지 (Anomaly detection): 원래 특성에서 분명하지 않은 비정상적인 변동은 종종 낮은 분산 구성 요소에 나타납니다. 이러한 구성 요소는 이상 또는 이상값 탐지 작업에서 매우 유용 할 수 있습니다.
- 노이즈 감소 (Noise reduction) : 센서 판독 값의 모음은 종종 공통적인 배경 노이즈를 공유합니다. PCA는 때때로 유익한 신호를 더 적은 수의 기능으로 수집하고 노이즈는 그대로 두어 신호 대 노이즈 비율을 높일 수 있습니다.
- 역 상관 (Decorrelation) : 일부 ML 알고리즘은 상관 관계가 높은 특성으로 어려움을 겪습니다. PCA는 상관 관계가 있는 특성을 상관 관계가 없는 구성 요소로 변환하므로 알고리즘이 더 쉽게 작동 할 수 있습니다.


<blockquote style="margin-right:auto; margin-left:auto; background-color: #ebf9ff; padding: 1em; margin:24px;">
<strong>PCA Best Practices</strong><br>
다음은 PCA를 적용 할 때 염두에 두어야 할 몇가지 사항입니다.:
<ul>
<li> PCA는 연속적인 수량 또는 개수와 같은 숫자 특성에서만 작동합니다.
<li> PCA는 scale에 민감합니다. 타당한 이유가 없는한 PCA를 적용하기 전에 데이터를 표준화하는 것이 좋습니다.
<li> 결과에 과도한 영향을 미칠 수 있으므로 이상값을 제거하거나 제한하는 것이 좋습니다.
</ul>
</blockquote>

# 예제 - 1985 Automobiles

[*Automobile*](https://www.kaggle.com/toramky/automobile-dataset) 해당 데이터 세트를 통해 특성을 발견하는 서술적 기법을 사용하여 PCA를 적용해보겠습니다.

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
from IPython.display import display
from sklearn.feature_selection import mutual_info_regression


plt.style.use("seaborn-whitegrid")
plt.rc("figure", autolayout=True)
plt.rc(
    "axes",
    labelweight="bold",
    labelsize="large",
    titleweight="bold",
    titlesize=14,
    titlepad=10,
)


def plot_variance(pca, width=8, dpi=100):
    # Create figure
    fig, axs = plt.subplots(1, 2)
    n = pca.n_components_
    grid = np.arange(1, n + 1)
    # Explained variance
    evr = pca.explained_variance_ratio_
    axs[0].bar(grid, evr)
    axs[0].set(
        xlabel="Component", title="% Explained Variance", ylim=(0.0, 1.0)
    )
    # Cumulative Variance
    cv = np.cumsum(evr)
    axs[1].plot(np.r_[0, grid], np.r_[0, cv], "o-")
    axs[1].set(
        xlabel="Component", title="% Cumulative Variance", ylim=(0.0, 1.0)
    )
    # Set up figure
    fig.set(figwidth=8, dpi=100)
    return axs

def make_mi_scores(X, y, discrete_features):
    mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores


df = pd.read_csv("../input/fe-course-data/autos.csv")
```

다양한 속성을 포괄하는 4가지 특성을 선택했습니다. 각 특성은 타겟인 가격과 함께 높은 MI 점수를 가지고 있습니다. 이러한 특성은 자연스럽게 동일한 규모가 아니기 때문에 데이터를 표준화 할 것입니다.

```python
features = ["highway_mpg", "engine_size", "horsepower", "curb_weight"]

X = df.copy()
y = X.pop('price')
X = X.loc[:, features]

# Standardize
X_scaled = (X - X.mean(axis=0)) / X.std(axis=0)
```

scikit-learn의 PCA 추정기를 맞추고 주성분을 만들 수 있습니다.

```python
from sklearn.decomposition import PCA

# Create principal components
pca = PCA()
X_pca = pca.fit_transform(X_scaled)

# Convert to dataframe
component_names = [f"PC{i+1}" for i in range(X_pca.shape[1])]
X_pca = pd.DataFrame(X_pca, columns=component_names)

X_pca.head()
```

![Image](https://i.imgur.com/JrETr7D.png)

피팅 후 PCA 인스턴스는 components_ 속성에 로딩을 포함합니다.

```python
loadings = pd.DataFrame(
    pca.components_.T,  # transpose the matrix of loadings
    columns=component_names,  # so the columns are the principal components
    index=X.columns,  # and the rows are the original features
)
loadings
```

![Image](https://i.imgur.com/mr89BuF.png)

구성 요소 가중치의 부호와 크기는 캡처 된 변동의 종류를 알려줍니다. 첫 번째 구성요소(PC1)는 연비가 좋지 않은 크고 강력한 차량과 연비가 더 좋은 더 작고 경제적인 차량 간의 대조를 보여줍니다. 이것을 '럭셔리 / 이코노미'축이라고 부를 수 있습니다.  다음 그림은 우리가 선택한 네 가지 특성이 대부분 '럭셔리 / 이코노미' 축을 따라 다양하다는 것을 보여줍니다.

```python
# Look at explained variance
plot_variance(pca);
```
![Image](https://i.imgur.com/SCUii0b.png)

구성요소의 MI 점수도 살펴 보겠습니다. 당연히 PC1은 매우 유익하지만 나머지 구성요소는 작은 차이에도 불구하고 여전히 가격과 상당한 관계가 있습니다. 이러한 구성요소를 조사하는 것은 '럭셔리 / 이코노미' 축에서 포착되지 않은 관계를 찾는데 유용 할 수 있습니다. 

```python
mi_scores = make_mi_scores(X_pca, y, discrete_features=False)
mi_scores
```

```
PC1    1.014209
PC2    0.378508
PC3    0.306665
PC4    0.204934
Name: MI Scores, dtype: float64
```

세 번째 구성요소는 'horsepower'과 'curb_weight' (스포츠카 대 왜건)의 대조를 보여줍니다.

```python
# Show dataframe sorted by PC3
idx = X_pca["PC3"].sort_values(ascending=False).index
cols = ["make", "body_style", "horsepower", "curb_weight"]
df.loc[idx, cols]
```

![Image](https://i.imgur.com/z4BKPum.png)

이 대조를 표현하기 위해 새로운 특성을 만들어 보겠습니다. 

```python
df["sports_or_wagon"] = X.curb_weight / X.horsepower
sns.regplot(x="sports_or_wagon", y='price', data=df, order=2);
```

![Image](https://i.imgur.com/YbbI9Ea.png)

