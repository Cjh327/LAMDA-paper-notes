## Semi-Supervised Document Retrieval

*Ming Li, Hang Li, Zhi-Hua Zhou*  
​	*National Key Laboratory for Novel Software Technology*  
​	*Nanjing University, Nanjing 210093, China * 
​	*Microsoft Research Asia, 49 Zhichun Road, Beijing 100080, China*  

Document retrieval is in nature a ranking problem 

One key idea in semi-supervised learning is to label unlabeled data using certain techniques and thus increase the amount of labeled training data. 

In learning for ranking, one needs to learn a model that can map instances to ordered categories. 

In this paper we consider the case in which for each query in the training data only a small number of documents (instances) associated with it are labeled and the remaining documents (instances) are unlabeled. 

##### Algorithm:  SSRank

**Input**: 	labeled instance set $L$, unlabeled instance set $U$, combining strategy $C$
​			conventional document retrieval method: $IR$
​			machine learning method for ranking: $ML$

**Process**:  
​		Construct $f^{(i)}$ using $IR$  
​		Calculate the scores of the instances w.r.t each query $q$ using $^{(i)}$   
​		Calculate the probabilities of all the ranks in $Y$ for each instance  
​		Assign scores to the unlabeled instances in $U$   
​		$t\leftarrow 1$  
​		Learn a ranking function $f^{(l)}$ from $L: f^{(l)}\leftarrow ML(L)$  
​		**Repeat Until** $f^{(l)}$ doesn't change  
​			Calculate the scores of the instances w.r.t each query $q$ using $f^{(l)}$     
​			Calculate the probabilities of all the ranks in $Y$ for each instance  
​			Assign scores to the unlabeled instances in $U$     
​			Combine the scores from $f^{(l)}$ and $f^{(i)}$ using $C$ to label unlabeled instances.  
​			Construct $L'$ using newly labeled instances
​			Calculate the number of newly labeled pairs $m_{t}$ and estimate the error rate $\hat{e}_{t}$  
​			Learn a ranking function from $L\cup L'$: $f^{(l)}\leftarrow ML(L\cup L')$   
​			$t \leftarrow t+1$

**Output**: the learned ranking function $f^{(l)}$

#### Summary

This paper addresses the issue of ranking model construction in document retrieval, particularly when there are only a small amount of labeled data available. The paper proposes a semi-supervised learning method SSRank for performing the task. It leverages the uses of both labeled data and unlabeled data, utilizes views from both conventional IR and supervised learning to conduct data labeling, and relies on a criterion to control the process of data labeling. 