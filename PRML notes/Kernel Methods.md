## Kernel Methods

$$k(\boldsymbol{x},\boldsymbol{x'})=\phi(\boldsymbol{x})^T\phi(\boldsymbol{x'})$$



##### 核函数：

$$k: \cal{X}\times \cal{X} \rightarrow \Bbb{R} $$

$$\forall x,z\in \cal{X}$$，则称 $k(x,z)$ 为核函数



##### 正定核：

$$k: \cal{X}\times \cal{X} \rightarrow \Bbb{R} $$

$\forall x,z\in \cal{X}$ ，有$k(x,z)$，如果$k(x,z)$满足：

1. 对称性   $k(x,z)=k(z,x)$
2. 正定性  任取$N$个元素， $x_1,x_2,\cdots,x_N\in\cal{X}$ ，对应的Gram Matrix是半正定的

则称$k(x,z)​$为正定核函数 

Gram Matrix $K = [k(x_i,x_j)]$



线性核 $k(\boldsymbol{x_i},\boldsymbol{x_j})=\boldsymbol{x_i}^T\boldsymbol{x_j}$

高斯核  $k(\boldsymbol{x_i},\boldsymbol{x_j})=\exp(-\frac{||\boldsymbol{x_i}-\boldsymbol{x_j}||^2}{2\sigma^2})$



#### Gaussian Process Regression:

##### Gaussian Process

高斯过程是定义在连续域上的无限多个高维随机变量所组成的随机过程

**Definition:** 

$\{\xi_t\}_{t\in T}$ where $T: $ continuous time/space.

If $\forall n \in N^+, t_1,\cdots,t_n(\mbox{index})\rightarrow \xi_1,\xi_2,\cdots,\xi_n(\mbox{r.v.})$ , 

let $\xi_{1:n}=(\xi_1,\xi_2,\cdots, \xi_n)^T$ 

If $\xi_{1:n}\sim\cal{N}(\mu_{1:n},\Sigma_{1:n})$ , then $\{\xi_t\}_{t\in T}$ is a Gaussian Process, $\xi_t\sim GP(m(t),K(t,s))$ 



two views (equal result): 

1. **weight-space view** 

   care $w$ 

   $$\begin{cases}f(x)=\phi^T(x)w\\y=f(x)+\epsilon\quad \epsilon\sim {\cal{N}}(0,\sigma^2)\end{cases} $$ 

   Bayessian Linear Regression + Kernel trick 

   **Bayesian Method:** 

   Given prior: $w\sim{\cal{N}}(0,\Sigma_p)$

   $$\because f(x)=\phi^T(x)w\\ \therefore E[f(x)]=E[\phi^T(x)w]=\phi^T(x)E[w]=0$$

   $$\begin{align}\forall x,x'\in \Bbb{R}^p, cov(f(x),f(x'))&=E[(f(x)-E[f(x')])(f(x')-E[f(x)])]\\&=E[f(x)f(x')]\\&=E[\phi(x)w\cdot\phi(x')^Tw]\\&=E[\phi(x)w\cdot w^T\phi(x')]\end{align}$$  

   $$(\because \phi(x')^Tw \mbox{ is a one-dim real number }\therefore  \phi(x')^Tw=w^T\phi(x'))$$ 

   $$\begin{align}cov(f(x),f(x'))&=\phi(x)^T E[ww^T]\phi(x')\\&=\phi(x)^T \Sigma_p\phi(x')\\&=k(x,x')\end{align}$$ 

   which is similar to the definition of GP

   $\{f(x)\}$ can be seen as a GP

2. **function-space view** 

   care $f(x)$ 

   $f(x)$ is a random variable(r.v.) and $f(x)\sim GP(m(x),k(x,x'))$ ( $\{f(x)\}$ is a Gaussian Process).

   Definition:

   $$\{f(x)\}_{x\in\Bbb{R}}\sim GP(m(x),K(x,x'))$$

   $$m(x)=E[f(x)]$$ 

   $$K(x,x')=E[(f(x)-m(x))(f(x')-m(x'))^T]$$ 

   **Regression:** 

   Data: $\{(x_i,y_i)\}_{i=1}^N$

   $$X=(x_1,\cdots, x_N)^T\quad N\times p$$ 

   $$Y=(y_1,\cdots,y_N)^T\quad N\times 1$$ 

   Suppose $f(X)\sim {\cal{N}} (\mu(X),K(X,X))$

   $$Y=f(X)+\epsilon$$  

   Prediction:  Given $X^*=(x_1^*,\cdots,x_M^*)$ , $Y^*=f(X^*)+\epsilon$ 

   $$\begin{pmatrix}Y\\f(X^*) \end{pmatrix}\sim{\cal{N}}(\begin{pmatrix}\mu(X)\\\mu(X^*) \end{pmatrix},\begin{pmatrix}K(X,X)+\sigma^2I\quad k(X,X^*)\\K(X^*,X)\quad K(X^*,X^*) \end{pmatrix})$$

   object:  $P(f(X^*)|Y,X,X^*)$ (已知联合高维分布，求条件概率)

   使用公式可直接求出 

Guassian Process Regression is the extension of Bayesian Linear Regression with kernel trick.