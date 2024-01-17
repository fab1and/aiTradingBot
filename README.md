## Introduction to the A2C algorithm.

The Actor-to-Critic (A2C) algorithm is an optimization of traditional algorithms, as the A2C algorithm takes the current level of values into account for updating it´s parameters.

The algorithm belongs to the asynchronous methods for deep reinforcement learning and was first proposed by Mnih et. al in 2016 [1].

According to the A2C logic the value of an action (the Q value) does not only depend on how good the action is, but of how better it can be. Or in other words the value of the current action taken does not only depend on it´s overall value but more on the relative value, relative to the current level of possible rewards in the given state. 

To account for this fact the A2C algorithms additionally ads an additional term which "punishes" the observed return by subtracting a baseline, so that the agent is able to distinguish between good returns and returns which are below the baseline. This is possible due to the relation:

$$\mathbb{E}_{a_t \sim \pi_{\theta}}{\nabla_{\theta} \log \pi_{\theta}(a_t|s_t) b(s_t)} = 0.$$

Therefore only the information which yields to high returns will be used in the model. Another advantage is the reduction of the variance such that the output is more stable. 

## Derivation of the method´s logic
Without the A2C, e. g. general Q-learning, the update step of the parameters can be written as:


$$
\boldsymbol{\theta}_{\pi} \leftarrow \boldsymbol{\theta}_{\pi} + \eta G_t \frac{\nabla \pi_{\boldsymbol{\theta}_{\pi}}(A_t | S_t)}{\pi_{\boldsymbol{\theta}_{\pi}}(A_t | S_t)}
$$

While with the A2C Algorithm we introduce a baseline $b(s)$ which tells us how good the current action is compared to the overall state value:


$$
\boldsymbol{\theta}_{\pi} \leftarrow \boldsymbol{\theta}_{\pi} + \eta G_t -b(s)\frac{\nabla \pi_{\boldsymbol{\theta}_{\pi}}(A_t | S_t)}{\pi_{\boldsymbol{\theta}_{\pi}}(A_t | S_t)}
$$

With a simple replacment of  $G_t$ with $R_{t+1} +v(s')$ we can represent the method as Temporal Difference learning (TD).

But what is the purpose for using the baseline? One reason is that it tells us  how much better the action value can be. Let´s look at an simple example of how that works:
