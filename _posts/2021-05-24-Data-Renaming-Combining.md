---
title: pandas rename, concat, join
tags: 
  - python
  - datascience
  - pandas
  
categories: pandas
date: '2021-05-24'

---

## 데이터 인덱스, 열 이름 변경 rename

종종 데이터는 만족스럽지 않은 열 이름, 인덱스 이름으로 우리에게 제공됩니다. 이 경우 rename 함수를 사용하여 문제가 되는 항목의 이름을 더 나은 이름으로 변경할 수 있습니다.

```python
df = pd.DataFrame({'key':['a','b','c'],'data':[1,2,3]})
df
```

|   | key  | data  |
|---|------|-------|
| 0 | a    | 1     |
| 1 | b    | 2     |
| 2 | c    | 3     |


<br>
rename()으로 인덱스 이름 및 열 이름을 변경할 수 있습니다.
원래 객체를 변경하지 않고 새로운 객체를 생성하므로, 원본 데이터를 바로 변경하려면 inplace=True 옵션을 줘야합니다.

```python
df.rename(columns={'key':'key2'})
```
|   | key2  | data  |
|---|------|-------|
| 0 | a    | 1     |
| 1 | b    | 2     |
| 2 | c    | 3     |

```python
df.rename(index={0: 'first', 1: 'second'})
```

|        | key  | data  |
|------- |------|-------|
| first  | a    | 1     |
| second | b    | 2     |
| 2      | c    | 3     |

## 데이터 결합 concat, join
데이터 세트에 대한 작업을 수행 할 때 때때로 다른 DataFrame 및 Series를 결합해야합니다. Pandas에는이를위한 핵심 방법이 있는데
concat()과 join()에 대해서 알아보겠습니다.

먼저 concat()은 축을 따라 데이터를 합치는 기능을 제공합니다.
이는 서로 다른 DataFrame 또는 Series에 동일한 열이 있는 경우에 유용합니다.

```python
df = pd.DataFrame({'key':['a','b','c'],'data':[1,2,3]})
df
```

|   | key  | data  |
|---|------|-------|
| 0 | a    | 1     |
| 1 | b    | 2     |
| 2 | c    | 3     |

```python
df2 = pd.DataFrame({'key':['d','e','f','g'],'data':[4,5,6,7]})
df2
```

|   | key  | data  |
|---|------|-------|
| 0 | d    | 5     |
| 1 | e    | 6     |
| 2 | f    | 7     |
| 3 | g    | 8     |

<br>

axis=0을 기본값으로 하여 새로운 객체를 생성합니다.

```python
pd.concat([df,df2])
```

|   | key  | data  |
|---|------|-------|
| 0 | a    | 1     |
| 1 | b    | 2     |
| 2 | c    | 3     |
| 0 | d    | 4     |
| 1 | e    | 5     |
| 2 | f    | 6     |
| 3 | g    | 7     |

```python
pd.concat([df,df2],axis=1)
```

|   | key  | data  | key | data |
|---|------|-------|---- |------|
| 0 | a    | 1.0   | d   | 4    |
| 1 | b    | 2.0   | e   | 5    |
| 2 | c    | 3.0   | f   | 6    |
| 3 | NaN  | NaN   | g   | 7    |

---
join()은 인덱스가 공통인 다른 DataFrame 객체를 결합 할 수 있습니다.

```python
df.join(df2,lsuffix='_df',rsuffix='_df2')
```

|   | key_df  | data_df  | key_df2 | data_df2 |
|---|------   |-------   |----     |------    |
| 0 | a       | 1.0      | d       | 4        |
| 1 | b       | 2.0      | e       | 5        |
| 2 | c       | 3.0      | f       | 6        |

lsuffix 및 rsuffix 옵션은 데이터가 df 및 df2에서 동일한 열 이름을 갖기 때문에 여기에 필요합니다.


