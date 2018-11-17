## Semi-Supervised Multi-Modal Learning with Incomplete Modalities 

**Dilemma**: Most of the previous multi-modal methods assume that training examples are with complete modalities. However, due to the failures of data collection, self-deficiencies and other various reasons, multi-modal examples are usually with **incomplete feature representation** in real applications. 

SLIM utilizes the **intrinsic modal consistencies** and **extrinsic unlabeled information** in one unified framework as well as can perform in both transductive and inductive configurations. 

#### The Formulation of SLIM 

SLIM can be decomposed into two targets:

- With the incomplete modal examples, we aim to learn the predictors to **classify** the test instances of each modality accurately 

- We wish to **cluster** the unlabeled instances by modeling a joint transformed matrix factorization problem with respect to each modal similarity matrix and the learned predictions, and pushes them towards a consensus. 

  SLIM can be defined as: 

  $$\min\limits_{W_{k},b_{k},F}\sum\limits_{k=1}\limits^{K}(\hat{L}_{k}(F_{k},F)+\frac{\lambda_{2}}{2}\tilde{L}_{k}(\tilde{X}_{k},F))$$

  $K$: number of modalities

  $\hat{L}_{k}(F_{k},F)$: the loss of classification of the k-th modality 

  $F_{k}, F$: the classification results and the labels of all the instances on $k$-th modality to be learned 

  $\tilde{L}_{k}(\tilde{X}_{k},F))$: considers both the intrinsic and extrinsic information for incomplete modalities. In detail, we treat the **incomplete similarity matrix** of each modal and the **learned predictions** as a transformed matrix factorization problem, and wish to **keep the consistency** between them, $\lambda_{2} > 0$ is a balance parameter.