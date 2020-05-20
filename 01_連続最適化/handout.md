# 準ニュートン法とかのお話

今回は，$ f:\mathbb{R}^m \rightarrow \mathbb{R} $ となるような関数の**最小化**について考えていきます．

## ニュートン法とは？

- 一次微分の情報と二次微分の情報を使って，極値(最小値)を求める方法
- $f:\mathbb{R}^m \rightarrow \mathbb{R}$ が凸関数の場合，常に大域的最適解を求めることが可能

### ざっくりとした数学的な解説

1. 初期点 $ \mathbf{x}_0 = (x_{01}, \dots, x_{0m}) $ とする

2. 初期点 $ \mathbf{x}_0 $ の近傍を $ \mathbf{x}_0 + \Delta \mathbf{x} = (x_{01}+\Delta x_1,\dots, x_{0m}+\Delta x_m) $とし，$ \mathbf{x}_0 $周りの2次までのテーラー展開を考えると以下のようになる:
   $$
    f( \mathbf{x}_0 + \Delta \mathbf{x} ) = f(\mathbf{x}_0) + \sum_{i=1}^{n}\frac{\partial f(\mathbf{x}_0)}{\partial x_i}\Delta x_i + \frac{1}{2}\left( \frac{\partial}{\partial x_1}\Delta x_1 + \cdots + \frac{\partial}{\partial x_n}\Delta x_n \right)^2 f(\mathbf{x}_0) \tag{1}
   $$

3. (1)式を$ \Delta x_i $で微分すると以下のようになる:
   $$
    \frac{\partial f( \mathbf{x}_0 + \Delta \mathbf{x} )}{\partial x_i} = \frac{\partial f(\mathbf{x}_0)}{\partial x_i} + \sum_{k=1}^{m}\frac{\partial^2 f(\mathbf{x}_0)}{\partial x_i \partial x_k}\Delta x_k \tag{2}
   $$

4. 全ての $i$ について，(2)式が0となるとき，$f(\mathbf{x}_0 + \Delta \mathbf{x})$は極値を取る

5. $\mathbf{x}_0$における，$f$ の勾配ベクトルを $\nabla f_0$，ヘシアン(ヘッセ行列)を $H_0$ とすると，$\partial f( \mathbf{x}_0 + \Delta \mathbf{x} )/\partial x_i = 0$の解は次のように表せる:
   $$
    \Delta \mathbf{x} = -{H_0}^{-1}\nabla f_0
   $$
6. 次の点を $\mathbf{x}_1 = \mathbf{x}_0 - {H_0}^{-1} \nabla f_0$ に更新し，繰り返し計算を続ける

- 簡単に言ってしまえば，関数を二次近似して改善方向(と移動距離)を求めていく方法

### ニュートン法のメリット・デメリット

- メリット
  - 収束がとても早い (2次収束する)
  - 原理的に理解しやすい
- デメリット
  - ヘッセ行列を陽に求める必要がある
  - 初期点によっては収束しない

## 準ニュートン法

