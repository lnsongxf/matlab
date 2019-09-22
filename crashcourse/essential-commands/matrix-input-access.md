---
description: >-
  This section familiarises you with basic commands to input matrices/vectors
  and accessing their elements. You should memorise these to speed up your
  coding.
---

# Matrix Input and Access

## Basic syntax

{% hint style="info" %}
To try out the commands on this page just type them directly into the MATLAB Command Window and hit &lt;Enter&gt; to execute them.
{% endhint %}

Most MATLAB commands follow one of the following syntaxes

```text
variable = expression;
variable = command(arguments);
variable = command(arguments)
command(arguments)
```

The semicolon at the end of a command `;` suppresses the display of the result or the output of the command. Lines can be commented out by starting the line with a percentage sign `%`.

```text
% this is a comment which will not be executed
command(arguments)
```

## Variables

In MATLAB, we store any kind of data \(numbers, strings etc.\) in `variables`. Here are a few examples of how to assign variables.

```text
x = 1                       % store scalar value
y = 3 + 2 * exp(x);         % evaluate expression and store value
z = 3 + 2 * exp(x)          % evaluate expression, store and print value

y                           % print value to console
display(y)                  % equivalent

u = 'I am not a number'     % store strings
```

## Vectors and matrices

Vectors and matrices are a special type of variables which can be created, accessed and modified using special commands.

**Creating vectors and matrices**

We can create row and column vectors either by entering them directly or by transposing vectors.

```text
a = [1, 2, 3, 4, 5]         % row vector
b = [6; 7; 8; 9; 10]        % column vector

z = a'                      % column vector by transposing row vector
u = b'                      % row vector by transposing column vector
```

We can create matrices in a similar fashion by entering them row by row or by concatenating previously entered vectors or matrices.

```text
A = [1, 2; 3, 4]            % declare matrix directly by rows

b = [5; 6];
B = [A, b]                  % join columns of 2x2 matrix A and 2x1 vector b
C = [A; b']                 % join rows of 2x2 matrix A and 1x2 vector b'
```

**Accessing matrix and vector elements**

We can access elements of a vector by supplying the indices of the values that we want to select in parentheses.

```text
a = [5, 6, 7, 8, 9];        % row vector
b = a';                     % column vector

a(4)                        % returns the 4-th element
a(2:4)                      % returns elements 2-4 of row-vector
a([1, 3, 4])                % returns elements 1, 3, 4 of row-vector
a([1; 3; 4])                % equivalent

b([1, 3, 4])                % returns elements 1, 3, 4 of column vector
```

We can access elements of a matrix in a similar fashion by supplying either the indices with respect to the column-wise index or by supplying row and column indices separately.

```text
A = [1, 2, 3; 4, 5, 6; 7, 8, 9]

A(4:6)                      % returns elements 4-6 counting columnwise
A(2,3)                      % returns element in row 2, column 3
A(1:2, 2:3)                 % return submatrix with rows 1-2, columns 2-3
A([1, 3], [1, 2])           % return submatrix with rows 1, 3 and columns 1, 2
```

We can also use the colon-operator `:` to select all elements of a specific dimension.

```text
A(2, :)                     % return second row of the matrix
A(:, 3)                     % return third row of the matrix
A(1:2, :)                   % return submatrix with first two rows
```

The concepts discussed in this section extend easily to arrays of higher dimensions that 2.

**Replacing elements in matrices**

We can use the tools from the last section to easily replace individual elements of a matrix or even sub-matrices.

```text
A = [1, 2, 3; 4, 5, 6; 7, 8, 9]

A(2,3) = 10                 % replace element in row 2, column 3
A(1:2, 1:2) = zeros(2,2)    % replace upper left 2x2 submatrix
A(:, 1) = [0, 1, 2]'        % replace first column
```

## Special vectors and matrices

MATLAB supplies you with a set of functions that allow to create vectors or matrices that have a special form. These functions are often useful to avoid unnecessary repetition of inputs.

**linspace and : operator**

The `linspace` command and the `:` operator allow to create row vectors of sequences that are linearly spaced. Consider first the `:` operator.

```text
a = 2:5                     % sequence from 2 to 5 in increments of 1
b = 2:3:11                  % sequence from 2 to 11 in increments of 3
c = 0:0.2:1                 % sequence from 0 to 1 in increments of 0.2
```

The `linspace(x1, x2, N)` command generates a row vector containing a sequence of N linearly spaced points between x1 and x2. If N is omitted, it generates 100 points.

```text
c = linspace(0, 1, 6)       % same as c above
d = linspace(2, 9, 3)       % sequence from 2 to 8 with 3 values
```

**logspace**

The logspace operators works the same way as the linspace operator, but it produces a sequence of uniformly spaced values in the log-10 space, i.e. logspace\(x1, x2, N\) generates N points between 10^x1 and 10^x2.

```text
e = logspace(0, 2, 4)       % logarithmically spaced values between 1 and 100
```

**zeros, ones, nan**

These commands create matrices of the supplied dimensions which are filled with 0, 1 or missing values \(nan = not a number\).

```text
A = zeros(2, 3)
B = ones(1, 4)
C = nan(2,2)
```

**eye**

eye\(n\) creates an identity matrix \(i.e. a square matrix with ones on the main diagonal and zeros everywhere else\) of dimension .

```text
eye(3)
```

**diag**

If X is a matrix, diag\(X\), returns the column vector which extracts the main diagonal of the matrix X. If x is a vectors, diag\(X\) returns a square diagonal matrix which has the vector x on its main diagonal

```text
X = [1, 2; 3, 4]
x = [2, 5];

diag(X)
diag(x)
```

**repmat**

repmat\(A, M, N\) replicates the vector/matrix A copy its rows M times and its columns N times.

```text
A = repmat([1, 2, 3], 4, 1)         % copy row vector a 4 times along rows
B = repmat([1 ,2; 3, 4], 2, 2)      % copy matrix 2 times along each dimension
```

**reshape**

reshape transforms a matrix into an matrix and can be used if the number of elements does not change i.e. if . It can e.g. be used to convert a matrix into a vector or vice versa.

```text
X = [1, 2, 3; 4, 5, 6]

reshape(X, 1, 6)        % reshape into 1x4 vector
reshape(X, 3, 2)        % reshape into 3x2 matrix
```

Note that for the reshape command, the elements retain their index in the matrix which is counted column-wise.

