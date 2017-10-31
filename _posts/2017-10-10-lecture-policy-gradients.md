---
title: Lecture on Policy Gradients
---

$$\underbrace{p_{\theta}(s_1, a_1, ...., s_T, a_T)}_{\pi_{\theta}(\tau)} = p(s_1) \prod_{t=1}^{T} \pi_{\theta}(a_t | s_t) p(s_{t+1}| s_t, a_t)$$

$$\theta^{*} = \operatorname{argmax}_{\theta}E_{\tau \sim p_{\theta}(\tau)} \bigg[\sum_{t} r(s_t, a_t) \bigg]$$


$$\theta^{*} = \operatorname{argmax}_{\theta}\underbrace{E_{\tau \sim p_{\theta}(\tau)} \bigg[\sum_{t} r(s_t, a_t) \bigg]}_{J(\theta)}$$

$$J(\theta) = E_{\tau \sim p_{\theta}(\tau)} \bigg[\sum_{t} r(s_t, a_t) \bigg] \approx \frac{1}{N} \sum_{i} \sum_{t} r(s_{i,t}, a_{i,t})$$

---

**Optimising the policy** 

Let us denote $$r(\tau) = \sum_{t=1}^{T} r(s_t, a_t)$$ and therefore, we can rewrite $$J(\theta)$$ as

$$J(\theta) = E_{\tau \sim \pi_{\theta}(\tau)}[r(\tau)] = \int \pi_{\theta}(\tau) r(\tau) d\tau$$

Our goal is to maximise the expected reward. Therefore, differentiating this function yields 

$$\nabla_{\theta} J(\theta) = \int \nabla_{\theta} \pi_{\theta}(\tau) r(\tau) d\tau$$

A convenient identity to use here is that 

$$\pi_{\theta}(\tau) \nabla_{\theta}\log \pi_{\theta}(\tau) = \nabla_{\theta}\pi_{\theta}(\tau)$$

Therefore, the overall gradient becomes 

$$\nabla_{\theta} J(\theta) = E_{\tau \sim \pi_{\theta}(\tau)}[\nabla_{\theta}\log \pi_{\theta}(\tau) r(\tau)]$$

---

The gradient tries to:

- increase probability of paths with positive reward.
- decrease probability of paths with negative reward.

Let us assume that the reward is always positive _i.e._ r > 0 this will lead to increased probability of all paths. This isn't exactly what we want. Therefore, we need a baseline to subtract to get an overall relative reward. In [Williams 92] it is shown that the baseline does not change the overall objective we are maximising.

$$E_{\tau \sim \pi_{\theta}(\tau)}[\nabla_{\theta}\log \pi_{\theta}(\tau) b] = \sum_{\tau} \nabla_{\theta} \pi_{\theta}(\tau) b$$

$$\sum_{\tau} \nabla_{\theta} \pi_{\theta}(\tau) b = \nabla_{\theta}\sum_{\tau} ( \pi_{\theta}(\tau) b)$$

$$\sum_{\tau} \nabla_{\theta} \pi_{\theta}(\tau) b = \nabla_{\theta}\sum_{\tau} ( \pi_{\theta}(\tau) b) = \nabla_{\theta}(b) = 0$$

$$\implies \nabla_{\theta} E_{\tau \sim \pi_{\theta}(\tau)}[r(\tau)] = \nabla_{\theta} E_{\tau \sim \pi_{\theta}(\tau)}[r(\tau)-b]$$

Therefore, subtracting a baseline is unbiased in expectation. What possible choices of baseline can we consider? 

**Constant baseline**

$$b=E[r(\tau)] \approx \frac{1}{m} \sum_{i=1}^m r(\tau^{i})$$


**Baseline that minimises the variance**

Remember that $$Var[x] = E[x^2] - E[x]^2$$

$$ \nabla_{\theta}J(\theta) = E_{\tau \sim \pi_{\theta}(\tau)}[\nabla_{\theta} \log \pi_{\theta}(\tau) (r(\tau)-b)]$$

We would like to optimise over b which minimises the variance of $$\nabla_{\theta}J(\theta)$$

Let us denote $$g(\tau) = \log \pi_{\theta}(\tau)$$

$$Var = E_{\tau \sim \pi_{\theta}(\tau)}[(\nabla_{\theta} \log \pi_{\theta}(\tau) (r(\tau)-b))^2] - E_{\tau \sim \pi_{\theta}(\tau)}[\nabla_{\theta} \log \pi_{\theta}(\tau) (r(\tau)-b)]^2$$ 

$$\frac{dVar}{db} = \frac{d}{db}E[g(\tau)^2(r(\tau)-b)^2]$$

Remember that 

$$\nabla_{\theta} E_{\tau \sim \pi_{\theta}(\tau)}[r(\tau)] = \nabla_{\theta} E_{\tau \sim \pi_{\theta}(\tau)}[r(\tau)-b]$$ 

The derivative of the second bit is therefore zero.

$$\frac{d}{db} (E[g(\tau)^2r(\tau)^2] - 2E[g(\tau)^2 r(\tau) b] + b^2 E[g(\tau)^2]) = 0$$

$$\implies -2 E[g(\tau)^2 r(\tau)] + 2b E[g(\tau)^2] = 0$$

This yields 

$$b = \frac{E[g(\tau)^2 r(\tau)]}{E[g(\tau)^2]}$$

**Time-varying baseline**

$$b_t =\frac{1}{m} \sum_{i=1}^m \sum_{k=t}^{H-1} r(s_{k}^{i}, a_{k}^{i})$$

**Value function baseline that depends on the state**

$$b(s_t) = V^{\pi}(s_t)$$

Increase the log probability of actions proportional to how much its returns are better than the expected return under the current policy.

but **how do we estimate $$V^{\pi}$$?**

We could do roll-outs with the current policy and then collect the rewards to go and regress $$V^{\pi}$$ as 

$$\phi_{i+1} = \operatorname{argmin}_{\phi} \frac{1}{m} \sum_{i=1}^{m} \sum_{t=0}^{H-1} \bigg( V_{\phi}^{\pi}(s_t^{i}) - \sum_{k=t}^{H-1}r(s_{k}^{i}, a_{k}^{i}) \bigg)^2$$

where one could use $$V_{\phi}^{\pi}(s_t) = \phi(s_t)^T w_s$$

**Caveat:** The same batch of trajectories should not be used for both fitting the value function baseline, as well as estimating $$\nabla_{\theta}J$$, since it will lead to overfitting and a biased estimate. Thus, trajectories from iteration k−1 are used to fit the value function, essentially approximating $$V^{\pi}_{k-1}$$, and use trajectories from iteration k for computing advantage, $$A^{\pi}_{k}$$ and $$\nabla_{\theta} J$$.