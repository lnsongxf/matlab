---
description: This section deals with custom functions in MATLAB.
---

# Custom Functions

In MATLAB, we can define our custom functions. Functions are necessary to avoid repeating code throughout your script. Typically there are two reasons why we need a custom function.

1. We would like to repeat a more complex mathematical expression. The easiest way to achieve this is to use MATLAB's **anonymous functions**.
2. We would like to avoid repeating several statements to keep our code efficient and short. The best way to achieve this is to use **custom functions**.

## Defining anonymous functions

Anonymous functions are used to shorten and reuse mathematical expressions throughout your code e.g. when performing numerical optimization. You are already familiar with this type of function from basic analysis.

Anonymous functions typically have the following syntax.

`y = @(x) <expression based on x>`

Consider the following example where we would like to evaluate a more complex expression for different values of `x`.

```text
y = @(x) abs(x-2) + x^2 - x/2;
y(0)
y(1)
y(10)
y(-5)
```

## Defining custom functions

Custom functions must be defined in their own .m file with the name _yourfunctionname.m_ in your main working directory. They typically have the following syntax.

{% code-tabs %}
{% code-tabs-item title="myfunction.m" %}
```text
function [out1, out2, ...] = myfunction(in1, in2, ...)

  % Commands defining out1, out2, ...
  % depending on in1, in2, ...
end
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> _Note:_ If you wish to store you function in a subdirectory named _myfolder_, you can do this by adding `addpath('myfolder')` to the beginning of you main .m file.

## Function scope

Note that variables defined inside a function have **local scope** i.e. they are valid only inside the function. Also, functions operate on a copy of the input variables i.e. they do not directly change the value of the input variables.

Consider the following example.

{% code-tabs %}
{% code-tabs-item title="dividebytwo.m" %}
```text
function y = dividebytwo(x)
  y = x/2;
end
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="main.m" %}
```text
x = 5;
dividebytwo(x);
x % not changed

x = dividebytwo(x);
x % changed
```
{% endcode-tabs-item %}
{% endcode-tabs %}

