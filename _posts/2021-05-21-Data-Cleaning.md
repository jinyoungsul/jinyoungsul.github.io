---
title: pandas 결측치 처리
tags: 
  - isnull
  - dropna
  - fillna
  - python
  - datascience
  - pandas
  - 결측치 처리
categories: pandas
date: '2021-05-21'

---

<h2 id="누락된-데이터-처리하기-isnull">누락된 데이터 처리하기 isnull</h2>
<p>산술 데이터에 한해 pandas는 누락된 데이터를 실수값인 NaN으로 취급한다. 이 특성을 이용해 데이터의 type이 float이라면 누락된 데이터가 있는지 의심을 가질 수 있습니다.</p>
<pre class=" language-python"><code class="prism  language-python">df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token string">'apple'</span><span class="token punctuation">,</span><span class="token number">2500</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'orange'</span><span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'banana'</span><span class="token punctuation">,</span><span class="token number">3000</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">,</span>columns<span class="token operator">=</span><span class="token punctuation">[</span><span class="token string">'name'</span><span class="token punctuation">,</span><span class="token string">'price'</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
df
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>name</th>
<th>price</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>apple</td>
<td>2500.0</td>
</tr>
<tr>
<td>1</td>
<td>orange</td>
<td>NaN</td>
</tr>
<tr>
<td>2</td>
<td>banana</td>
<td>3000.0</td>
</tr>
</tbody>
</table><pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>isnull<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token builtin">sum</span><span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>name 0<br>
price 1<br>
dtype: int64</p>
</blockquote>
<p>isnull 메소드는 누락되거나 NA인 값을 알려주는 boolean값이 저장된 같은 형태의 객체를 반환하는데 sum메소드를 사용해서 각 컬럼별 누락된 데이터의 수를 확인할 수 있습니다.</p>
<h3 id="누락된-데이터-골라내기-dropna">누락된 데이터 골라내기 dropna</h3>
<p>dropna 메소드를 사용하면 누락된 데이터가 있는 축(로우, 컬럼)을 제외 시킬 수 있습니다. DataFrame 객체의 경우에는 모두 NA값인 로우나 컬럼을 제외시키거나 NA값을 하나라도 포함하고 있는 로우나 컬럼을 제외시킬 수 있습니다.<br>
<strong>note:</strong> 기본적으로는 NA값을 하나라도 포함하고 있는 로우를 제외시킵니다.</p>
<pre class=" language-python"><code class="prism  language-python">df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">,</span><span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token number">4</span><span class="token punctuation">,</span><span class="token number">5</span><span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">,</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
df
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>1.0</td>
<td>2.0</td>
<td>3.0</td>
</tr>
<tr>
<td>1</td>
<td>4.0</td>
<td>5.0</td>
<td>NaN</td>
</tr>
<tr>
<td>2</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
</tbody>
</table><pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>dropna<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>1.0</td>
<td>2.0</td>
<td>3.0</td>
</tr>
</tbody>
</table><p>how=‘all’ 옵션을 사용하면 모두 NA값인 로우만 제외시킵니다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>dropna<span class="token punctuation">(</span>how<span class="token operator">=</span><span class="token string">'all'</span><span class="token punctuation">)</span>
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>1.0</td>
<td>2.0</td>
<td>3.0</td>
</tr>
<tr>
<td>1</td>
<td>4.0</td>
<td>5.0</td>
<td>NaN</td>
</tr>
</tbody>
</table><p>컬럼을 제외시키는 방법도 동일하게 동작하며 옵션으로 axis=1을 사용한다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">]</span> <span class="token operator">=</span> np<span class="token punctuation">.</span>nan
df
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
<th>3</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>1.0</td>
<td>2.0</td>
<td>3.0</td>
<td>NaN</td>
</tr>
<tr>
<td>1</td>
<td>4.0</td>
<td>5.0</td>
<td>NaN</td>
<td>NaN</td>
</tr>
<tr>
<td>2</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
</tbody>
</table><pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>dropna<span class="token punctuation">(</span>how<span class="token operator">=</span><span class="token string">'all'</span><span class="token punctuation">,</span> axis<span class="token operator">=</span><span class="token number">1</span><span class="token punctuation">)</span>
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>1.0</td>
<td>2.0</td>
<td>3.0</td>
</tr>
<tr>
<td>1</td>
<td>4.0</td>
<td>5.0</td>
<td>NaN</td>
</tr>
<tr>
<td>2</td>
<td>NaN</td>
<td>NaN</td>
<td>NaN</td>
</tr>
</tbody>
</table><h3 id="결측치-채우기-fillna">결측치 채우기 fillna</h3>
<p>누락된 데이터를 제외시키지 않고 데이터를 어떻게든 채우고 싶은 경우가 있다. 이 경우 fillna 메소드를 활용하면 되는데, fillna 메소드에 채워 넣고 싶은 값을 넘겨주면 된다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">.</span>fillna<span class="token punctuation">(</span><span class="token number">5</span><span class="token punctuation">)</span>
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>0</th>
<th>1</th>
<th>2</th>
<th>3</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>1.0</td>
<td>2.0</td>
<td>3.0</td>
<td>5.0</td>
</tr>
<tr>
<td>1</td>
<td>4.0</td>
<td>5.0</td>
<td>5.0</td>
<td>5.0</td>
</tr>
<tr>
<td>2</td>
<td>5.0</td>
<td>5.0</td>
<td>5.0</td>
<td>5.0</td>
</tr>
</tbody>
</table><p>각 컬럼에 fillna를 이용해서 Series의 평균값이나 중간값을 채울 수도 있습니다.</p>
<pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>fillna<span class="token punctuation">(</span>df<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">.</span>mean<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>0    1.0<br>
1    4.0<br>
2    2.5<br>
Name: 0, dtype: float64</p>
</blockquote>
<p>문자열의 데이터의 경우 Series의 value_counts()메소드를 이용해서 최빈값의 데이터를 넣어주는것도 하나의 아이디어이다.</p>
<pre class=" language-python"><code class="prism  language-python">df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">[</span><span class="token punctuation">[</span><span class="token string">'bike'</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'bus'</span><span class="token punctuation">,</span><span class="token number">4</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token string">'bike'</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token punctuation">[</span>np<span class="token punctuation">.</span>nan<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">]</span><span class="token punctuation">]</span><span class="token punctuation">,</span>columns<span class="token operator">=</span><span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">,</span><span class="token string">'tire_num'</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
df
</code></pre>

<table>
<thead>
<tr>
<th></th>
<th>type</th>
<th>tire_num</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td>bike</td>
<td>2</td>
</tr>
<tr>
<td>1</td>
<td>bus</td>
<td>4</td>
</tr>
<tr>
<td>2</td>
<td>bike</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>NaN</td>
<td>2</td>
</tr>
</tbody>
</table><pre class=" language-python"><code class="prism  language-python">df<span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">]</span><span class="token punctuation">.</span>fillna<span class="token punctuation">(</span>df<span class="token punctuation">[</span><span class="token string">'type'</span><span class="token punctuation">]</span><span class="token punctuation">.</span>value_counts<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>index<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">)</span>
</code></pre>
<blockquote>
<p>0    bike<br>
1     bus<br>
2    bike<br>
3    bike<br>
Name: type, dtype: object</p>
</blockquote>

