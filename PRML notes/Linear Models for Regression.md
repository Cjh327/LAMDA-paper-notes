## Linear Models for Regression

$$D=\{(x_1,y_1),\cdots,(x_N,y_N)\}$$ 

$$x_i\in\Bbb{R}^p,y_i\in\Bbb{R}$$ 

$$X=(x_1,\cdots,x_N)^T\quad(N\times p)$$ 

$$Y=(y_1,\cdots,y_N)^T\quad(N\times 1)$$



#### Least Squares

$$\begin{align}L(w)&=\sum\limits_{i=1}\limits^{N}||w^T x_i-y_i||^2\\&=\sum\limits_{i=1}\limits^{N}(w^T x_i-y_i)^2\\&=(w^T(x_1,\cdots,x_N)-(y_1,\cdots,y_N))\begin{pmatrix}w^Tx_1-y_1\\\vdots\\w^Tx_N-y_N\end{pmatrix} \\&=(w^TX^T-Y^T)(Xw-Y)\\&=wX^TXw-2w^TX^TY+Y^TY\end{align}$$ 

$$\hat{w}=\arg\min\limits L(w)$$  

$$\frac{\partial L(w)}{\partial w}=2X^TXw-2X^TY=0$$ 

$$\therefore \hat{w}=(X^TX)^{-1}X^TY$$   ( $(X^TX)^{-1}X^T$ 称为伪逆) 

**几何意义 ** 

 $X$ 视为 $p$ 个 $N$ 维列向量， $Y$ 不在由这 $p$ 维向量张成的空间内，最小二乘法即最小化 $Y$ 向量到这$p$ 维向量距离。 

$$f(w)=w^T x=x^T \beta$$ 

$$X^T(Y-X\beta)=0$$ 

$$\therefore \beta = (X^TX)^{-1}X^TY$$ 

**概率视角** 

$$y=f(w)+\epsilon = w^Tx+\epsilon\quad \epsilon\sim {\cal{N}}(0,\sigma^2)$$ 

$$y|x;w\sim {\cal{N}}(w^Tx,\sigma^2)$$

MLE (极大似然估计):

$$\begin{align}L(w)&=\log P(Y|X;w)\\&=\log\prod\limits_{i=1}^{N}p(y_i|x_i;w)\\&=\sum\limits_{i=1}\limits^{N}(\log\frac{1}{\sqrt{2\pi}\sigma}-\frac{(y_i-w^Tx_i)^2}{2\sigma^2})\end{align}$$ 

$$\begin{align}\therefore \hat{w}&=\arg\max\limits_w L(w)\\&=\arg\max\limits_w\sum\limits_{i=1}\limits^{N} -\frac{(y_i-w^Tx_i)^2}{2\sigma^2}\\&=\arg\min\limits_w\sum\limits_{i=1}\limits^{N}(y_i-w^Tx)^2\end{align}$$

**LSE** $\boldsymbol{\Leftrightarrow}$ **MLE and suppose that noise is Gaussian Distribution** 

