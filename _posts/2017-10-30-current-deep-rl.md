---
title: Where does current deep RL stand?
---

![simulations are rewarding but can be far from reality](/images/sim_class.jpg) 

Recent advances have certainly highlighted what can be possibly be achieved with current state of the art with deep RL. However, bigger questions remain as the progress has come with various assumptions (consequently the limitations) which the methods often do not convey explicitly. Some of the (obvious and not so obvious) limitations that the current deep RL is riddled with are explained in detail below: 

## Very obvious
---

**Exploration:**

One of the primary reasons why RL has been extremely finicky and tricky to get to work is the exponentially growing search space that an RL algorithm must explore in pursuit of finding the actions that lead to high expected rewards. This, however, scales exponentially as the dimensions of the state and action space increase. An obvious solution is to have multiple workers doing explorations in parallel but at some point even that starts to hit a fundamental limit due to the curse of dimensionality. Such kind of brute-force search isn’t ideal and feasible often in many cases. In real world, where a robot is interacting with the environment, it is at times costly or impossible to carry out exploration at a scale needed for many RL algorithms. Often in simulations, one can run the world faster than real-time but it is not possible to run the real world faster than real-time. Even the choice of having multiple workers starts to get tricky because robots are costly and maintaining them to work non-stop without any damage or provide repeatable motion is extremely hard over long periods of time. 

**Sensitivity to various hyper-parameters**

Since RL requires a lot of exploration especially in the early phases where the agent is trying out random actions to figure out which actions are rewarding and help it achieve a particular goal, the random seeds used in the code can staggeringly affect the algorithm, its convergence and learning. Moreover, various other hyper-parameters including the epsilon (for epsilon greedy) and the gamma (discount factor) also affect in unexpected ways to the overall performance of the algorithm.

**Generalisation issues**

In most RL algorithms training and testing happens on the same environment. This is in stark contrast to most supervised learning methods where an explicit held-out test dataset is maintained to gauge the performance of the learnt model on relatively different distribution of data. Therefore, in RL, the agent is most often incentivised to master a particular skill needed for a given environment rather generalise across different environments or slightly different variations of environments it was trained on. It isn’t clear when it became socially acceptable in RL to train and test on the same dataset. 

**Only works for small time horizons**

Using a fixed gamma, the discount factor, already limits the number of time steps in future that can be affected by the current action. For instance, using a discount factor of 0.99 means that the current action can only affect the next 100 time steps  (geometric progression) and therefore, it cannot solve long time horizon tasks, particularly that require planning for long time. 

Sparse rewards very difficult to train

Consider training with policy gradients where the reward is only obtained at the end of the episode. Since each action’s log-likelihood is scaled by the reward to go (the Q value or the Advantage function) it is zero for those cases where there is no reward and therefore, very difficult to train. Because the gradient is zero it is impossible for the algorithm to get any signal for that move. Most ATARI environments provide fairly dense reward and hence it has been possible to train with standard DQN and policy gradients.

## Not so obvious
---

**Forgetting in self-play**

Self-play has been a powerful technique to enable learning of very complicated skills. It sits on top of the underlying RL algorithm. One would assume that if the rewards are reversed for agents and that they start competing against each other it will naturally lead to progressively increasing skills. But there is a problem: RL algorithms trained with policy gradients in sparsely-rewarded environments have a tendency to forget what they learnt and may end up learning to exploit each other’s skills akin to the mode-collapse problem in GANs. In a recent paper from OpenAI, the training was done on randomly sampled historic copy of the agent to add regularisation to the learning. 

**Throwing away the negative data**

Trajectories that lead to negative reward or an undesired states are, as training progresses, made less probable. However, even if the agent doesn’t reach the goal, the intermediate states it reaches, though undesirable for a particular goal, can be harnessed positively to achieve the goal of reaching that particular state in future i.e. most of the learning focusses on achieving only a particular goal and not on learning the model or build up a topological memory of the environment to speed up the learning process in future.

**Only maximises the reward with no safety constraints**

The objective function only focusses on the maximisation of the overall reward function without constraining the learnt policies in some way that are aligned with the value function of humans or safety constraints that allow to it operate in natural human environments without any catastrophic effects. 

**Limited to simulations environments**

Because a simulator allows rendering at super high frame-rates and that the renderings can be parallelised over a large number of workers, simulated environments have greatly accelerated the progress of deep RL. However, because deep RL currently is very much dependent on simulated environments, it has been difficult to try on tasks which cannot be simulated easily e.g. folding a cloth. Whatever we cannot simulate, we cannot accomplish. Even the recent attempts at sim2real have mostly focussed on domain randomisation for possible transfer of those simulated environments to real world: randomising textures and camera positions as well as shapes of objects. However, domain randomisation grows exponentially as the number of objects increases as well as when the horizon of the task goes beyond a limit.