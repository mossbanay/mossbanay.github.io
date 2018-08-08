+++
title = "Week 3 Lecture - Parameter Estimation"
date = 2018-08-08T21:00:00+10:00
categories = ["emacs"]
draft = false
+++

## Maximum likelihood {#maximum-likelihood}

Suppose we have some sample \\(y\\) drawn from a parametric distribution and we wish to estimate the unknown parameterisation \\(\theta\\). Fisher's MLE proposes we look at the probability of drawing our sample from the distribution conditional on some parametrisation. We call this the **likelihood function** and write it as

\\[ p(\bf{y} | \theta) \\]

For independent draws, this is simply an evaluation of the joint distribution

\\[ p(\textbf{y} | \theta) = \prod\_{i=1}^n p(y\_i | \theta) \\]

The maximum likelihood estimator (MLE) is the parametrisation that maximises the likelihood function. Concretely the MLE \\(\hat{\theta}\\) is

\\[ \hat{\theta} = \underset{\theta}{\text{argmax}} \{ p(\textbf{y} | \theta) \} \\]

In practice, it's normally easier to maximise the negative log likelihood for numerical reasons.


## Sampling distribution {#sampling-distribution}

When we collect a sample of observations from a population, we should note that we have picked one sample of a particular size of out of infinitely many possiblities. It's possible that if we had picked another sample (even of the same size) and ended up with different estimates for the mean and variance of a distribution (for example).

Suppose we have \\(n\\) draws from a normal distribution \\(Y\_i \stackrel{iid}{\sim} N(\mu, \sigma^2)\\). The distribution of the sample mean \\(\hat{Y}\\) where

\\[ \hat{Y} = \frac{1}{n} \sum\_{i=1}^n Y\_i \\]

then \\(\hat{Y}\\) is also a random variable, also with a normal distribution. Using some simple facts about adding and scaling normal distributions to show that

\\[ \hat{Y} \sim N \left ( \mu, \frac{\sigma^2}{n} \right ) \\]

We see a number of expected properties here,

-   The average value of \\(\hat{Y}\\) is indeed the population mean \\(\mu\\)
-   The larger the sample we draw, the less variability \\(\hat{Y}\\) has

It is crucial to take into account the uncertainty of our estimates of the mean and variance of the distribution when making inference from our data. The point estimates are useful but not exact, since they are themselves random variables.


## Bias and variance {#bias-and-variance}

<div class="DEF">
  <div></div>

**Estimator bias** is the degree to which an estimator tends to overestimate or underestimate a population parameter. Given a sample \\(\textbf{y}\\), if \\(\hat{\theta}(\textbf{y})\\) is an estimator then its bias is given by

\\[ b\_{\theta}(\hat{\theta}) = \mathbb{E}[\hat{\theta}(\textbf{y})] - \theta \\]

If \\(b\_{\theta}(\hat{\theta}) = 0\\) \\(\forall \theta\\) then we say the estimator is **unbiased**.

</div>

<div class="DEF">
  <div></div>

**Estimator variance** is the degree to which an estimator fluctuates around the population parameter. It is the variance of the **sampling distribution** of \\(\hat{\theta}\\).

\\[ \text{Var}\_{\theta}(\hat{\theta}) = \mathbb{E} \left [ \left (\hat{\theta}(\textbf{y}) - \mathbb{E}[\hat{\theta}(\textbf{y})] \right )^2 \right ] = \mathbb{V}[\hat{\theta}(\textbf{y})] \\]

</div>

In some cases we may find that we have a tradeoff to make between an estimator that has lower systematic bias but higher variance compared to an estimator with low variance but higher systematic bias. This may become a messy and unstructured choice, one way of simplifying such a decision is to use **mean squared error (MSE)** as a heuristic to pick an estimator. The MSE of an estimator is simply given as

\\[ \text{MSE}\_{\theta}(\hat{\theta}) = \mathbb{E}[(\hat{\theta}(\textbf{y}) - \theta)^2] \\]

The lower the MSE the better the estimator. We may notice through some algebra that the MSE can also be written as

\\[ \text{MSE}\_{\theta}(\hat{\theta}) = b\_{\theta}(\hat{\theta})^2 + \text{Var}\_{\theta}(\hat{\theta}) \\]


## Consistency {#consistency}

An estimator \\(\hat{\theta}\\) is consistent if and only if the estimator **converges in probability** to the population parameter. Concretely,

\\[ \lim\_{n \rightarrow \infty} Pr(|\hat{\theta}(\textbf{y}) - \theta| > \epsilon) = 0 \\]

for some small \\(\epsilon > 0\\).
