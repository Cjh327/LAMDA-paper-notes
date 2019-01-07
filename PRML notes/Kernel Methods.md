## Kernel Methods

$$k(\boldsymbol{x},\boldsymbol{x'})=\phi(\boldsymbol{x})^T\phi(\boldsymbol{x'})$$



核函数：

$$k: \cal{X}\times \cal{X} \rightarrow \Bbb{R} $$

$$\forall x,z\in \cal{X}$$，则称 $k(x,z)$ 为核函数



正定核：

$$k: \cal{X}\times \cal{X} \rightarrow \Bbb{R} $$

$\forall x,z\in \cal{X}$ ，有$k(x,z)$，如果$k(x,z)$满足：

1. 对称性   $k(x,z)=k(z,x)$
2. 正定性  任取$N$个元素， $x_1,x_2,\cdots,x_N\in\cal{X}$ ，对应的Gram Matrix是半正定的

则称$k(x,z)​$为正定核函数 

Gram Matrix $K = [k(x_i,x_j)]$

