---
description: >-
  This section familiarises you with basic matrix algebra operations in MATLAB.
  Together with the commands from the previous sections, they provide the
  fundamental building blocks of any MATLAB program.
---

# Matrix Algebra

## Standard Matrix operators

The following standard matrix operations from linear algebra are available in MATLAB: Transpose `'`, Addition `+`, Subtraction `-`, Multiplication `*` and Exponentiation `^`.

```text
A = [1, 2; 3, 4];
B = [1, 1; 2, 2];

A'                    % Matrix transpose

A * B                 % Matrix times matrix           
A * 2                 % Matrix times scalar

A + B                 % Matrix plus matrix
A + 1                 % Matrix plus scalar
0.5 - A               % Scalar minus matrix

A - B                 % Matrix minus matrix
A - 0.5               % Matrix minus scalar
1 - A                 % Scalar minus matrix

A^3                   % Matrix exponentiation (A*A*A)
```

Note that the typical restrictions on matrix dimension apply. For addition and subtraction, the matrices need to have the same dimensions or one input needs to be a scalar. For matrix multiplication, the inside dimension need to be the same or one input needs to be a scalar. For matrix exponentiation, at least the exponent needs to be a scalar.

### Left and right division

Eventhough matrix division is not defined in linear algebra, left and right division operators \(`\` and `/`\) can be used to solve linear equations or to calculate the inverse of a matrix.

Consider the linear matrix equation

$$B = AX$$

where $$A$$ is an $$n \times m$$ matrix, $$X$$ is an $$m \times l$$ matrix and $$B$$ is an $$n \times l$$ matrix.

To solve for $$X$$, we can use the matrix left division operator `\`.

Similarly, the matrix right division operator `/` can be used to solve for A in the equation above.

Consider the following example.

```text
A = [1, 2; 0, 1]
X = [2, 3; 1, 2]
B = A * X

A \ B                       % Same as X
B / X                       % Same as A
```

Note that there is also an inverse operator `inv(A)`. However this operator should not be used to solve a linear equation such as the one above by using `X=inv(A)*B` as it is computed in a different way and computationally less efficient.

### Matrix inverse

We can use the matrix left division operator `\` to efficiently solve for the matrix inverse of an invertible matrix $$A$$. Note that following the example above, if we set $$B=I$$, the left division operator solves for the inverse $$A^{-1}$$.

$$I = AX$$ 

$$X = A \backslash I$$

Consider the following example.

```text
A = [1, 2; 0, 1];

A \ eye(2)            % same as A^-1
inv(A)                % equivalent
A^(-1)                % equivalent
```

As you can see, the `inv(A)` operator also solves for the matrix inverse. `A^(-1)` is just another way of writing `inv(A)`.

### Dot operators

MATLAB also provides a set of matrix operators for element-wise operations. Note that to perform element-wise operations, the matrices involved need to have the same dimensions or at least one of them needs to be a scalar.

```text
A = [1, 2; 3, 4]
B = [1, 1; 2, 2]

A .* B             % Element-wise multiplication
1 ./ A             % Element-wise inverse

A ./ B             % Element-wise (right) division

A.\B               % Element-wise (left) division
B./A               % equivalent


A./2               % Element-wise division by scalar
A/2                % equivalent
```

## Basic matrix functions

MATLAB provides a wide array of matrix functions. All functions in MATLAB follows one of the following syntaxes.

```text
out1 = functionname(in1)
[out1, out2, ...] = functionname(in1, in2, ...)
```

where `in1, in2, ...` denote the arguments of the function and `out1, out2, ...` are the outputs of the functions.

To see the brief summary of any function, enter

```text
help functionname
```

into the command window. Alternatively, enter

```text
doc functionname
```

into the command window to see the detailed documentation and examples.

### **length**

`length(X)` returns the maximum dimension of the vector/matrix X which can be either the number of rows or number of columns, depending on which is larger.

```text
A = ones(3, 2);
B = zeros(1, 4);
C = nan(2, 4);
D = 5;

length(A)
length(B)
length(C)
length(D)
```

### **size**

`size(X)` returns the dimensions of the supplied array `X`. `size(X, dim)` returns the size of dimension `dim`.

```text
A = ones(3, 2);

d = size(A)
[r, c] = size(A)
size(A, 1)
size(A, 2)
```

### **min, max**

`min(X), max(X)` compute the minimum or maximum elements of matrix `X` column-by-column. By wrapping multiple calls of min or max, we can compute the minimal or maximal element of a matrix.

```text
X = [1, 4; 3, 2]
min(X)              % row vector of column-minimal elements
max(X)              % row vevtor of column-maximal elements

min(min(X))         % scalar minimal element
max(max(X))         % scalar maximal element
```

### **sum**

`sum(X)` returns a row vector which contains the column-wise sum of the matrix X.

```text
X = [0, 4; 3, 2]
y = [1, 2, 3]'

sum(X)
sum(y)
```

### prod

`prod(X)` returns a row vector which contains the column-wise product of the matrix `X`. `prod(X,dim)` computes the product of the elements of dimension `dim`.

```text
X = [1, 4; 0.5, 2]
y = [1, 0.5, 3]'

prod(X)                 % product over rows (columnwise)
prod(X, 1)              % equivalent
prod(X, 2)              % product over columns (rowwise)

prod(y)
```

### **mean**

`mean(X)` returns a row vector which contains the column-wise mean of the matrix `X`. `mean(X, dim)` returns a vector of means computed over dimension `dim`.

```text
X = [1, 4; 0.5, 2]
y = [1, 0.5, 3]'

mean(X)                 % mean over rows (columnwise)
mean(X, 1)              % equivalent
mean(X, 2)              % mean over columns (rowwise)

mean(y)
```

### **var**

`var(X)` returns a row vector which contains the column-wise variance of the matrix `X`. `var(X,[],dim)` returns a vector of variances computed over dimension `dim`.

```text
X = [1, 4; 0.5, 2]
y = [1, 0.5, 3]'

var(X)                 % mean over rows (columnwise)
var(X, [], 1)              % equivalent
var(X, [], 2)              % mean over columns (rowwise)

var(y)
```

### **std**

`std(X)` returns a row vector which contains the column-wise standard deviation of the matrix `X`. `std(X,dim)` returns a vector of standard deviations computed over dimension `dim`.

```text
X = [1, 4; 0.5, 2]
y = [1, 0.5, 3]'

std(X)                 % mean over rows (columnwise)
std(X, [], 1)          % equivalent
std(X, [], 2)          % mean over columns (rowwise)

std(y)
```

### **sqrt, exp and log**

If applied to a matrix X, these functions are applied element-by-element.

```text
X = [1, 2; 3, 4]

sqrt(X)
exp(X)
log(X)
```

### **Other functions**

Here are some examples of other linear algebra matrix functions which are often used.

* `chol(X)` - Compute Cholesky-factor of pos. def. matrix
* `det(X)` - Compute determinant of square matrix
* `trace(X)` - Compute the trace of square matrix
* `eig(X)` - Compute eigenvalues and -values of square matrix
* `kron(x, y)` - Compute Kronecker product of x and y

