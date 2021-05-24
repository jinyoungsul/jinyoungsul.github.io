---
title: pandas dtype, info
tags: 
  - python
  - datascience
  - pandas
  
categories: pandas
date: '2021-05-23'

---

## 데이터 타입 dtype, info

DataFrame 또는 Series의 열에 대한 데이터 유형을 dtype이라고 합니다.

dtype 속성을 사용하여 특정 열의 유형을 가져올 수 있습니다.

```python
df = pd.DataFrame({'key':['a','b','c'],'data1':[1,2,3],'data2':[3.3,4.4,5.5]})
df
```

|     | key    | data1 | data2 |
|-----|-------|--------|-------|
|0    | a     | 1      | 3.3   |
|1    | b     | 2      | 4.4   |
|2    | c     | 3      | 5.5   |

```python
df.data1.dtype
```
```
dtype('int64')
```
<br>

데이터 타입은 pandas가 내부적으로 데이터를 저장하는 방법에 대해 알려줍니다. int64는 64비트 정수 숫자를 사용하고 있음을 의미합니다.

염두에 두어야 할 한 가지 특징은 문자열로 구성된 열은 자체 유형을 얻지 못한다는 것입니다. 대신 object 유형이 제공됩니다.

astype() 메소드를 사용하여 이러한 변환이 타당 할 때마다 한 유형의 열을 다른 유형으로 변환 할 수 있습니다. 예를 들어 data1 열을 기존 int64 데이터 유형에서 float64 데이터 타입으로 변환 할 수 있습니다.

```python
df.data1.astype('float64')
```
```
0    1.0
1    2.0
2    3.0
Name: data1, dtype: float64
```
**note**: astype() 메소드를 사용한다고 해서 원본 자체의 데이터 타입이 바뀌는 것이 아니기 때문에 변환한 데이터를 재할당 해줘야 한다.
```python
df.data1 = df.data1.astype('float64')
```

<br>

전체 데이터에 대한 유형을 쉽게 확인하는 방법이 있을까? 그럴때는 info() 메소드를 사용해보자.

```python
df.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 3 entries, 0 to 2
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   key     3 non-null      object 
 1   data1   3 non-null      int64  
 2   data2   3 non-null      float64
dtypes: float64(1), int64(1), object(1)
memory usage: 200.0+ bytes
```

info()는 index, dtype 및 열, null이 아닌 값 및 메모리 사용량을 알려주어 굉장히 자주 쓰는 메소드이니 꼭 기억하도록 하자.



