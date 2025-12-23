
# 似然

## 1. 似然 

- **概率**：在参数 $θ$ **已知** 的情况下，预测未来观测到某数据 $D$ 的可能性，即$P(D|θ)$。
- **似然**：在数据 $D$ **已经观测到** 的情况下，反过来评估不同参数  $θ$ 的合理性，即$L(θ|D)$。

| 维度         | 概率（Probability）                                     | 似然（Likelihood）                                                            |
| ---------- | --------------------------------------------------- | ------------------------------------------------------------------------- |
| **核心定义**   | 固定模型参数 $θ$，事件 $X$ 发生的可能性                            | 固定观测数据 $X$，模型参数 $θ$ 为真实值的支持程度                                             |
| **变量与常量**  | 变量：事件 $X$；常量：模型参数 $θ$                               | 变量：模型参数 $θ$；常量：观测数据 $X$                                                   |
| **数学表示**   | $P (X; θ)$（分号表示 $θ$ 为固定参数）                          | $L (θ; X)$（分号表示 $X$ 为固定数据）                                                |
| **取值范围**   | $[0, 1]$（符合概率公理）                                    | $[0, +∞)$（非概率，仅表示相对支持度）                                                   |
| **技术场景举例** | 已知机器人雷达噪声服从 $σ=0.1$ 的高斯分布（$θ=σ$），预测某次测量误差$≤0.2$ 的概率 | 观测到机器人 10 次雷达测量误差（$X=[0.08, 0.12,...]$），判断 $σ=0.1$ 和 $σ=0.2$ 哪个更可能是真实噪声参数 |

## 2. 似然函数

**似然函数** 衡量的是，在给定不同的模型参数（如我们的 $θ$）时，**观察到我们手头现有数据** 的可能性有多大，在数学形式上，其**完全等于**在给定参数下数据出现的**联合概率**。
$$L(\theta | \mathbf{X}) = \prod_{i=1}^n P(X_i | \theta)$$

**伯努利分布**
$$L(p | \mathbf{X}) = \prod_{i=1}^n p^{x_i}(1-p)^{1-x_i} = p^{\sum x_i}(1-p)^{n-\sum x_i}$$

**正态分布**
$$L(\mu, \sigma^2 | \mathbf{X}) = \prod_{i=1}^n \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x_i-\mu)^2}{2\sigma^2}\right)$$

**泊松分布**
$$L(\lambda | \mathbf{X}) = \prod_{i=1}^n \frac{\lambda^{x_i} e^{-\lambda}}{x_i!}$$


## 3. 最大似然估计

**最大似然估计**(Maximum Likelihood Estimation, MLE)的目标是找到一个参数值 $\hat{\theta}$，使得似然函数 $L(\theta | \mathbf{X})$ 达到最大:
$$\hat{\theta}_{MLE} = \arg \max_{\theta \in \Theta} L(\theta | \mathbf{X})$$

通常，直接最大化似然函数 $L(θ)$在数学上比较困难，因为它常常是连乘的形式（比如独立同分布的数据）。一个更常用的技巧是最大化 **对数似然函数**。

1. **构建似然函数**:	$L(\theta | \mathbf{X}) = \prod_{i=1}^n P(X_i | \theta)$（对于独立同分布数据${x_1, x_2, \ldots, x_n}$）
2. **转化为对数似然函数**: $\ell(\theta) = \ln L(\theta) = \sum_{i=1}^n \ln P(x_i | \theta)$
3. **求解似然方程**: $\frac{\partial \ell(\theta)}{\partial \theta} = 0$
4. **检查二阶导数**: 确保找到的是最大值点（二阶导数为负）。


## 4. 贝叶斯估计
 
 基于**贝叶斯定理**，融合「先验信息（对参数的已有认知）」和「观测数据」，输出参数的**后验概率分布**（而非单点估计），是 MLE 的扩展（MLE 忽略先验信息）Bayesian Estimation
#TODO

## 5. 矩估计
（Method of Moments, MOM）
#TODO

## 6. 最小二乘估计
Least Squares Estimation, LSE
#TODO


# 三、从数学期望、方差、协方差到中心极限定理

## 3.1 数学期望

### 3.1.1 期望定义
**数学期望**（期望值、均值）是随机变量取值的**加权平均**，权重为概率。

**离散型随机变量** $X$，取值 $x_1, x_2, \ldots$，概率 $p_i = P(X=x_i)$：
$$
E[X] = \sum_{i} x_i p_i
$$

**连续型随机变量** $X$，概率密度函数 $f_X(x)$：
$$
E[X] = \int_{-\infty}^{\infty} x f_X(x) \, dx
$$

**可将其理解为**：长期重复试验中，随机变量取值的平均值。

### 3.1.2 期望计算示例
**例1**：掷一颗均匀骰子，$X$ 为点数。
$$
E[X] = \sum_{i=1}^{6} i \cdot \frac{1}{6} = \frac{1+2+3+4+5+6}{6} = 3.5
$$

**例2**：$X \sim \text{Exp}(\lambda)$，指数分布。
$$
\begin{aligned}
E[X] &= \int_{0}^{\infty} x \cdot \lambda e^{-\lambda x} \, dx \\
&= \left[-x e^{-\lambda x}\right]_0^{\infty} + \int_{0}^{\infty} e^{-\lambda x} \, dx \quad (\text{分部积分}) \\
&= 0 + \left[-\frac{1}{\lambda} e^{-\lambda x}\right]_0^{\infty} = \frac{1}{\lambda}
\end{aligned}
$$

**例3**：$X \sim N(\mu, \sigma^2)$，正态分布。
$$
\begin{aligned}
E[X] &= \int_{-\infty}^{\infty} x \cdot \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x-\mu)^2}{2\sigma^2}} \, dx \\
\text{令 } z = \frac{x-\mu}{\sigma}，则 x = \mu + \sigma z \\
E[X] &= \int_{-\infty}^{\infty} (\mu + \sigma z) \cdot \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \, dz \\
&= \mu \int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \, dz + \sigma \int_{-\infty}^{\infty} z \cdot \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \, dz \\
&= \mu \cdot 1 + \sigma \cdot 0 = \mu
\end{aligned}
$$

## 3.2 方差

### 3.2.1 定义
**方差**衡量随机变量取值相对于其均值的**离散程度**（波动大小）。

设 $X$ 的期望为 $\mu = E[X]$，则方差定义为：
$$
\text{Var}(X) = E[(X - \mu)^2]
$$

**标准差**：$\sigma_X = \sqrt{\text{Var}(X)}$

### 3.2.2 方差的性质
1. **非负性**：$\text{Var}(X) \geq 0$，且 $\text{Var}(X) = 0 \iff P(X=\mu)=1$

2. **常数方差**：$\text{Var}(c) = 0$

3. **线性变换**：
   $$
   \text{Var}(aX + b) = a^2 \text{Var}(X)
   $$

4. **简化计算公式**：
   $$
   \text{Var}(X) = E[X^2] - (E[X])^2
   $$

5. **独立变量的和**：
   若 $X_1, X_2, \ldots, X_n$ 相互独立，则
   $$
   \text{Var}\left(\sum_{i=1}^n X_i\right) = \sum_{i=1}^n \text{Var}(X_i)
   $$

6. **一般和的方差**（考虑协方差）：
   $$
   \text{Var}\left(\sum_{i=1}^n X_i\right) = \sum_{i=1}^n \text{Var}(X_i) + 2\sum_{i<j} \text{Cov}(X_i, X_j)
   $$

### 3.2.3 方差计算示例
**例1**：伯努利分布 $X \sim \text{Bernoulli}(p)$
$$
\begin{aligned}
E[X] &= 1 \cdot p + 0 \cdot (1-p) = p \\
E[X^2] &= 1^2 \cdot p + 0^2 \cdot (1-p) = p \\
\text{Var}(X) &= E[X^2] - (E[X])^2 = p - p^2 = p(1-p)
\end{aligned}
$$

**例2**：均匀分布 $X \sim U(a, b)$
$$
\begin{aligned}
E[X] &= \frac{a+b}{2} \\
E[X^2] &= \int_a^b x^2 \cdot \frac{1}{b-a} \, dx = \frac{1}{b-a} \cdot \frac{b^3 - a^3}{3} = \frac{a^2 + ab + b^2}{3} \\
\text{Var}(X) &= \frac{a^2 + ab + b^2}{3} - \left(\frac{a+b}{2}\right)^2 = \frac{(b-a)^2}{12}
\end{aligned}
$$

**例3**：正态分布 $X \sim N(\mu, \sigma^2)$
$$
\begin{aligned}
\text{Var}(X) &= E[(X-\mu)^2] = \int_{-\infty}^{\infty} (x-\mu)^2 \cdot \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x-\mu)^2}{2\sigma^2}} \, dx \\
\text{令 } z = \frac{x-\mu}{\sigma}，则 \\
\text{Var}(X) &= \sigma^2 \int_{-\infty}^{\infty} z^2 \cdot \frac{1}{\sqrt{2\pi}} e^{-z^2/2} \, dz \\
&= \sigma^2 \cdot 1 = \sigma^2 \quad (\text{标准正态的二阶中心矩为1})
\end{aligned}
$$


### 3.2.4 常见分布的方差
| 分布                               | 方差公式                     |
| -------------------------------- | ------------------------ |
| 伯努利 $\text{Bernoulli}(p)$        | $p(1-p)$                 |
| 二项 $\text{Binomial}(n, p)$       | $np(1-p)$                |
| 泊松 $\text{Poisson}(\lambda)$     | $\lambda$                |
| 几何 $\text{Geometric}(p)$         | $\frac{1-p}{p^2}$        |
| 均匀 $U(a, b)$                     | $\frac{(b-a)^2}{12}$     |
| 正态 $N(\mu, \sigma^2)$            | $\sigma^2$               |
| 指数 $\text{Exp}(\lambda)$         | $\frac{1}{\lambda^2}$    |
| 伽马 $\text{Gamma}(\alpha, \beta)$ | $\frac{\alpha}{\beta^2}$ |

## 3.3 协方差（Covariance）
### 3.3.1 定义
**协方差**衡量两个随机变量的**线性相关程度**。

设 $X, Y$ 是两个随机变量，期望分别为 $\mu_X = E[X]$，$\mu_Y = E[Y]$，则：
$$
\text{Cov}(X, Y) = E[(X - \mu_X)(Y - \mu_Y)]
$$

**简化计算公式**：
$$
\text{Cov}(X, Y) = E[XY] - E[X]E[Y]
$$

### 3.3.2 协方差的性质
1. **对称性**：$\text{Cov}(X, Y) = \text{Cov}(Y, X)$

2. **与自身关系**：$\text{Cov}(X, X) = \text{Var}(X)$

3. **双线性性**：
$$
   \begin{aligned}
   &\text{Cov}(aX + bY, Z) = a\text{Cov}(X, Z) + b\text{Cov}(Y, Z) \\
   &\text{Cov}(X, aY + bZ) = a\text{Cov}(X, Y) + b\text{Cov}(X, Z)
   \end{aligned}
$$
4. **常数协方差**：$\text{Cov}(X, c) = 0$

5. **独立则协方差为0**：
   若 $X, Y$ 独立，则 $\text{Cov}(X, Y) = 0$
   （注意：反之不成立！协方差为0不一定独立）

6. **方差与协方差关系**：
   $$
   \text{Var}(aX + bY) = a^2\text{Var}(X) + b^2\text{Var}(Y) + 2ab\text{Cov}(X, Y)
   $$

### 3.3.3 相关系数
为了消除量纲影响，定义**相关系数**：
$$
\rho_{XY} = \text{Corr}(X, Y) = \frac{\text{Cov}(X, Y)}{\sqrt{\text{Var}(X)\text{Var}(Y)}}
$$

**性质**：
1. $-1 \leq \rho_{XY} \leq 1$
2. $\rho_{XY} = 1 \iff Y = aX + b$，$a > 0$（完全正相关）
3. $\rho_{XY} = -1 \iff Y = aX + b$，$a < 0$（完全负相关）
4. $\rho_{XY} = 0$ 称 $X, Y$ **不相关**

### 3.3.4 协方差计算示例
**例1**：设 $(X, Y)$ 的联合分布为：
$$
\begin{aligned}
P(X=0, Y=0) = 0.2, \quad P(X=0, Y=1) = 0.3 \\
P(X=1, Y=0) = 0.4, \quad P(X=1, Y=1) = 0.1 
\end{aligned}
$$

**计算**：
$$
\begin{aligned}
E[X] &= 0 \times 0.5 + 1 \times 0.5 = 0.5 \\
E[Y] &= 0 \times 0.6 + 1 \times 0.4 = 0.4 \\
E[XY] &= 0 \times 0 \times 0.2 + 0 \times 1 \times 0.3 + 1 \times 0 \times 0.4 + 1 \times 1 \times 0.1 = 0.1 \\
\text{Cov}(X, Y) &= E[XY] - E[X]E[Y] = 0.1 - 0.5 \times 0.4 = -0.1
\end{aligned}
$$

**例2**：设 $X, Y$ 独立，$X \sim N(0,1)$，$Y \sim N(0,1)$，求 $\text{Cov}(X+Y, X-Y)$

**计算**：
$$
\begin{aligned}
\text{Cov}(X+Y, X-Y) &= \text{Cov}(X, X) - \text{Cov}(X, Y) + \text{Cov}(Y, X) - \text{Cov}(Y, Y) \\
&= \text{Var}(X) - \text{Cov}(X, Y) + \text{Cov}(X, Y) - \text{Var}(Y) \\
&= 1 - 0 + 0 - 1 = 0
\end{aligned}
$$
说明 $X+Y$ 与 $X-Y$ 不相关（且独立，因为正态分布下不相关等价于独立）。


## 3.4 协方差矩阵
### 3.4.1 定义
**协方差矩阵**可用来描述**多维随机变量各个分量之间的相关性结构**。对于 $n$ 维随机向量 $\mathbf{X} = (X_1, X_2, \ldots, X_n)^T$，其**协方差矩阵**为：
$$
\Sigma = \text{Cov}(\mathbf{X}) = E[(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T]
$$
其中 $\boldsymbol{\mu} = E[\mathbf{X}] = (E[X_1], \ldots, E[X_n])^T$。

**矩阵元素**：
$$
\Sigma_{ij} = \text{Cov}(X_i, X_j)
$$

**矩阵形式**：
$$
\Sigma = 
\begin{pmatrix}
\text{Var}(X_1) & \text{Cov}(X_1, X_2) & \cdots & \text{Cov}(X_1, X_n) \\
\text{Cov}(X_2, X_1) & \text{Var}(X_2) & \cdots & \text{Cov}(X_2, X_n) \\
\vdots & \vdots & \ddots & \vdots \\
\text{Cov}(X_n, X_1) & \text{Cov}(X_n, X_2) & \cdots & \text{Var}(X_n)
\end{pmatrix}
$$

### 3.4.2 性质
1. **对称性**：$\Sigma^T = \Sigma$

2. **半正定性**：对任意向量 $\mathbf{a} \in \mathbb{R}^n$，
   $$
   \mathbf{a}^T \Sigma \mathbf{a} \geq 0
   $$

3. **线性变换**：设 $\mathbf{Y} = A\mathbf{X} + \mathbf{b}$，则
   $$
   \text{Cov}(\mathbf{Y}) = A \text{Cov}(\mathbf{X}) A^T
   $$

4. **对角化**：可通过正交变换将协方差矩阵对角化。
### 3.4.3 相关系数矩阵
**相关系数矩阵** $R$：
$$
R_{ij} = \rho_{X_i X_j} = \frac{\text{Cov}(X_i, X_j)}{\sqrt{\text{Var}(X_i)\text{Var}(X_j)}}
$$

**矩阵形式**：
$$
R = 
\begin{pmatrix}
1 & \rho_{12} & \cdots & \rho_{1n} \\
\rho_{21} & 1 & \cdots & \rho_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
\rho_{n1} & \rho_{n2} & \cdots & 1
\end{pmatrix}
$$

### 3.4.4 从数据样本估计协方差矩阵

给定 $n$ 个样本，每个样本为 $p$ 维向量：
$$
\mathbf{x}_1, \mathbf{x}_2, \dots, \mathbf{x}_n \in \mathbb{R}^n
$$
组成数据矩阵（行是样本）, $X \in \mathbb{R}^{n \times p}$：
$$
X =
\begin{bmatrix}
x_{11} & x_{12} & \cdots & x_{1p} \\
x_{21} & x_{22} & \cdots & x_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
x_{n1} & x_{n2} & \cdots & x_{np}
\end{bmatrix}

$$

**1. 计算样本均值**
第 $j$ 个特征的样本均值：
$$
\bar{x}_j = \frac{1}{n} \sum_{i=1}^{n} x_{ij}
$$
组成均值向量：
$$
\bar{\mathbf{x}} =
\begin{bmatrix}
\bar{x}_1 & \bar{x}_2 & \cdots & \bar{x}_p
\end{bmatrix}
$$
**2. 计算中心化矩阵$X_{c}$**
$$
(X_c)_{ij} = x_{ij} - \bar{x}_j
$$
其矩阵形式为：
$$
X_c =
\begin{bmatrix}
\mathbf{x}_1 - \bar{\mathbf{x}} \\
\mathbf{x}_2 - \bar{\mathbf{x}} \\
\vdots \\
\mathbf{x}_n - \bar{\mathbf{x}}
\end{bmatrix}
$$
**3.样本协方差矩阵 $S$**
$$
\hat{\Sigma} = S = \frac{1}{n - 1} X_c^T X_c = \frac{1}{n-1} \sum_{k=1}^{n}
(\mathbf{x}_k - \bar{\mathbf{x}})
(\mathbf{x}_k - \bar{\mathbf{x}})^T
$$

### 3.4.5 举例说明

| $x1$ | $x2$ |
| ---- | ---- |
| $2$  | $3$  |
| $3$  | $5$  |
| $4$  | $7$  |

$$
\mathbf{x}_1 = \begin{bmatrix}2 \\ 3\end{bmatrix},\;
\mathbf{x}_2 = \begin{bmatrix}3 \\ 5\end{bmatrix},\;
\mathbf{x}_3 = \begin{bmatrix}4 \\ 7\end{bmatrix}
$$

**1. 计算样本均值**
$$
\bar{\mathbf{x}} =
\begin{bmatrix}
3 \\
5
\end{bmatrix}
$$

**2. 中心化**
$$
X_c =
\begin{bmatrix}
2-3 & 3-5 \\
3-3 & 5-5 \\
4-3 & 7-5
\end{bmatrix}
=
\begin{bmatrix}
-1 & -2 \\
0  &  0 \\
1  &  2
\end{bmatrix}
$$

**3. 计算样本协方差矩阵 $S$**

$$
X_c^T =
\begin{bmatrix}
-1 & 0 & 1 \\
-2 & 0 & 2
\end{bmatrix}
$$
$$
X_c^T X_c =
\begin{bmatrix}
2 & 4 \\
4 & 8
\end{bmatrix}
$$
$$
S = \frac{1}{2}
\begin{bmatrix}
2 & 4 \\
4 & 8
\end{bmatrix}
=
\begin{bmatrix}
1 & 2 \\
2 & 4
\end{bmatrix}

$$

**4. 求特征值**
$$
\det(S - \lambda I) = 0
$$
$$
\left|
\begin{matrix}
1-\lambda & 2 \\
2 & 4-\lambda
\end{matrix}
\right|
= (1-\lambda)(4-\lambda) - 4
= \lambda^2 - 5\lambda = 0
$$
可得$\lambda_1 = 5,\quad \lambda_2 = 0$
- $\lambda_1 = 5,$：  
    👉 第一主成分方向上的 **样本方差**
- $\lambda_2 = 0$：  
    👉 第二个正交方向上 **完全没有任何方差**

这说明**所有数据点都严格落在一条直线上**

**5. 计算第一主成分方向**
解$(S - 5I)\mathbf{v} = 0$
即： 
$$
\begin{bmatrix}
-4 & 2 \\
2 & -1
\end{bmatrix}
\mathbf{v} = 0
$$
解得一个方向向量：
$$
\mathbf{v}_1 =
\begin{bmatrix}
1 \\
2
\end{bmatrix}
$$
归一化：
$$
\mathbf{v}_1 = \frac{1}{\sqrt{5}}
\begin{bmatrix}
1 \\
2
\end{bmatrix}
$$


$$
D_{\mathbf{u}} f(\mathbf{x})
=
\lim_{h \to 0}
\frac{f(\mathbf{x} + h\mathbf{u}) - f(\mathbf{x})}{h}

$$
