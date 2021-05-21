---
title: pandas 결측치 처리
tags: 
  - isnull
  - dropna
  - fillna
  - python
  - datascience
  - pandas
  - 결측치처리
categories: pandas
date: '2021-05-21'

---

## 누락된 데이터 처리하기 isnull
산술 데이터에 한해 pandas는 누락된 데이터를 실수값인 NaN으로 취급한다. 이 특성을 이용해 데이터의 type이 float이라면 누락된 데이터가 있는지 의심을 가질 수 있습니다.
```python
df = pd.DataFrame([['apple',2500],['orange',np.nan],['banana',3000]],columns=['name','price'])
df
```
|   |name    |price   |
|---|:-------|:-------|
| 0 | apple  | 2500.0 |
| 1 | orange | NaN    |
| 2 | banana | 3000.0 |

| Default aligned | Left aligned | Center aligned  | Right aligned  |
|-----------------|:-------------|:---------------:|---------------:|
| First body part | Second cell  | Third cell      | fourth cell    |
| Second line     | foo          | **strong**      | baz            |
| Third line      | quux         | baz             | bar            |
|-----------------+--------------+-----------------+----------------|
| Second body     |              |                 |                |
| 2nd line        |              |                 |                |
|-----------------+--------------+-----------------+----------------|
| Third body      |              |                 | Foo            |

```python
df.isnull().sum()
```
```
name 0
price 1
dtype: int64
```
isnull 메소드는 누락되거나 NA인 값을 알려주는 boolean값이 저장된 같은 형태의 객체를 반환하는데 sum메소드를 사용해서 각 컬럼별 누락된 데이터의 수를 확인할 수 있습니다.

### 누락된 데이터 골라내기 dropna
dropna 메소드를 사용하면 누락된 데이터가 있는 축(로우, 컬럼)을 제외 시킬 수 있습니다. DataFrame 객체의 경우에는 모두 NA값인 로우나 컬럼을 제외시키거나 NA값을 하나라도 포함하고 있는 로우나 컬럼을 제외시킬 수 있습니다. 
**note:** 기본적으로는 NA값을 하나라도 포함하고 있는 로우를 제외시킵니다.

```python
df = pd.DataFrame([[1,2,3],[4,5,np.nan],[np.nan,np.nan,np.nan]])
df
```
| 1  | 0     | 1     | 2
|-- |--     |--     |--   
| 0 | 1.0   | 2.0   | 3.0
| 1 | 4.0   | 5.0   | NaN
| 2 | NaN   | NaN   | NaN

```python
df.dropna()
```
|  1 | 0     | 1     | 2
|-- |--     |--     |--   
| 0 | 1.0   | 2.0   | 3.0

how='all' 옵션을 사용하면 모두 NA값인 로우만 제외시킵니다.
```python
df.dropna(how='all')
```
| 1  | 0     | 1     | 2
|-- |--     |--     |--   
| 0 | 1.0   | 2.0   | 3.0
| 1 | 4.0   | 5.0   | NaN

컬럼을 제외시키는 방법도 동일하게 동작하며 옵션으로 axis=1을 사용한다.
```python
df[3] = np.nan
df
```
| 1  | 0     | 1     | 2   |3
|-- |--     |--     |--   |--
| 0 | 1.0   | 2.0   | 3.0 | NaN
| 1 | 4.0   | 5.0   | NaN | NaN
| 2 | NaN   | NaN   | NaN | NaN
```python
df.dropna(how='all', axis=1)
```
| 1  | 0     | 1     | 2
|-- |--     |--     |--   
| 0 | 1.0   | 2.0   | 3.0
| 1 | 4.0   | 5.0   | NaN
| 2 | NaN   | NaN   | NaN

### 결측치 채우기 fillna
누락된 데이터를 제외시키지 않고 데이터를 어떻게든 채우고 싶은 경우가 있다. 이 경우 fillna 메소드를 활용하면 되는데, fillna 메소드에 채워 넣고 싶은 값을 넘겨주면 된다.
```python
df.fillna(5)
```
|1   | 0     | 1     | 2   |3
|-- |--     |--     |--   |--
| 0 | 1.0   | 2.0   | 3.0 | 5.0
| 1 | 4.0   | 5.0   | 5.0 | 5.0
| 2 | 5.0   | 5.0   | 5.0 | 5.0

각 컬럼에 fillna를 이용해서 Series의 평균값이나 중간값을 채울 수도 있습니다.
```python
df[0].fillna(df[0].mean())
```
```
0    1.0
1    4.0
2    2.5
Name: 0, dtype: float64
```
문자열의 데이터의 경우 Series의 value_counts()메소드를 이용해서 최빈값의 데이터를 넣어주는것도 하나의 아이디어이다.
```python
df = pd.DataFrame([['bike',2],['bus',4],['bike',2],[np.nan,2]],columns=['type','tire_num'])
df
```
| 1  |type  |tire_num|
|-- |--    |--      |
| 0 | bike | 2      |
| 1 | bus  | 4      |
| 2 | bike | 2      |
| 3 | NaN  | 2      |

```python
df['type'].fillna(df['type'].value_counts().index[0])
```
```
0    bike
1     bus
2    bike
3    bike
Name: type, dtype: object
```
