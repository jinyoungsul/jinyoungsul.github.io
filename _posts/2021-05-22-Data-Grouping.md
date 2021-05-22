---
title: pandas groupby,agg,sort_values,sort_index
tags: 
  - python
  - datascience
  - pandas
  
categories: pandas
date: '2021-05-22'

---

## 그룹 분석 groupby, agg
우리는 데이터를 그룹화 한 다음 데이터가 속한 그룹에 특정한 작업을 수행할 수 있습니다. 
해당 작업은 groupby() 연산을 통해 수행합니다.

지금까지 많이 사용해온 함수 중 하나는 value_counts()입니다.
```python
df = pd.DataFrame({
    'key1':['a','b','c','a','b','a','a','b','b'],
    'key2':['one','two','three','two','one','one','two','one','two'],
    'data1':[1,2,3,4,5,6,11,12,13],
    'data2':[6,7,8,9,10,2,3,4,5]
})
df
```

|     |key1  |key2 |data1 |data2|
|-----|------|-----|------|-----|
|0    |   a  | one |   1  |  6  |
|1    |   b  | two |   2  |  7  |
|2    |   c  | three | 3 |  8   |
|3    |   a  | two |   4  |  9  |
|4    |   b  | one |   5  |  10 |
|5    |   a  | one |   6  |  2  |
|6    |   a  | two |  11  |  3  |
|7    |   b  | one |  12  |  4  |
|8    |   b  | two |  13  |  5  |
|9    |   a  | one |  4   |  6  |

```python
df.key1.value_counts()
```
```
a    5
b    4
c    1
Name: key1, dtype: int64
```

다음을 수행하여 value_counts()가 하는 일을 복제 할 수 있습니다.

```python
df.groupby('key1').key1.count()
```
```
key1
a    5
b    4
c    1
Name: key1, dtype: int64
```
groupby()는 key1을 각 그룹으로 생성하고 key1이 몇 번 나타나는지 계산했습니다.
value_counts()는 이 groupby() 작업의 손쉬운 방법입니다. 
또한 요약 함수를 사용할 수 있습니다. 
예를 들어 각 key1의 그룹에서 가장 적은 data1의 값을 얻으려면 다음과 같이 합니다.

```python
df.groupby('key1').data1.min()
```
```
key1
a    1
b    2
c    3
Name: data1, dtype: int64
```
이 DataFrame은 apply() 메소드를 사용하여 직접 액세스 할 수 있으며, 어떤 방식으로든 데이터를 조작할 수 있습니다.
예를 들어 각 key1의 그룹에서 첫 번째 data2를 선택하는 한 가지 방법은 다음과 같습니다.

```python
df.groupby('key1').apply(lambda df: df.data2.iloc[0])
```
```
key1
a    6
b    7
c    8
dtype: int64
```
보다 세분화된 제어를 위해 둘 이상의 열로 그룹화 할 수도 있습니다. 예를 들어, key1, key2로 그룹화하여 data2가 가장 높은 것을 고르는 방법은 다음과 같습니다.
```python
df.groupby(['key1','key2']).apply(lambda df:df.loc[df.data2.idxmax()])
```

|          |           |key1  |key2   |data1 |data2|
|-----     |-----      |------|-----  |------|-----|
|**key1**  |**key2**   |      |       |      |     |
| **a**    |**one**    |   a  | one   |   1  |  6  |
|          |**two**    |   a  | two   |   4  |  9  |
| **b**    |**one**    |   b  | one   |   5  |  10 |
|          |**two**    |   b  | two   |   2  |  7  |
| **c**    |**three**  |   c  | three |   3  |  8  |

언급 할 가치가 있는 또 다른 groupby() 메소드는 agg()로, DataFrame에서 여러 기능을 동시에 실행할 수 있습니다. 예를 들어 다음과 같이 간단한 통계 요약을 생성 할 수 있습니다.

```python
df.groupby('key1').data1.agg([len,min,max])
```

|         |len   |min  |max |
|-----    |------|-----|----|
|**key1** |      |     |    |
|**a**    |   5  | 1   |11  |
|**b**    |   4  | 2   |13  |
|**c**    |   1  | 3   | 3  |

## 멀티 인덱스 

groupby()는 우리가 실행하는 작업에 따라 때때로 다중 인덱스라고 불리는 결과가 발생합니다.

```python
key1_key2_df = df.groupby(['key1','key2']).data1.agg([len])
key1_key2_df
```

|          |           |len   |
|-----     |-----      |------|
|**key1**  |**key2**   |      |
| **a**    |**one**    |   3  |
|          |**two**    |   2  |
| **b**    |**one**    |   2  |
|          |**two**    |   2  |
| **c**    |**three**  |   1  |

```python
key1_key2_df.index
```
```
MultiIndex([('a',   'one'),
            ('a',   'two'),
            ('b',   'one'),
            ('b',   'two'),
            ('c', 'three')],
           names=['key1', 'key2'])
```
```python
key1_key2_df.loc['a']
```

|        | len|
|----    |----|
|**key2**|    |
|**one** |  3 |
|**two** |  2 |

다음과 같이 한번에 tuple을 이용해서 접근이 가능합니다.
```pyhton
key1_key2_df.loc[('a','one')]
```
```python
len    3
Name: (a, one), dtype: int64
```

일반적으로 가장 자주 사용하는 다중 인덱스 메소드는 일반 인덱스로 다시 변환하는 reset_index() 메소드입니다.

```python
key1_key2_df.reset_index()
```

|         |key1  |key2   |len |
|-----    |------|-----  |----|
|**0**    |   a  | one   | 3  |
|**1**    |   a  | two   | 2  |
|**2**    |   b  | one   | 2  |
|**3**    |   b  | two   | 2  |
|**4**    |   c  | three | 1  |

## 정렬 sort_values, sort_index
key1_key2_df를 다시 살펴보면 그룹화가 값 순서가 아닌 인덱스 순서로 반환한다는 것을 알 수 있습니다. 
> 즉, groupby의 결과를 출력 할 때 행의 순서는 데이터가 아닌 인덱스의 값에 따라 달라진다.

우리는 sort_values() 메소드를 이용해 원하는 순서대로 데이터를 가져와 직접 정렬 할 수 있습니다.
```python
key1_key2_df = key1_key2_df.reset_index()
key1_key2_df.sort_values(by='len')
```

|         |key1  |key2   |len |
|-----    |------|-----  |----|
|**4**    |   c  | three | 1  |
|**1**    |   a  | two   | 2  |
|**2**    |   b  | one   | 2  |
|**3**    |   b  | two   | 2  |
|**0**    |   a  | one   | 3  |

sort_values()는 기본적으로 오름차순 정렬이며 가장 낮은 값이 먼저 표시됩니다.
그러나 대부분의 경우 우리는 더 높은 숫자를 먼저 보여주는 내림차순 정렬을 원합니다. 따라서 다음과 같은 옵션을 주어 사용합니다.
```python
key1_key2_df.sort_values(by='len',ascending=False)
```

|         |key1  |key2   |len |
|-----    |------|-----  |----|
|**0**    |   a  | one   | 3  |
|**1**    |   a  | two   | 2  |
|**2**    |   b  | one   | 2  |
|**3**    |   b  | two   | 2  |
|**4**    |   c  | three | 1  |

인덱스 값을 기준으로 정렬하려면 sort_index()를 사용하면 됩니다.
```python
key1_key2_df.sort_index(ascending=False)
```
|         |key1  |key2   |len |
|-----    |------|-----  |----|
|**4**    |   c  | three | 1  |
|**3**    |   b  | two   | 2  |
|**2**    |   b  | one   | 2  |
|**1**    |   a  | two   | 2  |
|**0**    |   a  | one   | 3  |

마지막으로 한번에 둘 이상의 열을 기준으로 정렬 할 수 있습니다.
```python
key1_key2_df.sort_values(by=['key2','key1'])
```

|         |key1  |key2   |len |
|-----    |------|-----  |----|
|**0**    |   a  | one   | 1  |
|**2**    |   b  | one   | 2  |
|**4**    |   c  | three | 2  |
|**1**    |   a  | two   | 2  |
|**3**    |   b  | two   | 3  |
