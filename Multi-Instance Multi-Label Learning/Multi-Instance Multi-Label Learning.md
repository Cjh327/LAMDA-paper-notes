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

transform each example $(X_{u},Y_{u})$ into a set of $|Y|$ number of multi-instance bags $\{[(X_{u}, y_{1}), \Psi(X_{u}, y1)],[(X_{u}, y_{2}), \Psi(X_{u}, y_{2})], · · · , [(X_{u}, y_{|Y|}), \Psi(X_{u}, y_{|Y|})]\} $ $\psi(X_{u}, y_{v}) \in \{-1, +1\}$ 

Thus, the original data set is transformed into a multi-instance data set
containing $m \times |Y|$ number of bags. 

##### MIMLSVM (an illustration of Solution B)

The basic assumption of MimlSvm is that the spatial distribution of the bags carries **relevant** information, and information helpful for label discrimination can be discovered by measuring the closeness between each bag and the representative bags identified through clustering.  

- Step 1: the Xu of each MIML example $(X_{u}, Y_{u}) (u =1, 2, · · · , m)$ is collected and put into a data set $\Gamma$. 

- Step 2: $k$-medoids clustering is performed on $\Gamma$.

- Step 3: the data set $\Gamma$ is divided into $k$ partitions, whose medoids are $M_{t} (t = 1, 2, · · · , k)$, respectively. The original multi-instance example $X_{u}$ is transformed into a $k$-dimensional numerical vector $z_{u}$, where the $i$-th $(i = 1, 2, · · · , k)$ component of $z_{u}$ is the distance between $X_{u}$ and $M_{i}$, that is, $d_{H}(X_{u}, M_{i}) $  

**Medoids**是[数据集](https://en.wikipedia.org/wiki/Data_set)或具有[数据集](https://en.wikipedia.org/wiki/Data_set)的[集群的](https://en.wikipedia.org/wiki/Cluster_analysis)代表性对象，其与集群中所有对象的平均差异最小。(https://en.wikipedia.org/wiki/Medoid)

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

#### Solving MIML Problems by Regularization







