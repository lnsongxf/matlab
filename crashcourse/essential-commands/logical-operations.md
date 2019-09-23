---
description: >-
  This section covers basic logical operators available in MATLAB as well as
  logical indexing and some basic logical functions.
---

# Logical Operations

## Basic logical operations

Logical operators in MATLAB are used to make comparisons between objects such as scalars, vectors or matrices. Logical operators are binary operators i.e. they return a boolean value which is either true \(which has numeric value 1\) or false \(which has numeric value 0\). When logical operators are applied to vectors, matrices or arrays, the operations are carried out element-by-element, therefore the matrices/vectors must have the same dimensions.

The basic logical operators are the following.

| **Math** | **MATLAB** | **Description** |
| :--- | :--- | :--- |
| $$>$$ | &gt; | Greater than |
| $$\geq$$ | &gt;= | Greater than or equal to |
| $$<$$ | &lt; | Less than |
| $$\leq$$ | &lt;= | Less than or equal to |
| $$=$$ | == | Equal to |
| $$\neq$$ | ~= | Not equal to |

Consider the following examples.

```text
% Scalar logical comparisons
x = 5;

x==2
x>=2
x<5

% Matrix logical comparisons
X = [1, 2; 3, 4];
X==2
X<=3
X~=1
```

## Combining logical expressions

Logical expressions can be combined to evaluate more complex conditions by chaining them using one of the following three operators.

| **Math** | **Array operator** | **Scalar operator** |
| :--- | :--- | :--- |
| AND | & | && |
| OR | \| | \|\| |
| NOT | ~ | ~ |

Eventhough the array operators can also be used when comparing two scalars, it is recommended to use the scalar operators in this case as they are computationally efficient. To understand better how these operators work, lets evaluate the following logic tables, by combining the elements of the following logical matrices which give all possible comparisons between two logical values.

```text
X = [0, 0;
     1, 1];
Y = [0, 1;
     0, 1];

X & Y                   % AND
X | Y                   % OR
~X                      % NOT
```

Consider the following examples for chaining logical expressions.

```text
x = [1, 2, 3, 4];
y = [0, 1, 5, 4];

(x>y) | (x==y)
(x>y) & (y~=2)
~(x>=2)
```

## Logical Indexing

We can use logical expressions to access elements of a vector or matrix. Instead of providing the numeric indices of which element to select, we provide a boolean true/false value for each element of the matrix, choosing whether it should be selected \(true i.e. 1\) or not \(false i.e. 0\). Consider the following examples.

```text
X = [1, 2; 3, 4];

X([true, false; true, false])       % select by boolean matrix
X(logical([1, 0; 1, 0]))            % equivalent

X((X>2) & X~=4)
```

Note here the use of the `logical` function in the second example which turns any numeric 1 into a boolean true \(boolean 1\) and any numeric 0 into a boolean false \(boolean 0\).

## Logical Functions

MATLAB provides some functions which are very useful when working with logical expressions. Here is a summary of the most important functions.

### **all and any**

`all(X)` and `any(X)` take a logical vector or matrix as an input and return column-by-column whether all elements of that column are true \(in the case of all\) and whether any element of that column is true. This can be particularly useful for checking whether a condition is met in the column of a matrix or the whole vector/matrix. It can also sometimes be useful to nests these commands to get more complex conditions.

```text
X = [1, 2;
     0, 2];

B = (X==0)
any(B)              % Is condition true for any element in column?
any(any(B))         % Is condition true for any element in matrix?

all(B)              % Is condition true for all elements in column?
all(all(B))         % Is condition true for all elements in matrix?

any(all(B))         % At least one column where all elements meet condition?
all(any(B))         % For all columns does at least one element meet condition?
```

### **is-functions**

MATLAB provides a collection of functions that can be used to check whether a vector/matrix has special characteristics. The details for each function should be checked by consulting the documentation or using the help command.

The following commands summarize properties of the whole matrix and hence return a scalar boolean value whether the condition is met or not.

* `isreal(X)` - Logical 1 if array is real-valued, 0 otherwise
* `ischar(X)` - Logical 1 if array is character array, 0 otherwise
* `isempty(X)` - Logical 1 if array is empty, 0 otherwise
* `isequal(X,Y)` - Logical 1 if all elements in array are equal, 0 otherwise
* `islogical(X)` - Logical 1 if array is a logical array, 0 otherwise
* `isscalar(X)` - Logical 1 if argument is scalar, 0 otherwise
* `isvector(X)` - Logical 1 if argument is row- or column-vector, 0 otherwise
* `isrow(x)` - Logical 1 if argument is a row-vector, 0 otherwise
* `iscolumn(x)` - Logical 1 if argument is a column-vector, 0 otherwise
* `ismatrix(X)` - Logical 1 if argument is matrix \(or vector\), 0 otherwise

Consider the following examples.

```text
A = [];
B = [1, 2; 3, 4];
C = [2, 2; 2, 2];
a = [1, 2, 3, 4];
b = [true, false];

isempty(A)
isempty(B)

isequal(B, C)
isequal(B, B)

isrow(a)
iscolumn(a)

islogical(b)
islogical(a)

ismatrix(B)
isvector(B)
isvector(a)
```

There are also logical functions which work element-by-element and hence output a matrix of the same dimensions as the input matrix.

* `isnan` - Logical 1 if element is NaN, 0 otherwise
* `isinf` - Logical 1 if element is Inf, 0 otherwise
* `isfinite` - Logical 1 if element is not Inf, 0 otherwise

Consider the following examples

```text
X = [1, NaN;
     Inf, 0];

isnan(X)
isinf(X)
isfinite(X)
```

### **find**

This is a very useful function that takes logical inputs and returns the matrix indices where the logical statement is true. There are two ways to call the function.

* `ix = find(B)` - saves indices of elements \(column-wise\) for which B is true
* `[ir, ic] = find(B)` - saves row and column indices of the elements for which B is true

```text
X = [1, 2;
     3, 4];
B = (X>1 & X<4)

ix = find(B)            % save overall index (columnwise)
[ir, ic] = find(B)      % save row and column indices separately
```

