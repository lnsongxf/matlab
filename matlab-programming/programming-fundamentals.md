---
description: >-
  This section gives an abstract introduction to some of the concepts used in
  this section.
---

# Programming Fundamentals

The goal of this section is to introduce the reader to some of the abstract concepts that are used in \(scientific\) programming. Since most programming languages share the same abstract concepts, it is very beneficial to familiarise oneself with the abstract building blocks of a programming language before learning programming patterns specific to MATLAB.

This section will introduce the reader to abstract concepts like variables, loops, conditions, functions and debugging.

{% hint style="info" %}
Most examples on this page use pseudo-code notation i.e. it the displayed code is not valid MATLAB code. The code is meant to provide an example of how the concepts could be implemented in different programming languages \(R, C++, Python, MATLAB, ...\) and is therefore general. The next sections of the course will cover the specific implementations in MATLAB.
{% endhint %}

## Essential ingredients of a programme

The reason we write computer programs/scripts in scientific applications is that we want to solve problems that we cannot solve by hand because the task is either too complex or it would take too long to carry out all necessary steps. In essence, a **computer program** or **script** is a set of instructions that tell a computer which operations to perform step by step to solve a specific problem.

All scientific programs, simple or complex can be reduced to the following essential types of instructions:

* **Inputting data:** Reading data from memory, file or some other device
* **Outputting data:** Saving/writing data to memory, file or some other device
* **Basic mathematical operations:** Perform simple calculations like addition, subtraction, multiplication or division
* **Repetition:** Repeat sets of commands \(with slight variations\)
* **Conditional execution:** Execute one code block or another based on a simple criterion

Writing programs is solving complex tasks by sequentially stacking very simple building blocks one after each other. Most programming languages share the following fundamental building blocks.

## Values

In an abstract sense, a value is data of some specific form that is stored in the computers memory and is used to carry out a specific command. Usually a value is one of the following data types.

| Data type | Description | Example | Comment |
| :--- | :--- | :--- | :--- |
| **int** | Integer \(whole number\) | 7 or 3 or -5 |  |
| **float** | A real floating point number \(has a fractional part\) | 1.2 or 3.14159 | 32 bit, takes up less memory, but less precise |
| **double** | A double-precision floating point number | 3.14159265359 | 64 bit, takes up more memory, but more precise |
| **char** | A single character | "a" or "Q" |  |
| **string** | An array of chars \(text\) | "hello" or "This is a sentence" |  |
| **boolean** | A logical value, either 'True' \(=1\) or 'False' \(=0\) | True, False, 1, 0 |  |

Scientific programming languages like MATLAB often also have specific data types to store arrays of numbers \(e.g. `matrix` or `array` in MATLAB\) or arrays of mixed numbers and text \(`cellarray` in MATLAB\).

## Constants and variables

Constants and variables are essentially names that point to specific values which are stored in memory \(i.e. a named memory location\). **Constants** are objects whose value cannot be changed during the runtime of the program while the values of **variables** can be changed while the program is running.

Consider the following pseudo-code that declares different variables and assigns them a value which might be changed later.

{% tabs %}
{% tab title="Pseudocode" %}
```text
x = 3
c = "Z"
name = "this is a string"
Pi = 3.14159265359
x = 5
completed = False
```
{% endtab %}

{% tab title="MATLAB" %}
```text
x = 3;
c = "Z";
name = "this is a string";
Pi = 3.14159265359;
x = 5;
completed = false;
```
{% endtab %}

{% tab title="Python" %}
```python
x = 3
c = "Z"
name = "this is a string"
Pi = 3.14159265359
x = 5
completed = False
```
{% endtab %}

{% tab title="R" %}
```r
x <- 3
c <- "Z"
name <- "this is a string"
Pi <- 3.14159265359
x <- 5
completed = FALSE
```
{% endtab %}
{% endtabs %}

Later when we would like to use the value in our program, we can refer to the value by its name, e.g. `x`.

Note that some program languages require you to declare the data type before first assigning a value to a constant or variable. Other languages like MATLAB automatically set the data type based on the value that is assigned.

Generally variables can be named freely, however different programming languages make different restrictions \(e.g. in MATLAB variable names cannot start with a number or contain special characters\). Also certain names might be reserved by the language as keywords since they refer to a command or function and using them as a variable name would cause ambiguity.

## Functions

A function is a block of instructions that are performed on one or multiple input values and which returns one or multiple output values. Essentially a function is a program that performs a specific computation and that has been given a specific name so that it is reusable. Functions do not need to have an input but it is good practice to have a function always return some value.

Examples for functions can e.g. be mathematical operations/functions like `sqrt(x)` which accepts an input value `x` and returns its square-root or more complex operations like e.g. `compute_ols_estimator(y, X)` which could be a function that computes the OLS regression coefficients from regression the vector `y` on the columns of the matrix `X` and which outputs the coefficients, their standard errors, the fit of the model etc.

Most scientific programming languages come with built-in functions for standard mathematical or statistical operations, but functions can also be declared by the user to re-use code in different parts of your program without having to repeat it. As a general rule, if you need to repeat some blocks of code somewhere in your script you should create a function for it.

Functions usually have a syntax similar to the following one.

{% tabs %}
{% tab title="Pseudocode" %}
```text
function functionname (input_arguments) {
  code_block_that_uses_inputs_to_calculate_output
  return(output)
}
```
{% endtab %}

{% tab title="MATLAB" %}
```text
function [outputArg1,outputArg2] = functionName(inputArg1,inputArg2)
  ...
  outputArg1 = ...;
  outputArg2 = ...;
end
```
{% endtab %}

{% tab title="Python" %}
```python
def functionname(inputArg1, inputArg2):
  ...
  return outputs
```
{% endtab %}

{% tab title="R" %}
```r
functionname <- function (inputArg1, inputArg2) {
  ...
  return(outputs)
}
```
{% endtab %}
{% endtabs %}

**Example**

Consider the following example where we code an estimator that makes a prediction of the next value of some variable `y` based on the previous value `y_prev` and some other variable `x` and returns an object with the prediction.

```text
function predict_y (y_prev, x) {

  code_to_make_prediction

  return(prediction)
}
```

Once declared we could then call the function anywhere in the code e.g.

```text
y_prev =3
x = 5
ynext = predict_y(y_prev, x)
```

## Conditions

A condition defines a decision about which block of code to execute depending on a simple criterion. Conditions are phrased in terms of boolean i.e. true-false decisions. The following condition clauses are used in many programming languages

### **if-else statements**

**if statements** wrap around a code block and execute it only when a certain condition is met \(i.e. checking the condition returns a `True` boolean value\).

**if-else statements** wrap around two code blocks and execute the first block only when the condition returns `True`. Otherwise the second code block is executed.

These statements usually follow the following syntax \(in pseudocode\).

{% tabs %}
{% tab title="Pseudocode" %}
```text
if (condition) {
  code_block
}

if (condition) {
  code_block
} else {
  alternative_code_block
}
```
{% endtab %}

{% tab title="MATLAB" %}
```text
if condition
  ...
end

if condition
  ...
else
  ...
end
```
{% endtab %}

{% tab title="Python" %}
```python
if (condition):
  ...
  
if (condition):
  ...
else:
  ...
```
{% endtab %}

{% tab title="R" %}
```r
if (condition) {
  ...
}

if (condition) {
  ...
} else {
  ...
}
```
{% endtab %}
{% endtabs %}

**Example**

Consider the following pseudocode example where we assume that we have created a variable `number` in which we stored some value.

```text
if (number > 5) {
  number = number -1
} else {
  number = number + 1
}
```

Of course multiple if or if-else statements can be nested to describe more complex decisions.

### **switch-case-otherwise statements**

**switch-case-otherwise statements** work similarly to if-else statements, but are especially useful if the condition involves checking multiple cases. They take the following form \(in pseudocode\).

{% tabs %}
{% tab title="Pseudocode" %}
```text
switch (condition) {
  case value_1:
    code_block_1

  case value_2:
    code_block_2

  case value_3:
    code_block_3

  otherwise:
    alternative_code_block
}
```
{% endtab %}

{% tab title="MATLAB" %}
```text
switch variable
    case value1
        ...
    case value2
        ...
    case value3
        ...
    ...
    otherwise
        ...
end
```
{% endtab %}

{% tab title="Python" %}
{% hint style="info" %}
Python has no implementation of switch-case.
{% endhint %}
{% endtab %}

{% tab title="R" %}
```r
# R's switch works on string variables only
switch(variable, 
foo={
  ...
},
bar={
  ...   
},
{
  ...
}
)
```
{% endtab %}
{% endtabs %}

**Example**

Say we are writing a program that allows the user to replicate some results obtained using an algorithm we invented. The program also allows to run the same calculations using two algorithms proposed earlier by the literature. The user can decide which program to run by entering the respective string which is saved in the `method` variable.

```text
  method = input('Which algorithm would you like to run?')

  switch (method) {

    case "my_algorithm"
      run_my_algorithm()

    case "algorithm_paper1"
      run_algorithm_from_paper_1()

   case "algorithm_paper2"
      run_algorithm_from_paper_2()

    otherwise
      display("Please specify a valid algorithm.")
  }
```

## Loops

Loops are used to repeat sets of commands \(with some slight variations\) without having to rewrite them multiple times.

### **for-loop**

A **for-loop statement** loops over a command a specific number of times, keeping an index of the current iteration which increments each time the loop is completed.

{% tabs %}
{% tab title="Pseudocode" %}
```text
for counter = start_value to end_value {
    code_block_dependend_on_counter
}
```
{% endtab %}

{% tab title="MATLAB" %}
```text
for counter=startValue:endValue
  ...
end
```
{% endtab %}

{% tab title="Python" %}
```python
for counter in range(1,n+1):
  ...
```
{% endtab %}

{% tab title="R" %}
```r
for (counter in seq(1,n)) {
  ...
}
```
{% endtab %}
{% endtabs %}

**Example**

Consider the following example where we would like to run a simulation which runs some estimation on an artificially generated dataset.

```text
  nr_simulations = 5000
  for i = 1 to nr_simulations {

    generate_dataset()
    run_estimation()
    save_results()

  }
```

### **while-loop**

A **while\_loop statement** iterates as long as the supplied condition is `True`.

It has the following form

{% tabs %}
{% tab title="Pseudocode" %}
```text
while boolean_condition {
  code_block
}
```
{% endtab %}

{% tab title="MATLAB" %}
```text
while condition
  ...
end
```
{% endtab %}

{% tab title="Python" %}
```python
while condition:
  ...
```
{% endtab %}

{% tab title="R" %}
```r
while (condition) {
  ...
}
```
{% endtab %}
{% endtabs %}

Often it is useful to manually introduce a counter of the number of iterations.

```text
iter = 1
while boolean_condition {
  code_block_potentially_dependend_on_iter
  iter = iter + 1
}
```

> Note: Caution must be taken when programming while loops as mistakes in the condition can cause the loop to iterate infinitely thereby blocking execution of the rest of the program.

**Example**

Say we are coding a fixed point algorithm and we would like to check whether the algorithm has converged. Then we could set up the following loop.

```text
tolerance = 1e-5
converged = False
iter = 1
while (!converged) {

  do_algorithm_step()

  convergence_criterion = calculate_criterion()

  if (convergence_criterion < tolerance) {
    converged = True
  }

}
```

This loop will iterate on the step of the algorithm until the convergence criterion \(which e.g. could be the difference between the value at `iter` and value at `iter-1` is smaller than `tolerance`, here 0.00001\).

