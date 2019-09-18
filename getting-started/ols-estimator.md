---
description: >-
  This section provides some exercises that are meant to deepen your knowledge
  in the topics covered in this section and to gain experience solving
  real-world problems.
---

# Applied exercises

## 1. Computing the OLS estimator

In this exercise you will compute the OLS estimator on a simulated data set using basic MATLAB commands. Please refer to the theory section below for the necessary formulas.

{% tabs %}
{% tab title="Exercise" %}
Import the simulated data from _olsdata.m_ and compute the OLS estimator $$\hat{\beta}$$ using matrix expressions. Create a results matrix which stacks the estimated parameters and the values supplied in the vector `beta_true` side by side. Are the estimated and the true values close?

Next, read up on MATLABs `regress` function on the [MATLAB documentation page on regress](https://www.mathworks.com/help/stats/regress.html). Estimate the OLS coefficient using this function and compare the results to the ones you computed manually.
{% endtab %}

{% tab title="Getting started" %}
* [ ] Create a new folder for this exercise and copy the olsdata.mat file into it
* [ ] In MATLAB, create a new script and save it into the same folder 
* [ ] Start your script with the following commands

```text
  clear all; close all; clc;
  load olsdata.m
```

* [ ] Check the data has been loaded into your workspace. You should see a matrix `X`, a vector `y` as well as a vector `beta_true` which contains the true values of $$\beta$$ that were used to generate the data
* [ ] Add a line which computes the OLS estimator and saves it into a new variable `beta_hat`

```text
beta_hat = ...formula goes here...
```

_Note that you can code up the formula in two ways. Either by computing_ $$(X'X)^{-1}$$ _separately from_ $$X'y$$ _and then multiplying them or by directly writing the formula into one line_.
{% endtab %}

{% tab title="Solution" %}
```text
% Compute OLS estimator
clear all; close all; clc;

load olsdata

% Compute OLS estimator
beta_hat = (X'*X)\(X'*y);

% Compare to true value
[beta_hat, beta_true]

% Extension: Compare to MATLABs regress function
beta_regress = regress(y,X);
[beta_hat, beta_regress]
```
{% endtab %}
{% endtabs %}

#### Theoretical Background

Let $$y$$ be a $$N \times 1$$ vector of data on the dependent variable and let $$X$$ be a $$N \times K$$ matrix with data on the regressors where the first column is a vector of ones.

The OLS estimator of the regression coefficients is defined as



$$
\hat{\beta} = (X'X)^{-1} (X'y)
$$

## 2. Computing the log-likelihood of a Probit model

&lt;TBA soon&gt;

## 3. Estimating a factor model using Principal Components

&lt;TBA soon&gt;

