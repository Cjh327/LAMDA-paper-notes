## Towards Sample Efficient Reinforcement Learning∗

**Yang Yu*  
​	*National Key Laboratory for Novel Software Technology, Nanjing University, Nanjing 210023, China*  



- Considering the **exploration-learning** procedure, how to efficiently **explore** the environment and how to better **optimize** the policy; 

- Considering the **environment**, how to **learn** the environment model;

- Considering **multiple environments**, how to **reuse** and **transfer** experiences across environments; 

- And more essentially, how to **abstract** states and actions. 

#### Exploration

In an unknown environment, the agent needs to visit states that have not been visited in order to collect better trajectory data. The agent cannot follow its current policy tightly, which
has been learned from the previous data and may only lead to follow the previous paths. Exploration strategies are usually employed to encourage veering off the previous paths.  

##### Parameter space noise   

##### Curiosity-driven exploration   

The agent may repeatedly try a bad path many times, since it does not know if the path has been explored before. The current general reinforcement learning algorithms require a lot of samples — find a good path by luck. 

**Curiosity-driven exploration**: The agent records the counts of the visits of every states and actions.  According to the counts, an intrinsic reward is added to the environment reward to encourage visiting states that are less visited. 

#### Optimization

After the exploration step that collects interaction data from the environment, the learning step updates the model of policy or value function from the data.  

Introduce several optimization methods.

#### Environment Modeling

contains:

- A transition function, telling how the state will change after taken an action 
- A reward function, telling how a transition would be rewarded  

Unfortunately, such supervised learning approach works well only in discrete or small state space, but rarely works for large/high-dimensional cases. 

#### Experience Transfer 

An agent can learn more efficiently in a task if experiences are available.  

Introduce some recent progress in transfer reinforcement learning.

#### Abstraction 

We believe abstraction is in the core of the sample efficiency issue. 

- Hierarchical reinforcement learning 
- Neural network with symbols 

#### Summary

##### Dilemma

Current reinforcement learning techniques are still suffer from **requiring a huge amount of interaction data**, which could result in **unbearable cost** in real world applications. 

Current reinforcement learning techniques is the **low sample efficiency**,  which causes a huge amount of interactions with the
environment 

##### Method

Discuss possible ways to **alleviate the sample cost** of reinforcement learning, from the aspects of **exploration**, **optimization**, **environment modeling**, **experience transfer**, and **abstraction**. 