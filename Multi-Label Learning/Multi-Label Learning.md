# Multi-Label Learning 

Author: Zhi-Hua Zhou and Min-Ling Zhang



Structure:

$X=R^{d}$: $d$-dimensional instance space

$Y=\{y_{1},y_{2},...,y_{q}\}$: the label space consisting of $q$ class labels.

$D=\{(x_{i},Y_{i}) |1 \leq i \leq m\}$: multi-label training set

$h: X \rightarrow 2^{Y}$: the function to learn



##### ML-KNN: 

应用kNN算法的思想

##### RANK-SVM:

学习$q$ 个线性分类器$W={(w_{j},b_{j})|1 \leq j \leq q}$

margin定义为所有relevant-irrelevant组到超平面的距离的最小值，计算时利用 relevant-irrelevant label pair $(y_{j}, y_{k})​$ 对应的参数之差$w_{j}-w_{k}​$

优化问题为maximize margin，即minimize $max \parallel w_{j}-w_{k}\parallel ^{2}$

##### CC:

将问题转化为一系列二分类问题

##### RAKEL：

将问题转化为多分类问题的集成

每个学习器取包含$k$个随机label的集合，将这个集合的幂集作为新的label，由此将问题转化为多分类单标签问题

对于待预测的输入$x$，将其放入$n$个学习完成的学习器中进行分类，并对每一个label $y_{j}$，计算$\frac{y_{j}\mbox{实际得到的票数}}{y_{j}\mbox{最多能得到的票数}}$，若比值大于0.5，则$y_{j}$为$x$的标签

