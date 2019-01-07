## Multi-Instance Multi-Label Learning

Zhi-Hua Zhou ∗ , Min-Ling Zhang, Sheng-Jun Huang, Yu-Feng Li 

#### Related Work

Roughly speaking, earlier approaches to multi-label learning attempt to **divide multi-label learning to a number of two-class classification problems** or **transform it into a label ranking problem**, while some later approaches try to **exploit the correlation between the labels**.

#### The MIML FrameWork

learning task:  $f: 2^{X}\rightarrow 2^{Y}$ 

data set:	  $\{(X_{1},Y_{1}), (X_{2},Y_{2}), ..., (X_{m},Y_{m})\}$ where $X_{i}\in X$ is a set of instances $\{x_{i1}, x_{i2}, ..., x_{i,n_{i}}\}, x_{ij}\in X$, and $Y_{i}\in Y$ is a set of labels $\{y_{i1}, y_{i2}, ..., y_{i,l_{i}}\}, y_{ij}\in Y$



#### Solving MIML Problem by Degeneration

##### Solution A: Using multi-instance learning as the bridge

learning task: $f_{MIL}: 2^{X}\times Y \rightarrow \{-1,+1\}$   

The proper labels for a new example $X^{*}$ can be determined according to $Y^{*} = \{y|sign[f_{MIL}(X^{*}, y)] = +1\}$ 

##### Solution B: Using multi-label learning as the bridge

learning task: $f_{MLL}: Z \rightarrow 2^{Y}$ 

For any $z_{i} \in Z$, $f_{MLL}(z_{i}) = f_{MIML}(X_{i})$ if $z_{i} = \phi(X_{i}), \phi:2^{X} \rightarrow Z $

The proper labels for a new example $X^{*}$ can be determined according to $Y^{*} = f_{MLL}(\phi(X^{*})) $ 

##### MIMLBOOST (an illustration of Solution A)

transform each example $(X_{u},Y_{u})$ into a set of $|Y|$ number of multi-instance bags $\{[(X_{u}, y_{1}), \Psi(X_{u}, y1)],[(X_{u}, y_{2}), \Psi(X_{u}, y_{2})], · · · , [(X_{u}, y_{|Y|}), \Psi(X_{u}, y_{|Y|})]\} $ 

where $\Psi(X_{u}, y_{v}) \in \{-1, +1\}$ 

Thus, the original data set is transformed into a multi-instance data set
containing $m \times |Y|$ number of bags. 

##### MIMLSVM (an illustration of Solution B)

The basic assumption of MimlSvm is that the spatial distribution of the bags carries **relevant** information, and information helpful for label discrimination can be discovered by measuring the closeness between each bag and the representative bags identified through clustering.  

- Step 1: the $X_{u}$ of each MIML example $(X_{u}, Y_{u}) (u =1, 2, · · · , m)$ is collected and put into a data set $\Gamma$. 

- Step 2: $k$-medoids clustering is performed on $\Gamma$.

- Step 3: the data set $\Gamma$ is divided into $k$ partitions, whose medoids are $M_{t} (t = 1, 2, · · · , k)$, respectively. The original multi-instance example $X_{u}$ is transformed into a $k$-dimensional numerical vector $z_{u}$, where the $i$-th $(i = 1, 2, · · · , k)$ component of $z_{u}$ is the distance between $X_{u}$ and $M_{i}$, that is, $d_{H}(X_{u}, M_{i}) $  

**Medoids**是[数据集](https://en.wikipedia.org/wiki/Data_set)或具有[数据集](https://en.wikipedia.org/wiki/Data_set)的[集群的](https://en.wikipedia.org/wiki/Cluster_analysis)代表性对象，其与集群中所有对象的平均差异最小。(https://en.wikipedia.org/wiki/Medoid)

将multi-instance example转换为到聚类中心点距离的single-instance（第$i$维表示到第$i$个中心点的距离）

Thus, the original MIML examples $(X_{u}, Y_{u}) (u = 1, 2, · · · , m)$ have been transformed into multi-label examples $(z_{u}, Y_{u}) (u = 1, 2, · · · , m) $ 

- Step 4: from the data set a multi-label learning function $f_{MLL}$ can be learned, which
  can accomplish the desired MIML function because $f_{MIML}(X^{∗}) = f_{MLL}(z^{∗})$. 
- Step 5: in making predictions, the TCriterion [11] is used.

##### Five criteria used for evaluating the performance of learning with multi-label examples

- hamming loss
- one-error
- coverage
- ranking loss
- average precision

#### Solving MIML Problems by Regularization: D-MIMLSVM

The degeneration methods may lose information during the degeneration process.

Assumption: all the class labels share some **commonness** 

##### Loss Function

$$V=V_{1}+V_{2}$$

$V_{1}$ considers the loss between the ground-truth label set of each training bag $X_{i}$ 

$V_{2}$ considers the loss between $\boldsymbol{f}(X_{i})$ and the predictions of $X_{i}$’s constituent instances.

##### Regularizer

$$\Omega(\boldsymbol{f})=\frac{1}{T}\sum\limits_{t=1}\limits^{T}||\boldsymbol{w}_{t}||^{2}+\mu ||\boldsymbol{w}_{0}||^{2}$$

##### Regularization framework:

$$\min \limits_{f\in H} \Omega(\boldsymbol{f})+\gamma V$$

#### Solving Single-Instance Multi-Label Problems through MIML Transformation: INSDIF

Transform single-instance multi-label examples into MIML examples to exploit the power of MIML.

##### Basic assumption

The spatial distribution of instances with different labels encodes information helpful for discriminating these labels, and such information will become more explicit by breaking the single instances into a number of instances each corresponds to one label.   

##### Process

- First, transform each example into a bag of instances, by deriving one instance for each class label, in order to explicitly express the ambiguity of the example in the input space.  

- Second, an MIML learner is utilized to learn from the transformed data set.

In the first stage, INSDIF derives a prototype vector $\boldsymbol{v}_{l}$ for each class label $l \in Y$ by averaging all the training instances belonging to $l$, i.e.,  

$$\boldsymbol{v}_{l} =\frac{1}{|S_{l}|}(\sum\limits_{\boldsymbol{x}_{i}\in S_{i}}\boldsymbol{x}_{i})$$  

After obtaining the prototype vectors, each example $\boldsymbol{x}_{i}$ is re-represented by a bag of instances $B_{i}$, where each instance in $B_{i}$ expresses the difference between $\boldsymbol{x}_{i} $ and a prototype vector.  

$$B_{i} = \{\boldsymbol{x}_{i} - \boldsymbol{v}_{l}|l \in Y\} $$

#### Solving Multi-Instance Single-Label Problems through MIML Transformation: SubCod (i.e., SUB-COncept Discovery) 

Transform multi-instance single-label examples into MIML examples
to exploit the power of MIML.

##### Basic Assumption

High-level complicated concepts can be derived by a number of lower-level sub-concepts which are relatively clearer and easier for learning, so that we can transform the single-label into a set of labels each corresponds to one subconcept. 

##### Process

- Transform each single-label example into a multi-label example by discovering and exploiting sub-concepts involved by the original label.  

  This is realized by constructing multiple labels through unsupervised clustering all instances and then treating each cluster as a set of instances of a separate subconcept.

- The outputs learned from the transformed data set are used to derive the original labels that are to be predicted.  

  This is realized by using a supervised learning algorithm to predict the original labels from the sub-concepts predicted by an MIML learner.

In the first stage, a Gaussian mixture model with M mixture components is to be learned from D by the EM algorithm, and the mixture components are regarded as sub-concepts. 

In the second stage, a traditional classifier $f : \{+1, -1\}^{M}\rightarrow Y$ is generated from the data set. This is relatively simple and traditional supervised learning algorithms can be applied.  

#### Summary

Having a good representation is often more important than having a strong learning algorithm because a good representation may capture more meaningful information and make the learning task easier to tackle.  

Since many real objects are inherited with input ambiguity as well as output ambiguity, MIML is more natural and convenient for tasks involving such objects.

- To exploit the advantages of the MIML representation, we propose the MimlBoost algorithm and the MimlSvm algorithm based on a simple degeneration strategy.  
- Considering that the degeneration process may **lose information**, we also propose the D-MimlSvm algorithm which tackles MIML problems directly in a regularization framework. 
- SIML: INSDIF
- MISL: SubCod