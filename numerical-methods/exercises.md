# Applied Exercises

## 1. Estimate a probit regression using MLE

In this exercise you will estimate a probit regression model using maximum likelihood.

{% tabs %}
{% tab title="Exercise" %}
Recall the log likelihood of the probit model from Section 1:

$$\mathcal{L}(\beta) = \sum^N_{i=1} \; y_i \ln\left( \frac{exp(x_i \beta)}{1+exp(x_i \beta)} \right) + (1-y_i) \ln\left( \frac{1}{1+exp(x_i \beta)} \right)$$

Using the dataset provided in Section 1, write a script that estimates the unknown parameter $$\beta$$ using

1. `fminunc`
2. `fminsearch`
3. `fminbnd`
{% endtab %}

{% tab title="Getting started" %}
* Using the log likelihood, create a target function .m file that accepts the unknown parameter and the dataset as inputs and outputs the log likelihood for those parameter values.
* In another script, select the options and starting values you want for each estimation function. Then use the optimization functions \(1\)-\(3\) to estimate the unknown parameter.
* **Bonus part**: Set up your script using `switch-case` so that when you run the script, it begins by asking the user which method is desired. _Hint:_ Use matlab's `input` function to ask the user which method to use.
{% endtab %}
{% endtabs %}

## 2. Estimate an AR\(1\) regression using MLE

In this exercise you will estimate an AR\(1\) regression using Maximum Likelihood.

{% tabs %}
{% tab title="Exercise" %}
This task consists of two parts. In the first part you will simulate data from a stationary AR\(1\). In the second part you will use this data to estimate the AR\(1\) model by MLE and verify that you correctly estimated $$\phi$$ and $$\sigma^2$$.

1.  Simulate data from a stationary AR\(1\) model building on the code example we covered in Part A of unit 4. Set $$T=500$$ and use $$y_0=0$$ and use 200 burn-in periods. Use the same parameter values that we used in the example. After you have simulated the data, export the vector containing the $$y$$ values into a .mat file using the `save` command.
2. Create a new script and load the .mat file you just generated. Write function file for the target function which calculates the likelihood given parameter values for $$\phi$$ and $$\sigma$$. Then, create a new script and use `fminunc` to estimate $$\phi$$ and $$\sigma^2$$ from the data on $$y$$ you just imported.

**Note:** Remember that you have to choose sensible starting values for the optimisation algorithm. Make sure these starting values are different from the true parameter values you used to generate the data.
{% endtab %}

{% tab title="Hint" %}
**Hint:** Since $$\sigma^2$$ is a variance, it should never take negative values. You can enforce this without having to rely on a constrained optimization routine. You can solve this by defining $$\sigma^2=\exp{x}$$ and optimize over $$x$$ instead of $$\sigma^2$$. Remember that when you compare your estimated parameter values to the ones you used to generate the data that you should compare to $$\exp{x}$$ and not $$x$$.
{% endtab %}
{% endtabs %}

### Theory

Consider the following stable AR\(1\) model

$$y_t = \phi \; y_{t-1} + \epsilon_t \hspace{20pt} \epsilon_t \sim iid \; N(0,\sigma^2), \hspace{20pt} |\phi|<1$$

We would like to estimate the unknown parameters $$\phi, \sigma^2$$ by maximum likelihood. Therefore we would like to find the values of $$\phi$$ and $$\sigma^2$$ which maximize the following log-likelihood.

$$\begin{align}\log \mathcal{L}(y; \phi,\sigma^2) = &-(T/2) \log(2\pi) -(T/2) \log(\sigma^2)-(2\sigma^2)^{-1}\sum_{t=2}^{T}(y_t-\phi y_{t-1})^2 \\ &+ (1/2)\log(1-\phi^2)-(2\sigma^2)^{-1}(1-\phi^2)y_1^2 \end{align}$$

## 3. Solving an optimal consumption problem

In this exercise you will solve an optimal consumption problem using MATLABs numerical solvers.

{% tabs %}
{% tab title="Exercise" %}
Consider a consumer who solves the following consumption \($$C$$\) vs. leisure \($$L$$\) problem

 $$max_{C,L} \; AC^{\alpha}L^{\beta}$$ 

subject to the budget constraint $$ C=wL$$ where $$w$$ is the wage.

Write a Matlab program that solves this problem for given parameter values of $$A$$, $$\alpha$$, $$\beta$$, and $$w$$. In particular

* Start by reducing the problem to a one-dimensional problem in either $$C$$ or $$L$$.
* First solve the one-dimensional problem using the `fzero` function.
* Then solve the one-dimensional problem using the `fminunc` function.
{% endtab %}
{% endtabs %}

