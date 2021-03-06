---
mathjax:
presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

## 統計量
パラメータ $\theta$ を持つ確率分布 $F_{\theta}$ において *iid* である標本 $X_1, X_2, \dots , X_n$
 が存在すると仮定する。

### 各種用語

- 点推定

標本 $X_n$ を用いてパラメータ $\theta$ の値を推定すること

$\hat{\theta} = h(X_1, X_2, \dots, X_n)$  

- 推定量 (Estimator)

Estimation process or rule for calculating statistic.

統計量を求めるために確率変数などを用いる考え方

$\overline{X} = \frac{1}{n} \sum_{i=1}^{i=n}X_{i}$

- 推定値 (Estimate)

Actual value based on a sample data.

実測値を用いて算出した計算結果

$\overline{x} = \frac{1}{n} \sum_{i=1}^{i=n}x_{i}$

[参考動画 (推定量と推定値)](https://www.hepokiki.com/%E8%AC%9B%E7%BE%A9%E3%83%93%E3%83%87%E3%82%AA/%E7%B5%B1%E8%A8%88%E5%AD%A6/%E6%8E%A8%E6%B8%AC%E7%B5%B1%E8%A8%88%E5%AD%A6/%E6%8E%A8%E5%AE%9A)

## 各種推定法

### 最尤法 (method of maximum likelihood)

尤もらしさを算出できる尤度関数 $L(\theta)$ を用いることで最尤推定量を求めることができる。

:::tip 尤度関数
$L(\theta) = \prod_{i=1}^{n}f(x_i; \theta)$
:::

![img](@/8th/img_1.png)


また、累積から和に変換でき、計算過程が単純になることから、対数尤度関数を用いて導出することが多い。

:::tip 対数尤度関数
$l(\theta) = logL(\theta) = \sum_{i=1}^{n}logf(x_i; \theta)$
:::

:::warning 注意
尤度方程式 (対数尤度関数を $\theta$ で偏微分したもの) の解が1つに定まらない場合がある。

また、標本が十分に大きい必要がある。
:::

[comment]: <> (:::details 例2 )

[comment]: <> (平均 $\mu$ と分散 $v$ が未知である正規分布に iid に従う標本 $X_1, \dots, X_n$が得られるとする。このとき $\mu$ および $v$ の最尤推定量は標本平均および標本分散になることを示せ。)


[comment]: <> (:::)

### モーメント法 (method of moments)

微分を毎回用いて統計量を算出することは時には困難な場合がある。そこで、**モーメント法 (積率推定法)** を用いることによって、推定量を導出することができる。

母数と積率の関係を表す式で、積率を標本積率に置き換えて解を母数の推定値とすることができる。

:::tip 復習 標本の中心積率
$\hat{\mu_1} = E[X] = 期待値$

$\hat{\mu_2} = E[(X-\mu_1)^2] = E[(X-E(X))^2] = 分散$
:::

:::details 証明 母数と積率の関係
母数の推定量は以下のように表すことができる。

$\hat{\mu} = \overline{X}$

$\hat{\sigma}^2 = \frac{1}{n}\sum_{i=1}^{n}(X_i-\overline{X})^2$

<証明>

母数と積率の関係は, 母平均を $\mu, 母分散を \sigma^2$ とすると以下のようにあらわされる。

$\mu_1 = \mu$

$\mu_2 = \sigma^2 + \mu^2$

つまり

$\mu = \mu_1$

$\sigma^2 = \mu_2 - \mu^2$

積率を標本積率で置換すると以下のようになる。

$\hat{\mu} = \hat{\mu_1} = \frac{1}{n}\sum_{i=1}^{n}X_i = \overline{X}$

$\hat{\sigma}^2 = \hat{\mu_2} - \hat{\mu}^2 =\hat{\mu_2} - \hat{\mu_1}^2\\ =\frac{1}{n}\sum_{i=1}^{n}X_i^2 - \overline{X}^2\\=\frac{1}{n}\sum_{i=1}^{n}(X_i-\overline{X})^2$
:::

[参照 (母数と積率の証明)](https://ymurasawa.web.fc2.com/us-sl18.pdf)  
[参照 (標本積率)](https://ymurasawa.web.fc2.com/us-ln07.pdf)

### 平均二乗誤差 (Mean Squared Error)

真のパラメータ $\theta$ と推定量 $\hat{\theta}$ の差異を評価するための指標。

:::tip
**平均二乗誤差**

$MSE_{\hat{\theta}} := E_{\theta}[(\hat{\theta} - \theta)^2]$

※ $E_\theta$ は確率分布 $F_\theta$ による期待値

**二つの推定量の精度を比較する**

$e(\hat{\theta_1}, \hat{\theta_2}) := \frac{E_\theta[(\hat{\theta_2} - \theta)^2]}{E_\theta[(\hat{\theta_1} - \theta)^2]}$
:::

## 点推定の性質

### バイアス・バリアンス分解 (bias-variance decomposition)

平均二乗誤差を **バイアス (bias / 偏り)** と **バイリアンス (variance / 分散)** に分解したもの。


$E_{\theta}[(\hat{\theta} - \theta)^2] = (E_\theta[\hat{\theta}] - \theta)^2 + V_\theta[\hat{\theta}] = (b_\theta(\hat{\theta}))^2 + V_\theta[\hat{\theta}]$

- バイアス

$b_\theta = E_\theta[\hat{\theta}] - \theta$

バイアスの項を 0 となるような不偏推定量 ($\hat{\theta}$) において、平均二乗誤差を最小化するためには **バリアンス (分散) を小さくしなければならない。** これを **一様最小分散不偏推定量 (uniformly minimum-variance unbiased estimator)** という。

### ガウス・マルコフの定理

一様最小分散不偏推定量の最小二乗法バージョン。
最良線形不変推定量ともよばれることも。

詳細は後でいい気がする

## 漸近的な性質

標本のサイズが十分に大きいときに推定の妥当性を評価する理論を漸近論という。

### クラーメル・ラオの不等式

一様最小分散不偏推定量であるかの判定に用いることができるものを **クラーメル・ラオの不等式** と呼ばれる。

:::tip 定義
$V_{\theta}[\hat{\theta}] \geq J_n(\theta)^{-1}$

尚、 $J_n(\theta)^{-1}$ は **フィッシャー情報量** (p63) によって求めることができる。
:::

上記の式を満たすような不偏推定量を **有効推定量 (efficient estimator)** という。また満たさない場合、 確率分布 $F_\theta$ に対して $\theta$ の有効推定量が存在しない。

### 十分統計量

以下を満たす統計量 $T(X)$ を **十分統計量と呼ぶ。**


$P(X = x \mid T(X) = t, \theta) = P(X = x \mid T(X) = t)$

> 解釈「パラメータ $\theta$ の情報を T(X) が十分に持っている」

どうやら、この公式が便利らしい (フィッシャーネイマンの分解定理) ので載せておきます (p63)。

:::tip フィッシャーネイマンの分解定理
$f(x; \theta) = h(x)g(T(x), \theta)$
:::

これの証明は 1級の範囲を逸脱しているそうなので、理解できれば良さげ。

あと、 $h(x)g(T(x))$ が何を表しているのかがよくわからなかったので、また分かれば説明します。

[参考 (定義がちゃんと書いてる)](http://mcm-www.jwu.ac.jp/~konno/pdf/statr28.pdf)

[ブログ (結構わかりやすそう)](https://www.bananarian.net/entry/2019/04/29/100000)


## 漸近有効性 と 一致性

不応本サイズが十分に大きく、適当な正則条件 ?? <- どういう意味？？

が成り立つとき、以下の式を満たすものを **漸近有効性を満たす** という。

:::tip 漸近有効性
$lim_{n \to \infty} nV_{\theta}[\hat{\theta}] = J_{1}(\theta)^{-1}$
:::

また、任意の値 $\epsilon > 0$ に対して、以下を満たすとき、その推定量が **一致性をもつ** という。（値のどっかに収束する）

:::tip 一致性
$lim_{n \to \infty} P(\mid \hat{\theta} - \theta \mid < \epsilon) = 1$
:::

## リサンプリング法
推定量が不偏ではなくバイアスがある場合、**ジャックナイフ法 (jackknife method)** を用いることで、得られている標本を再利用してバイアスを補正することができる。また、これによって求められる推定量を **ジャックナイフ推定量** という (p65)。 

:::tip ジャックナイフ推定量
$\hat{\theta}_{jack} = n\hat{\theta} - (n-1)\hat{\theta}_{(\cdot)}$
:::

バイアスを平均化することでより正確な値を求めることができる。