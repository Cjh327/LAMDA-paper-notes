## Mining extremely small data sets with application to software reuse

Yuan Jiang, Ming Li and Zhi-Hua Zhou∗, †
​	National Key Laboratory for Novel Software Technology, Nanjing University,
​	Nanjing 210093, China 

#### Introduction

In general, if a data set cannot fully cover the whole variable space, then the data set is referred as
*a small data set*. 



#### The RF2Tree Algorithm

```
Input: training set S, decision tree algorithm L
Output: decision tree DT
Process:
	F* = RandomForests(S, L)
		/* train a random forest F∗ from S via RandomForests */
	S' = GenVirExp(F*)
		/* use the random forest to generate virtual examples as more as possible */
	DT = L(S∪S')
		/* grow a decision tree from the enlarged training data set */ 	
```

#### Justification

* $F: X\rightarrow  Y$: target function

* $P_{F_{E}} =P_{F=F_{E}} =1-P_{F\neq F_{E}} =1-err_{E} $: the probability for $F_{E}$ to approach $F $
* * $F_{E}$: the function implemented by a random forest ensemble trained from a given training set
  *  $err_{E}$: the error rate of the ensemble. 

* $P_{F_{T}} =P_{F=F_{T}} =1-P_{F\neq F_{T}} =1-err_{T} $: the probability for $F_{T}$ to approach $F $
* * $F_{T}$: the function implemented by a decision tree trained from a given training set. 
  * $err_{T} =err^{(c)}_{T} +err^{(n)}_{T} +err^{(s)}_{T} $: the error rate of the tree
  * * $err^{(c)}_{T}$: 决策树模型的固有误差   
    * $err^{(n)}_{T}$: 数据噪声带来的误差
    * $err^{(s)}_{T} $: 数据集小带来的误差

* $P_{F^{*}_{T}}=P_{F=F^{*}_{T}}=P_{F_{E}}P_{F^{(c)}_{T}}=(1-err_{E})(1-err^{c}_{T})$: the probability for $F^{*}_{T}$ to approach $F$
* * $F^{*}_{T}$: the function implemented by a decision tree that grows from the training set processed by an ensemble in the way of the RF2Tree.  

* $P_{F^{*}_{T}} > P_{F_{T}}$ if $err_{E} < \frac{err_{T}-err^{(c)}_{T}}{1-err^{(c)}_{T}}$

* Thus, using a random forest ensemble to process the original extremely small training set in the way as the RF2Tree can benefit the construction of the decision tree, even when the original training set contains no noise, given that the ensemble is significantly more accurate than the single decision tree grown directly from the original training set. 

#### Verification

conduct experiments

Note that the RandomForests is an ensemble whose comprehensibility is poor. If we only want to get a high predictive accuracy, the RandomForests may be sufficient; but if we want to study which factor is important (this is our purpose), RandomForests could not help as it is a black-box model, while the RF2Tree is more helpful for this purpose. 

#### Mining Practice

Software reuse  experiment result analysis and some empirical analysis 

