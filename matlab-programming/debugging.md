---
description: This section covers the basics of debugging
---

# Debugging

A **bug** is an error in your code that causes your program to malfunction. A large ~~~~part of the programming experience is spotting and solving these errors. Every program eventually will have some minor or major errors, therefore it is important how to deal with them.

Errors in a program can be divided into the following classes.

## **Syntax errors**

These are errors which arise from not respecting the syntax of the language e.g. misspelling command names, forgetting to define some variable which is later used, forgetting a symbol like a parentheses somewhere. If you have syntax errors in your code and try to run it, it will not run, but throw an error instead. Most code editors \(like e.g. the MATLAB code editor\) will tell you exactly where it can´t understand your code and give you immediate feedback while you write your code. Therefore, syntax errors are easy to spot.

## **Runtime errors**

Runtime errors occur while the program is running, eventhough the syntax of your code is fine. Often they arise because the program depends on some inputs which are only defined during the runtime of the program and some code that depends on these inputs doesn´t know how to process the input.

Imagine e.g. you have a very simple program where the user can input two numbers `x` and `y` and it will return `x/y`. The program will run fine if the user enters e.g. 5 and 1, but if he/she enters 0 for y, the program will throw an error because division by 0 is not defined.

Because they only occur at runtime, runtime errors can only be spotted when regularly testing your code.

## **Semantic errors**

Semantic errors occur when the syntax is correct and your program doesn´t throw an error on runtime, but it is not behaving in the way you intended it to behave e.g. it returns the wrong results. Semantic errors are thus logical mistakes that you made when breaking the problem your are trying to solve into the essential ingredients.

Because they do not throw an error, semantic errors are the hardest to spot. The best way to spot them is to run extensive tests with your program where you use different inputs to your program and think before about how the program should behave and what the result should be. Then you run the program and compare your expectations with the results.

## Debugging Tools in MATLAB

Please refer to the MATLAB documentation page on Debugging Tools.

{% embed url="https://www.mathworks.com/help/matlab/matlab\_prog/debugging-process-and-features.html" %}



