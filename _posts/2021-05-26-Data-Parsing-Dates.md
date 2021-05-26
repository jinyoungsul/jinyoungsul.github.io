## Pandas Parsing Dates

```python
import pandas as pd
import seaborn as sns
```

```python
df = pd.DataFrame({'Date':['3/2/07','3/22/07','4/6/07','4/14/07','4/15/07']})
df
```

|    | Date    |
|----| ------  |
| 0  | 3/2/07  |
| 1  | 3/22/07 |
| 2  | 4/6/07  |
| 3  | 4/14/07 |
| 4  | 4/15/07 |

```python
df.Date
```
```
0     3/2/07
1    3/22/07
2     4/6/07
3    4/14/07
4    4/15/07
Name: Date, dtype: object
```
Date 열을 살펴보니 날짜로 표현되어 있습니다. 하지만 Python이 이 데이터가 날짜라는 것을 알고 있을까요? 데이터의 유형을 보면 "object"임을 알 수 있습니다. Pandas의 dtype 문서를 확인해보면 datetime64 dtype도 있음을 알 수 있습니다. 
열의 dtype이 object이기 때문에 Python이 이 열에 날짜가 포함되어 있다는 것을 알지 못합니다.

그럼, Date컬럼을 datetime형식으로 변환해볼까요?
[strftime 지시문](https://strftime.org/) 이라는 가이드를 통해 날짜 형식이 무엇인지 알 수 있습니다. 
날짜의 가능한 부분이 많이 있지만 가장 일반적인 부분은 일의 경우 %d, 월의 경우 %m, 두 자리 연도의 경우 %y, 네 자리 연도의 경우 %Y입니다.

Some examples:
- 1/17/07의 포맷은 "%m/%d/%y"
- 17-1-2007의 포맷은 "%d-%m-%Y"

```python
df['date_parsed'] = pd.to_datetime(df.Date, format="%m/%d/%y")
df
```

|    | Date    | date_parsed|
|----| ------  |------------|
| 0  | 3/2/07  | 2007-03-02 |
| 1  | 3/22/07 | 2007-03-22 |
| 2  | 4/6/07  | 2007-04-06 |
| 3  | 4/14/07 | 2007-04-14 |
| 4  | 4/15/07 | 2007-04-15 |

```python
df['date_parsed'].head()
```
```
0   2007-03-02
1   2007-03-22
2   2007-04-06
3   2007-04-14
4   2007-04-15
Name: date_parsed, dtype: datetime64[ns]
```
새 열의 행을 확인하면 dtype이 datetime64임을 알 수 있습니다.  또한 날짜가 (년-월-일)에 맞도록 약간 재정렬 된 것을 볼 수 있습니다.

<br>
파싱 된 날짜 열이 있으므로 날짜와 같은 정보를 추출 할 수 있습니다.

```python
day_df = df['date_parsed'].dt.day
day_df
```
```
0     2
1    22
2     6
3    14
4    15
Name: date_parsed, dtype: int64
```
