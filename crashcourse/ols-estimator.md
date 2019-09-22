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
* Create a new folder for this exercise and copy the olsdata.mat file into it
* In MATLAB, create a new script and save it into the same folder 
* Start your script with the following commands

```text
  clear all; close all; clc;
  load olsdata.m
```

* Check the data has been loaded into your workspace. You should see a matrix `X`, a vector `y` as well as a vector `beta_true` which contains the true values of $$\beta$$ that were used to generate the data
* Add a line which computes the OLS estimator and saves it into a new variable `beta_hat`

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

{% file src="../.gitbook/assets/datasets-getting-started.zip" caption="Datasets for this section" %}

#### Theoretical Background

Let $$y$$ be a $$N \times 1$$ vector of data on the dependent variable and let $$X$$ be a $$N \times K$$ matrix with data on the regressors where the first column is a vector of ones.

The OLS estimator of the regression coefficients is defined as $$\hat{\beta} = (X'X)^{-1} (X'y)$$.

## 2. Computing the log-likelihood of a Probit model

In this exercise you will compute the log-likelihood of a Probit model on a simulated data set using basic MATLAB commands. Please refer to the theory section below for the necessary formulas.

{% tabs %}
{% tab title="Exercise" %}
Import the simulated data from _logitdata.m_ and calculate the value of the log-likelihood for different values of the parameter vector $$\beta$$ using matrix expressions.

Approximately, for which value of $$\beta$$ is the log-likelihood maximal?
{% endtab %}

{% tab title="Getting started" %}
* Create a new folder for this exercise and copy the _logitdata.mat_ file into it
* In MATLAB, create a new script and save it into the same folder 
* Start your script with the following commands

```text
  clear all; close all; clc;
  load logitdata.m
```

* Check the data has been loaded into your workspace. You should see a matrix `X`, and a vector `y`
* Fix a value for $$\beta$$ by setting it to e.g. 0.5

```text
beta = 0.5
```

* Create a variable `L`and assign it the value of the formula for the likelihood from the theory section

```text
L = ...formula goes here...
```

_Hint: When coding up the formula, write it as a function of a vector. Start with the inner parts of the formula i.e. first think about how_ $$x_i \beta$$ _looks like for different_ $$i$$ _and how you can write it as a vector. Then think about what applying functions like `exp()` and `ln` \(which in MATLAB is the `log` function\) does to this vector. Finally think about how to evaluate the sum. It might be easiest to split up the formula into two separate parts \(the one starting with_ $$y_i$$ _and the one starting with_ $$(1-y_i)$$ _that you save in different variables, then evaluate the `sum` operator over the sum of these variables._
{% endtab %}
{% endtabs %}

{% file src="../.gitbook/assets/datasets-getting-started.zip" caption="Datasets for this section" %}

#### Theoretical Background

Consider the following discrete choice logit model with no constant and one regressor

$$y_i = x_i \beta + \varepsilon_i$$

where all variables are scalars and $$y_i$$ is a binary variable \(i.e. it has 0/1 values\).

The log-likelihood of the data given a value for the parameter vector $$\beta$$ is defined as

$$\mathcal{L}(\beta) = \sum^N_{i=1} \; y_i \ln\left( \frac{exp(x_i \beta)}{1+exp(x_i \beta)} \right) + (1-y_i) \ln\left( \frac{1}{1+exp(x_i \beta)} \right)$$

## 3. Estimating a factor model using Principal Components \(Advanced\)

In this exercise you will estimate a factor model on a simulated data set using basic MATLAB commands. Please refer to the theory section below for the necessary formulas.

{% tabs %}
{% tab title="Exercise" %}
Read up on MATLABs `eig` function on the [MATLAB documentation page on eig](https://www.mathworks.com/help/matlab/ref/eig.html). Use the `eig` function to estimate the matrix of factors $$F$$ and loadings $$\Lambda$$ for the following dataset for $$r=2$$.

**Caution:** By default, `eig` sorts the eigenvalues and corresponding vectors in ascending order of magnitude of the eigenvalues. Make sure you extract the $$r$$ eigenvectors corresponding to the $$r$$**largest** eigenvalues.
{% endtab %}

{% tab title="Extension" %}
The estimation above is valid only under the assumption that the factors are orthogonal i.e. $$F'F/T = I$$. Use MATLABs `scatter(x,y)` command and verify graphically that the normalization holds for the estimated factors. In the scatter command, `x` should be the first factor \(i.e. the first column of $$\hat{F}$$\) and `y` should be the second factor.
{% endtab %}
{% endtabs %}

{% file src="../.gitbook/assets/datasets-getting-started.zip" caption="Datasets for this section" %}

#### Theoretical Background

We will use the following factor model

$$X_t = \Lambda \; F_t + u_t$$

where $$X_t$$ is large $$N \times 1$$ vector of series which we would like to explain by a lower number of factors. $$F_t$$ is a $$r \times 1$$ vector of factors and $$u_t$$ an $$N \times 1$$ vector of idiosyncratic shocks. $$\Lambda$$ is a matrix of factor loadings of dimension $$N \times r$$. $$T$$ is the number of observations.

Under some normalizations, the $$r$$ factors and their factor loadings $$\Lambda$$ can be estimated by principal components using the following formulae.

$$\hat{F} = \sqrt{T} \; EV(XX')_{1:r}\hspace{1.5cm}  \hat{\Lambda} = \hat{F}' X / T$$

where $$F$$ is a $$T \times r$$ matrix and $$X$$ is a $$T \times N$$ matrix. $$EV(A)_{1:r}$$ denotes the first $$r$$ eigenvectors of the matrix $$A$$ which correspond to the $$r$$ largest eigenvalues.

