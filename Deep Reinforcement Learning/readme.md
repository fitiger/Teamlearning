# Team learning for reinforcement learning

## What is Reinforcement Learning

![overview](Img/rl-idea.png)

Problems involving an agent interacting with an environment, which provides numeric reward
signals.  
Goal: Learn how to take actions
in order to maximize reward.

![eg](Img/cart-pole-eg.png)

### Difference with supervised learning

- Data are not i.i.d. insead, a correlated time series data
- The learner is not told which actions to take, but instead must discover which actions yield the most reward by exploring
- No instant feedback or label for correct action
- Upper bound for supervised learning is human-performance but reinforcement learning is unknown

### Features of reinforcement learning

- need to explore new actions
- delayed reward
- sequential input data
- agent's actions affect the subsequent data it receives.

Deep Reinforcement Learning：do not need features engineering and use end-to-end training.  
