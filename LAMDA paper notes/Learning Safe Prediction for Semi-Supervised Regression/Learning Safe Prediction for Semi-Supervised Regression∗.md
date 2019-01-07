## Learning Safe Prediction for Semi-Supervised Regression∗

Yu-Feng Li and Han-Wen Zha and Zhi-Hua Zhou  
​	*National Key Laboratory for Novel Software Technology, Nanjing University, Nanjing 210023, China*  
​	*Collaborative Innovation Center of Novel Software Technology and Industrialization, Nanjing 210023, China*  

#### assumption

one assumes that $\boldsymbol{\alpha}$ is from a convex linear set $M = \{\boldsymbol{\alpha}|\boldsymbol{A}^{T}\boldsymbol{\alpha} ≤ \boldsymbol{b}; \boldsymbol{\alpha} ≥ 0\}$

#### Problem Setting and Formulation

Optimize the worst-case performance gain:   

$\max \limits_{\boldsymbol{f}\in \Bbb{R}^{u}} \min \limits_{\boldsymbol{\alpha} \in M}\sum_{i=1}^{b}\alpha_{i}(||\boldsymbol{f}_{0}-\boldsymbol{f}_{i}||^{2}-||\boldsymbol{f}-\boldsymbol{f}_{i}||^{2})$  

Note that the equation is concave to $\boldsymbol{f}$ and convex to $\boldsymbol{\alpha}$, and thus it is recognized as saddle-point convex-concave optimization. However, it is non-trivial to be solved efficiently because of poor convergence rate induced by typical gradient descent algorithms.  

#### Representation to Geometric Projection 

By setting the derivative of the equation w.r.t. $\boldsymbol{f}$ to zero, the equation has a closed-form solution w.r.t. $\boldsymbol{f}$ as:  

$$\boldsymbol{f} =\sum_{i=1}^{b} \alpha_{i}\boldsymbol{f}_{i}$$  

We then get the following equivalent form that only relates to $\boldsymbol{\alpha}$:  

$$\min \limits_{\boldsymbol{\alpha}\in  M}||\sum^{b}_{i=1}\alpha_{i}\boldsymbol{f}_{i}-\boldsymbol{f}_{0}||^{2}$$

By expanding the quadratic form, it can be rewritten as:  

$$\min \limits_{\boldsymbol{\alpha}\in M} \boldsymbol{\alpha}^{T}\boldsymbol{F}\boldsymbol{\alpha}-\boldsymbol{v}^{T}\boldsymbol{\alpha}$$  

where $\boldsymbol{F}\in \Bbb{R}^{b\times b}$ is a linear kernel matrix of $\boldsymbol{f}_{i}$'s, i.e., $F_{ij}=\boldsymbol{f}_{i}^{T}\boldsymbol{f}_{i} ,\forall 1\leq i,j\leq b$ and $\boldsymbol{v}=[2\boldsymbol{f}_{1}^{T}\boldsymbol{f}_{0};\cdots;2\boldsymbol{f}_{b}^{T}\boldsymbol{f}_{0}]$  

Since $\boldsymbol{F}$ is semi-definite, the equation is convex.  

#### How the Proposal Works
- **Theorem 1**.  $\bar{\boldsymbol{f}}-\boldsymbol{f}^{*}\leq ||\boldsymbol{f}_{0}-\boldsymbol{f}^{*}||$, if the ground truth label assignment $\boldsymbol{f}^{*}\in \Omega=\{\boldsymbol{f}|\sum^{b}_{i=1}\alpha_{i}\boldsymbol{f}_{i}, \boldsymbol{\alpha}\in M\}$

  Theorem 1 reveals that the proposal is provably safe, when ground-truth label assignment is realized by a convex linear combination of base regressors.  

- **Theorem 2**. $\bar{\boldsymbol{f}}$ has already achieved the maximal worst-case performance gain against $\boldsymbol{f}_{0}$, if the ground truth $\boldsymbol{f}^{*}\in\Omega$. Specifically, $\bar{\boldsymbol{f}}$  is the optimal solution of the following functional,  

  $$\bar{\boldsymbol{f}}=\arg \max \limits_{\boldsymbol{f}\in \Bbb{R}^{u}}\min\limits_{\boldsymbol{f}^{*}\in\Omega}(||\boldsymbol{f}_{0}-\boldsymbol{f}^{*}||^{2}-||\boldsymbol{f}-\boldsymbol{f}^{*}||^{2}$$  

  With Theorems 1-2, it is now clear that the proposed method is provably safe and achieves the maximal worst-case performance gain, if the ground-truth label assignment is realized by a convex linear combination of base regressors.   

#### Algorithm

**Algorithm** The SAFER Method

**Input**: multiple SSR predictions $\{\boldsymbol{f}_{i}\}^{b}_{i=1}$ and certain direct supervised regression prediction $\boldsymbol{f}_{0}$

**Output**: the learned prediction $\bar{\boldsymbol{f}}$

1. Construct a linear kernel matrix $\bar{\boldsymbol{F}}$ where $F_{ij}=\boldsymbol{f}_{i}^{T}\boldsymbol{f}_{j}, \forall 1\leq i,j\leq b$
2. Derive a vector $\boldsymbol{v}=[2\boldsymbol{f}_{1}^{T}\boldsymbol{f}_{0};\cdots;2\boldsymbol{f}_{b}^{T}\boldsymbol{f}_{0}]$
3. Solve the convex quadratic optimization and obtain the optimal solution $\boldsymbol{\alpha}^{*}=[\alpha_{1}^{*},\cdots,\alpha_{b}^{*}]$
4. Return $\bar{\boldsymbol{f}}=\sum_{i=1}^{b}\alpha_{i}^{*}\boldsymbol{f}_{i}$

#### Summary

Consider the learning of a safe prediction from multiple semi-supervised regressors, which is not worse than a direct supervised learner with only labeled data.   

aim: to optimize the worst-case performance gain   

算法：输入多个semi-supervised regression的预测结果和一个direct supervised regression的预测结果，计算这些结果的线性核(linear kernel)，解优化问题，返回新的预测值。  

论文中证明了在ground-truth label assignment is realized by a convex linear combination of base regressors(算法输入凸集？)假设下，该方法是safe的。  