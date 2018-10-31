## Feature Learning based Deep Supervised Hashing with Pairwise Labels

Wu-Jun Li, Sheng Wang and Wang-Cheng Kang   
*National Key Laboratory for Novel Software Technology   
Department of Computer Science and Technology, Nanjing University, China* 

#### deep pairwise-supervised hashing (DPSH)   

Three key components:   
- a deep neural network to learn image representation from pixels  
- a hash function to map the learned image representation to hash codes  
- a loss function to measure the quality of hash codes guided by the pairwise labels  

#### Feature Learning Part

a 7-layer CNN: 5 convolutiona  layers (conv 1-5) and 2 fully-connected layers (full 6-7)

#### Objective Function Part

Given the binary codes $B=\{\boldsymbol{b}_i\}^{n}_{i=1}$ for all the points, we can define the likelihood of the pairwise labels $S={s_{ij}}$ as that of LFH:

$\begin{equation}p(s_{ij}|B) =\begin{cases}\sigma(\Omega_{ij}), & s_{ij}=1 \\ 1- \sigma(\Omega_{ij}), & s_{ij}=0\end{cases}\end{equation}$

where $\Omega_{ij}=\frac{1}{2}\boldsymbol{b}^{T}_{i}\boldsymbol{b}_{j}$ and $\sigma(\Omega_{ij})=\frac{1}{1+e^{-\Omega_{ij}}}$. Note that $\boldsymbol{b}_{i} \in \{-1,1\}^{T}$

Optimization problem:

min_B  $J_{1}$ = $-$ log $p(S|B)$ = $-\Sigma_{s_{i,j}\in S}$ log $p(s_{ij}|B)$

The above optimization problem can make the Hamming distance between two similar points as small as possible, and simultaneously make the Hamming distance between two dissimilar points as large as possible. 

However, the problem is discrete and hard to solve. By relaxing $\{\boldsymbol{b}_{i}\}$ from discrete to continuous, the final regularized form of the problem:

min_B_U $J_{3}=-\Sigma_{s_{ij}\in S}(s_{ij}\Theta_{ij}-$log $(1+e^{\Theta_{ij}}))$

$\begin{equation} s.t.\quad \boldsymbol{u}_{i}  =\boldsymbol{b}_{i}, \forall i=1,2,\cdots, n\\ \boldsymbol{u}_{i}\in \Bbb{R}^{c\times 1} \forall i = 1,2,\cdots,n\\ \boldsymbol{b}_{i}\in \{-1,1\}^{c},\forall i=1,2,\cdots, n\end{equation}$

 

#### DPSH Model

$\boldsymbol{u}_{i} = \boldsymbol{W}^{T}\phi(\boldsymbol{x}_{i};\theta) + \boldsymbol{v}$

$\theta$ denotes all the parameters of the 7 layers

$\phi(\boldsymbol{x}_{i};\theta)$ denotes the output of the full7 layer associated with $\boldsymbol{x}_{i}$

$\boldsymbol{W}\in \Bbb{R}^{4096\times c}$ denotes a weight matrix

$v \in \Bbb{R}^{c\times 1}$ is a bias vector

It means that we connect the feature learning part and the objective function part by a fully-connected layer. 