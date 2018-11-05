## Online game props recommendation with real assessments

*De-Chuan Zhan· Jun Tang · Zhi-Hua Zhou*

#### Four Problems

##### Complicated Dependency on Context (CDC) 

Game props are not only dependent on the purchase activities of players but also heavily relevant to the elaborated game contexts. Props can be dependent on lots of features, and even worse, player intentions for buying certain props may depend on the game events which are not directly related to the purchase activities. These kinds of complicated contexts can be neither well captured by CF nor easily measured in CBR with ordinary similarity functions.

##### Long-Distance Intervention (LDI)

Player purchasing game props can be affected by events occurred long ago 

##### Props priority-Role Dependency (P-RD) 

There are lots of props in a certain game, while different types of characters 

##### Concept Variation (CV) 

The players may insist to obtain new props by playing games instead of purchasing 



#### Multi-instance multi-label representation

We define the prediction of single instance on prop $j$ as: 

$$f_{j}(\{x\}) = \max\limits_{l=1,\cdots,K}\boldsymbol{w}^{T}_{j,l_{j}}W^{T}_{0}\boldsymbol{x}$$

where $\boldsymbol{w}_{j}$, $l_{j}$ corresponds to the $l_{j}$-th sub-concept of purchase intention for prop $j$, $l_{j} = 1, 2, \cdots , K$ , i.e., with overall considerations around the events and event features, the intension of buying prop j may be related to one particular feature combination of one event which is of paramount importance. The operator $\max(·)$ introduces non-linearities for the prediction function. 

#### Ranking the multiple labels 

Ranking orders among multiple labels should be emphasized during the MIML learning procedure. 

Minimize the ranking error:

For a bag $\boldsymbol{X}_{i}$ and one of its relevant labels, i.e., $\{y_{ij}| y_{ij} =1\}$, we define a ranking risk function:  
​	$$R(\boldsymbol{X}_{i}, y_{ij}) =\sum\limits_{k:y_{ik}=0}I[f_{j}(\boldsymbol{X}_{i})] $$   
​	The Equation counts how many undesired props are ranked before prop j desired by
the i-th game player.   

The ranking error of $\boldsymbol{X}_{i}$ on label $y_{i}$ j can be defined as:

$$err_{rank}(\boldsymbol{X}_{i}, y_{ij}) =\sum\limits_{i=1}\limits^{R(\boldsymbol{X}_{i},y_{ij})}\alpha_{i}$$

#### Concept variations 

##### Prior weighting solution: We-MIML 

MIML prediction functions trained months ago cannot predict purchase intentions at present accurately.  

We first calculate the most recent “class priors” in a time window, and use the temporary class priors to “weight” the base learner described in the previous section.  

##### Sparse prediction solution: Sp-MIML 

##### Co-training style solution: Co-MIML 

Assume that the un-purchased props should be unlabeled rather than negative labeled.

The whole virtual props recommendation problem can be casted into a weak label problem. 

#### Summary

In this paper, we systematically analyze the **specific natures of game props recommendation** for the first time, and attribute the problems into four aspects: **the complicated dependencies on contexts**, **long-distance interventions**, **props priority-role dependencies**, and **concept variations**.

Methods:  

- CDC  MIML learning framework
- LDI   MIML learning framework
- PRD  Minimize the ranking error
- CV     modify the basic solution into three variants : We/Sp/Co-MIML

The first two issues are mainly about **how to take advantages of the given information (inputs) in the phone game props recommendation**, while the last two issues are towards
the **desired properties of outputs**. 

We deal with game prop recommendation under the **multi-instance multi-label learning** framework directly against the complicated dependencies and long-distance interventions, and **minimize the ranking error** to meet the requirements of the props priority-role dependencies. 

To address concept variations, we proposed three variants of MIML approaches, i.e.,**We/Sp/Co-MIML**, which consider the class prior weighting, sparse prediction, and co-training factors in MIML framework.