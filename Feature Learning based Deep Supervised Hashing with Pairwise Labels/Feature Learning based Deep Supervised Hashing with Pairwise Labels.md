## Feature Learning based Deep Supervised Hashing with Pairwise Labels

Wu-Jun Li, Sheng Wang and Wang-Cheng Kang   
​	*National Key Laboratory for Novel Software Technology*   
​	*Department of Computer Science and Technology, Nanjing University, China*  

#### Annotation

In machine learning，**feature hashing**, also known as the **hashing trick** (by analogy to the kernel trick), is a fast and space-efficient way of vectorizing features, i.e. turning arbitrary features into indices in a vector or matrix. It works by applying a hash function to the features and using their hash values as indices directly, rather than looking the indices up in an associative array.   

dimensionally reduction

#### deep pairwise-supervised hashing (DPSH)   

Three key components:   
- a deep neural network to learn image representation from pixels $\phi(\boldsymbol{x}_{i}; \theta)$  
- a hash function to map the learned image representation to hash codes  $sgn(\boldsymbol{W}^{T} \phi(\boldsymbol{x}_{i}; \theta) + \boldsymbol{v})$
- a loss function to measure the quality of hash codes guided by the pairwise labels  $J$

#### Feature Learning Part

a 7-layer CNN: 5 convolutional  layers (conv 1-5) and 2 fully-connected layers (full 6-7)

#### Objective Function Part

Given the binary codes $B=\{\boldsymbol{b}_i\}^{n}_{i=1}$ for all the points, we can define the likelihood of the pairwise labels $S={s_{ij}}$ as that of LFH:   

$\begin{equation}p(s_{ij}|B) =\begin{cases}\sigma(\Omega_{ij}), & s_{ij}=1 \\ 1- \sigma(\Omega_{ij}), & s_{ij}=0\end{cases}\end{equation}$  

where $\Omega_{ij}=\frac{1}{2}\boldsymbol{b}^{T}_{i}\boldsymbol{b}_{j}$ and $\sigma(\Omega_{ij})=\frac{1}{1+e^{-\Omega_{ij}}}$. Note that $\boldsymbol{b}_{i} \in \{-1,1\}^{T}$  

Optimization problem:  

$\min \limits_{B}  J_{1}$ = $-$ log $p(S|B)$ = $-\Sigma_{s_{i,j}\in S}$ log $p(s_{ij}|B)$   

The above optimization problem can make the Hamming distance between two similar points as small as possible, and simultaneously make the Hamming distance between two dissimilar points as large as possible.  

However, the problem is discrete and hard to solve. By relaxing $\{\boldsymbol{b}_{i}\}$ from discrete to continuous, we reformulate the problem as the following equivalent one:  

$\min \limits_{B,U}J_{2}=-\Sigma_{s_{ij}\in S}(s_{ij}\Theta_{ij}-$log $(1+e^{\Theta_{ij}}))$

$\begin{equation} s.t.\quad \boldsymbol{u}_{i}  =\boldsymbol{b}_{i}, \forall i=1,2,\cdots, n\\ \boldsymbol{u}_{i}\in \Bbb{R}^{c\times 1} \forall i = 1,2,\cdots,n\\ \boldsymbol{b}_{i}\in \{-1,1\}^{c},\forall i=1,2,\cdots, n\end{equation}$

where $\Theta_{ij}=\frac{1}{2}\boldsymbol{u}_{i}^{T}\boldsymbol{u}_{j}$ and $U=\{\boldsymbol{u}_{i}\}^{n}_{i=1}$

move the equality constraints to the regularization terms:

$\min \limits_{B,U} J_{3}=-\Sigma_{s_{ij}\in S}(s_{ij}\Theta_{ij}-$log $(1+e^{\Theta_{ij}}))+\eta \Sigma^{n}_{i=1}||\boldsymbol{b}_{i}-\boldsymbol{u}_{i}||^{2}_{2}$

where $\eta$ is the regularization term (hyper-parameter)

#### DPSH Model

$\boldsymbol{u}_{i} = \boldsymbol{W}^{T}\phi(\boldsymbol{x}_{i};\theta) + \boldsymbol{v}$

$\theta$ denotes all the parameters of the 7 layers

$\phi(\boldsymbol{x}_{i};\theta)$ denotes the output of the full7 layer associated with $\boldsymbol{x}_{i}$

$\boldsymbol{W}\in \Bbb{R}^{4096\times c}$ denotes a weight matrix

$v \in \Bbb{R}^{c\times 1}$ is a bias vector

It means that we connect the feature learning part and the objective function part by a fully-connected layer. 

The problem for learning becomes:

$\min \limits_{B,\boldsymbol{W},\boldsymbol{v},\theta} J=-\Sigma_{s_{ij}\in S}(s_{ij}\Theta_{ij}-$log $(1+e^{\Theta_{ij}}))$

$+\eta \Sigma^{n}_{i=1}||\boldsymbol{b}_{i}-(\boldsymbol{W}^{T}\phi(\boldsymbol{x}_{i};\theta) + \boldsymbol{v})||^{2}_{2}$

#### Learning

minibatch-based strategy  

In each iteration we sample a minibatch of points from the whole training set, and then perform learning based on these sampled points.  
​	We optimize one parameter with other parameters fixed.  
​	The $\boldsymbol{b}_{i}$ can be directly optimized as follows:  
​	$\boldsymbol{b}_{i} = sgn(\boldsymbol{u}_{i}) = sgn(\boldsymbol{W}^{T} \phi(\boldsymbol{x}_{i}; \theta) + \boldsymbol{v})$

For the other parameters $\boldsymbol{W}$, $\boldsymbol{v}$ and $\theta$, we use backpropagation (BP) for learning.  

#### Out-of-Sample Extension

For any point $\boldsymbol{x}_{q}  \notin X$ , we can predict its hash code just by forward propagation:  
​	$$\boldsymbol{b}_{q} = h(\boldsymbol{x}_{q}) = sgn(\boldsymbol{W}^{T}\phi(\boldsymbol{x}_{q};\theta) + \boldsymbol{v})$$

#### Algorithm

Learning algorithm for DPSH.  
​	**Input:  **  
​		Training images $X = \{\boldsymbol{x}_{i}\}^{n}_{ i=1}$ and a set of pairwise labels $S = \{s_{ij}\}$.  
​	**Output:  **  
​		The parameters $\boldsymbol{W}$,$\boldsymbol{ v}$, $\theta$ and $B$.  
​	**Initialization**: Initialize $\theta$ with the CNN-F model; Initialize each entry of $\boldsymbol{W}$ and $\boldsymbol{v}$ by randomly sampling from a Gaussian distribution with mean $0$ and variance $0.01$.  
​	**REPEAT  **  
​		Randomly sample a minibatch of points from $X$, and for each sampled point $\boldsymbol{x}_{i}$, perform the following operations:  

- Calculate $\phi(\boldsymbol{x}_{i}; \theta)$ by forward propagation;
- Compute $\boldsymbol{u}_{i} = \boldsymbol{W}^{T} \phi(\boldsymbol{x}_{i}; θ) + \boldsymbol{v}$;
- Compute the binary code of $\boldsymbol{x}_{i}$ with $\boldsymbol{b}_{i} = sgn(\boldsymbol{u}_{i})$.  
- Compute derivatives for point $\boldsymbol{x}_{i}$ 
- Update the parameters $\boldsymbol{W}$; $\boldsymbol{v}$;  $\theta$  by utilizing back propagation;

**UNTIL** a fixed number of iterations  

