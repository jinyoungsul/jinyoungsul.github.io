<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>2021-05-21-Data-Cleaning</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><h2 id="누락된-데이터-처리하기-isnull">누락된 데이터 처리하기 isnull</h2>
<p>산술 데이터에 한해 pandas는 누락된 데이터를 실수값인 NaN으로 취급한다. 이 특성을 이용해 데이터의 type이 float이라면 누락된 데이터가 있는지 의심을 가질 수 있습니다.</p>
<pre class=" language-python"><code class="prism  language-python">df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token string">'apple'</span><span class="token punctuation">,</span><span class="token number">2500</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'orange'</span><span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'banana'</span><span class="token punctuation">,</span><span class="token number">3000</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">,</span>columns<span class="token operator">=</span><span class="token punctuation">[</span><span class="token string">'name'</span><span class="token punctuation">,</span><span class="token string">'price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
df
</code></pre>
<p>|   |name    |price   |
|-- |--      |--      |
| 0 | apple  | 2500.0 |
| 1 | orange | NaN    |
| 2 | banana | 3000.0 |</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>isnull<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token builtin">sum</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>name 0
price 1
dtype: int64</p>
</blockquote>
<p>isnull 메소드는 누락되거나 NA인 값을 알려주는 boolean값이 저장된 같은 형태의 객체를 반환하는데 sum메소드를 사용해서 각 컬럼별 누락된 데이터의 수를 확인할 수 있습니다.</p>
<h3 id="누락된-데이터-골라내기-dropna">누락된 데이터 골라내기 dropna</h3>
<p>dropna 메소드를 사용하면 누락된 데이터가 있는 축(로우, 컬럼)을 제외 시킬 수 있습니다. DataFrame 객체의 경우에는 모두 NA값인 로우나 컬럼을 제외시키거나 NA값을 하나라도 포함하고 있는 로우나 컬럼을 제외시킬 수 있습니다.
<strong>note:</strong> 기본적으로는 NA값을 하나라도 포함하고 있는 로우를 제외시킵니다.</p>
<pre class=" language-python"><code class="prism  language-python">df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">,</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token number">4</span><span class="token punctuation">,</span><span class="token number">5</span><span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
df
</code></pre>
<p>|   | 0     | 1     | 2
|-- |--     |--     |--<br>
| 0 | 1.0   | 2.0   | 3.0
| 1 | 4.0   | 5.0   | NaN
| 2 | NaN   | NaN   | NaN</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>dropna<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
<p>|   | 0     | 1     | 2
|-- |--     |--     |--<br>
| 0 | 1.0   | 2.0   | 3.0
how='all' 옵션을 사용하면 모두 NA값인 로우만 제외시킵니다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>dropna<span class="token punctuation">(</span>how<span class="token operator">=</span><span class="token string">'all'</span><span class="token punctuation">)</span>
</code></pre>
<p>|   | 0     | 1     | 2
|-- |--     |--     |--<br>
| 0 | 1.0   | 2.0   | 3.0
| 1 | 4.0   | 5.0   | NaN
컬럼을 제외시키는 방법도 동일하게 동작하며 옵션으로 axis=1을 사용한다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span> <span class="token operator">=</span> np<span class="token punctuation">.</span>nan
df
</code></pre>
<p>|   | 0     | 1     | 2   |3
|-- |--     |--     |--   |--
| 0 | 1.0   | 2.0   | 3.0 | NaN
| 1 | 4.0   | 5.0   | NaN | NaN
| 2 | NaN   | NaN   | NaN | NaN</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>dropna<span class="token punctuation">(</span>how<span class="token operator">=</span><span class="token string">'all'</span><span class="token punctuation">,</span> axis<span class="token operator">=</span><span class="token number">1</span><span class="token punctuation">)</span>
</code></pre>
<p>|   | 0     | 1     | 2
|-- |--     |--     |--<br>
| 0 | 1.0   | 2.0   | 3.0
| 1 | 4.0   | 5.0   | NaN
| 2 | NaN   | NaN   | NaN</p>
<h3 id="결측치-채우기-fillna">결측치 채우기 fillna</h3>
<p>누락된 데이터를 제외시키지 않고 데이터를 어떻게든 채우고 싶은 경우가 있다. 이 경우 fillna 메소드를 활용하면 되는데, fillna 메소드에 채워 넣고 싶은 값을 넘겨주면 된다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>fillna<span class="token punctuation">(</span><span class="token number">5</span><span class="token punctuation">)</span>
</code></pre>
<p>|   | 0     | 1     | 2   |3
|-- |--     |--     |--   |--
| 0 | 1.0   | 2.0   | 3.0 | 5.0
| 1 | 4.0   | 5.0   | 5.0 | 5.0
| 2 | 5.0   | 5.0   | 5.0 | 5.0</p>
<p>각 컬럼에 fillna를 이용해서 Series의 평균값이나 중간값을 채울 수도 있습니다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>fillna<span class="token punctuation">(</span>df<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>mean<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>0    1.0
1    4.0
2    2.5
Name: 0, dtype: float64</p>
</blockquote>
<p>문자열의 데이터의 경우 Series의 value_counts()메소드를 이용해서 최빈값의 데이터를 넣어주는것도 하나의 아이디어이다.</p>
<pre class=" language-python"><code class="prism  language-python">df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token string">'bike'</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'bus'</span><span class="token punctuation">,</span><span class="token number">4</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'bike'</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">,</span>columns<span class="token operator">=</span><span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">,</span><span class="token string">'tire_num'</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
df
</code></pre>
<p>|   |type  |tire_num|
|-- |--    |--      |
| 0 | bike | 2      |
| 1 | bus  | 4      |
| 2 | bike | 2      |
| 3 | NaN  | 2      |</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">]</span><span class="token punctuation">.</span>fillna<span class="token punctuation">(</span>df<span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">]</span><span class="token punctuation">.</span>value_counts<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>index<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>0    bike
1     bus
2    bike
3    bike
Name: type, dtype: object</p>
</blockquote>
</div>
</body>

</html>
