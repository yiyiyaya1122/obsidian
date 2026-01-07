---
title: 深度学习入门：基于python的理论与实现
author: 斋藤康毅
date: 2025-01-18 Saturday
tags:
  - 个人成长
---
# 一、感知机
## 1. 逻辑电路
与门

| x1  | x2  |  y  |
| :-: | :-: | :-: |
|  0  |  0  |  0  |
|  1  |  0  |  0  |
|  0  |  1  |  0  |
|  1  |  1  |  1  |

或门

| x1  | x2  |  y  |
| :-: | :-: | :-: |
|  0  |  0  |  0  |
|  1  |  0  |  1  |
|  0  |  1  |  1  |
|  1  |  1  |  1  |

与非门

| x1  | x2  |  y  |
| :-: | :-: | :-: |
|  0  |  0  |  1  |
|  1  |  0  |  1  |
|  0  |  1  |  1  |
|  1  |  1  |  0  |


异或门

| x1  | x2  |  y  |
| :-: | :-: | :-: |
|  0  |  0  |  0  |
|  1  |  0  |  1  |
|  0  |  1  |  1  |
|  1  |  1  |  0  |

## 2. 神经网络
### 激活函数
a.  激活函数怎么来的？
b. 不同激活函数的优缺点？
c. 如何实现？前向传播？反向传播？

Step Function
$$ f(x) = \begin{cases} 0 & \text{if } x < 0 \\ 1 & \text{if } x \geq 0 \end{cases} $$
Sigmoid
$$f(x) = \frac{1}{1 + e^{-x}}$$
Tanh
$$ f(x) = \tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}} $$
ReLU
$$ f(x) = \begin{cases} x & \text{if } x > 0 \\ 0 & \text{if } x \leq 0 \end{cases} $$

Leaky ReLu
$$ f(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha x & \text{if } x \leq 0 \end{cases} $$
Softmax
$$ f(x_i) = \frac{e^{x_i}}{\sum_{j} e^{x_j}} $$

### 损失函数
a.  损失函数的作用？
b. 常用的损失函数？优缺点？
c. 如何实现？

MAE
$$ L(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i| $$
MSE
$$ L(y, \hat{y}) = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 $$

Cross-Entropy Loss
$$ L(y, \hat{y}) = - \sum_{i=1}^{C} y_i \log(\hat{y}_i) $$


### 优化器
a. 优化器的作用？
b. 常用的优化器有哪些？分析一下优缺点？
c. 实现？

SGD
$$ \theta = \theta - \eta \cdot \nabla_{\theta} L(\theta) $$
Momentum
$$ v_t = \beta v_{t-1} + (1 - \beta) \nabla_{\theta} L(\theta) $$ $$ \theta = \theta - \eta \cdot v_t $$
Adagrad: $$ G_t = G_{t-1} + \nabla_{\theta} L(\theta)^2 $$ $$ \theta = \theta - \frac{\eta}{\sqrt{G_t + \epsilon}} \cdot \nabla_{\theta} L(\theta) $$
RMSprop: $$ E[g^2]_t = \beta E[g^2]_{t-1} + (1 - \beta) \nabla_{\theta} L(\theta)^2 $$ $$ \theta = \theta - \frac{\eta}{\sqrt{E[g^2]_t + \epsilon}} \cdot \nabla_{\theta} L(\theta) $$Adam:
$$
m_t = \beta_1 m_{t-1} + (1 - \beta_1) \nabla_{\theta} L(\theta)
$$
$$
v_t = \beta_2 v_{t-1} + (1 - \beta_2) \nabla_{\theta} L(\theta)^2
$$
$$
\hat{m}_t = \frac{m_t}{1 - \beta_1^t}
$$
$$
\hat{v}_t = \frac{v_t}{1 - \beta_2^t}
$$
$$
\theta = \theta - \frac{\eta}{\sqrt{\hat{v}_t + \epsilon}} \cdot \hat{m}_t
$$
