---
description: >-
  This section provides some exercises that are meant to deepen your knowledge
  in the topics covered in this section and to gain experience solving
  real-world problems.‌
---

# Applied Exercises

## 1. Forecast density

In this exercise you will simulate a density forecast from a simple AR\(1\) model.

{% tabs %}
{% tab title="Exercise" %}
* Using an AR\(1\) model \(see below\) and assuming that $$\rho=0.7$$ and $$y_{T}=1.5$$, simulate 1000 paths for the process, 20 periods into the future, assuming that the error term is iid $$N(0,0.5^2)$$.
* Using the `prctile` function, find the median path for the process.
* Create a plot over time of the median path and the $$16^{th}$$ and $$84^{th}$$ percentiles of the forecast "distribution".
{% endtab %}
{% endtabs %}

### Theory

To forecast from an AR\(1\) model, in general we need to know the parameter values and the last value of the process, $$y_{T}$$. We can then construct the forecast for time $$T+1$$ as

$$\hat{y}_{T+1} = \rho \; y_{T}$$

We can then use the forecasted value for $$T+1$$ to create a forecast for $$T+2$$.

Note that above the error term is ignored as $$E(\epsilon_{T+i}\vert \Omega_T)=0, \forall i>0$$ where $$\Omega_T$$ is the information set at time $$T$$. We can however use Monte Carlo simulation to incorporate the uncertainty inherent in the model and get a "distribution" of forecasts.

## 2. Finding the probability of an event using Monte Carlo simulation

In this exercise you will write a Monte-Carlo simulation to answer a simple question on probabilities.

{% tabs %}
{% tab title="Exercise" %}
* Write a script that performs a Monte Carlo simulation to find the probability that the sum of the numbers coming up on two \(fair\) dice is equal to 6.
* Perform the simulation 10, 100, 1000, 10,000 times and compare the results to the theoretical answer.
{% endtab %}
{% endtabs %}

## 3. Large-sample distribution of the OLS estimator

In this exercise you will simulate the large-sample distribution of the OLS estimator.

{% tabs %}
{% tab title="Exercise" %}
1. Write a Monte Carlo simulation to explore these large sample properties. Assume that the true model is $$ y = 1 + 2x_1 + 5x_2 + \epsilon$$, $$\epsilon \sim N(0,1)$$. Let the sample size be 50 and set the number of replications to 2000.
   * Create the data sets assuming that the regressors are iid $$N(0,1)$$
   * For each replication, estimate the OLS coefficients, the variance of the error term, and the variance of the OLS coefficients.
2. Run the following experiments
   * Check that the OLS estimate has the right mean, i.e. compare the mean of the estimated coefficients to the true coefficients.
   * Check that the variance of the OLS coefficients is correctly estimated, i.e., compare your estimate to the covariance of the coefficient estimates using the `cov` function.
   * Check that the OLS estimator has the right distribution: Compare the CDF of the normalized estimate of $$\beta_2$$ to the CDF of the standard normal distribution
{% endtab %}

{% tab title="Check" %}
From standard asymptotic theory we know that the OLS estimator is normally distributed with mean equal to the true coefficients and covariance equal to $$\sigma^2(X'X)^{-1}$$.
{% endtab %}
{% endtabs %}

