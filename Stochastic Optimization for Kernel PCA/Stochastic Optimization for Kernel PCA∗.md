## Stochastic Optimization for Kernel PCA∗

*Lijun Zhang and Tianbao Yang and Jinfeng Yi and Rong Jin and Zhi-Hua Zhou*

#### Summary

##### Dilemma

 The application of kernel PCA to large scale problems remains a big challenge, due to its quadratic space complexity and cubic time complexity in the number of examples.  

##### Method

We utilize techniques from stochastic optimization to solve kernel PCA with linear space and time complexities per iteration.   

kernel PCA, a non-linear extension of PCA

The key idea is to map the data into a kernel-induced Hilbert space, where dot
product between points can be computed efficiently through the kernel evaluation. 