# Numerical Optimization

## Numerical Optimization in MATLAB

Matlab's optimization toolbox contains several routines designed to find the minimum of a user-supplied objective function. This is, obviously, not restrictive as the minimum of a function -f\(\) is located at the same point as the maximum of f\(\).

To use the routines we need to begin by creating a matlab function that returns the value of the function we want to find an extremum of for a given set of parameters. An example would be the value of the log-likelihood of a model given the parameter values. As a rule, these custom functions need to have the parameters as the first argument.

A general form of such a custom function would be

```text
function obj = target_function(params,var1,var2,...)
obj = f(params,var1,var2,...);
end
```

where "params" is the vector of parameters we want to numerically optimize and the rest are other relevant variables, such as data or hyperparameters, and "obj" is the value of the function given values of "params". Note that if the parameters do not enter the function of interest as a single vector we will have to "unwrap" them within the function. For example, if our function is the log-likelihood of a linear model with a constant and one explanatory variable, the "params" vector will have three elements, the constant, the coefficient related to our explanatory variable, and the standard deviation of the error term. Within our function we would thus have to unwrap them as

```text
b = params(1:2);
s2 = params(3);
```

after which we can set up the function to be minimized.

## Unconstrained Derivative-based Optimization

The routine `fminunc` is a gradient based routine that finds an unconstrained minimum. Its generic form is

```text
[p, fval, exitflag] = fminunc('target_function',p0,options,var1,var2,...)
```

where p0 is a vector of starting values for the parameters, "options" specifies the optimization options to use, and "var1", "var2", etc. are optional variables that will be passed to the target\_function.

For example, say that our objective function is

```text
function obj = target_function(params,hyperparams)
x = params(1);
y = params(2);

a = hyperparams(1);
b = hyperparams(2);
c = hyperparams(3);
d = hyperparams(4);
e = hyperparams(5);

obj = a+ b*x + c*x^2 + d*y + e*y^2;
end
```

To find the minimum, we write

```text
options = optimset('fminunc');
options = optimset(options, 'Display','iter');
p0 = [1 1];
hyper = [1, 2, 1.5, 1, 0.5];
[p,fval,exitflag] = fminunc('target_function',p0,options,hyper);
```

## Unconstrained Derivative-free Optimization

A possible drawback of `fminunc` is that it requires the function to be differentiable. If our function on interest is not continuously differentiable, we need to use derivative-free methods. One such method is `fminsearch` which uses an "amoeba" to explore the parameter space while always moving to a lower objective function value.

The syntax for `fminsearch` has the same form as `fminunc` so to continue on with our example from above, we have

```text
options = optimset('fminsearch');
options = optimset(options, 'Display','iter');
p0 = [1 1];
hyper = [1, 2, 1.5, 1, 0.5];
[p,fval,exitflag] = fminsearch('target_function',p0,options,hyper);
```

However, `fminsearch` is a lot slower than `fminunc` as it requires more iterations and more function evaluations. Thus it should not be used unless `fminunc` does not perform satisfactorily.

## Bounded Scalar Optimization

If we have a problem where we need to find the minimum of a function with respect to only a single parameter we can \(in addition to using `fminunc`\) use `fminbnd` which searches for a minimum over a bounded interval using a golden section algorithm.

The syntax is similar to the previous ones with the exception that instead of starting values we have the upper and lower bounds of the interval to search in, i.e.:

```text
[p, fval, exitflag] = fminbnd('target_function',lb,ub,options,var1,var2,...)
```

where lb and ub are the lower and upper bounds of the parameter.

Modifying the target function from above, we have

```text
function obj = target_function2(x,hyperparams)

a = hyperparams(1);
b = hyperparams(2);
c = hyperparams(3);

obj = a+ b*x + c*x^2;
end
```

To use `fminbnd` to find the minimum we write

```text
options = optimset('fminbnd');
options = optimset(options,'Display','iter');
hyper = [1,2,1.5];
[x,fval,exitflag] = fminbnd('target_function2',-5,5,options,hyper)
```

## Constrained Derivative-based Optimization

Finally, if our problem includes linear and/or nonlinear constraints, which can be in equality and/or inequality form, we can use the `fmincon` function. For more information on performing constrained optimization in Matlab see the help documentation.

## Optimization Options

To change the options related to the optimization routine, we use `optimset`. Changing the options should always start by calling

```text
options = optimset('fminXXX')
```

i.e., create a structure called "options" consisting of the default options for "fminXXX", representing a specific optimization routine. After that, specific options are changed by

```text
options = optimset(options,'option1', option1 value, 'option2', option2 value,...)
```

Some common examples of options changed for, e.g., `fminunc` are

```text
options = optimset('fminunc');
options = optimset(options, 'Display', 'iter');
options = optimset(options, 'MaxFunEvals', 1000);
options = optimset(options, 'MaxIter', 1000);
options = optimset(options, 'TolFun', 1e-5);
```

