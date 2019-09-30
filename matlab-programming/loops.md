---
description: This section covers the basics of loops in MATLAB.
---

# Loops

Loops in MATLABs typically come in two forms: _For-loops_ and _While-loops_.

### For-loops

For loops iterate over a predetermined set of values \(e.g. a counter\) and execute a code block as many times as there are elements in the set. The basic syntax of a for loop is the following.

```text
for iterator=vector
    Code block
end
```

`iterator` is a variable that takes on the value of the current element in vector at which the loop is currently running.

To familiarise yourself with the concept of a for-loop consider the following example.

```text
for i=1:5
    i
end
```

### While-loops

While loops iterate over a code block as long as a boolean condition returns `true`.

The basic syntax of a while-loop in MATLAB is the following.

```text
while condition
    code_block
end
```

**Important:** Choose the condition carefully! If the condition never returns `true`, the loop will never stop.

### **Example: Finding root of 2 by an easy numeric algorithm**

While loops are often used to code algorithms which iterate on a number of steps. Take a look at the following example for an easy numeric algorithm where we try to evaluate when $$x^2$$ is equal to 2 i.e we wish to find the square root of 2. We will use the following algorithm.

Start at a guess $$x=5$$ and subtract $$x/10$$ until we reach the point where $$x^2=2$$ up to a tolerance of 1e-2.

```text
x = 5;
fx = 25;
converged = false;

i = 1;
while converged==false

    x_new = x - x/10;
    fx = x_new^2;

    fprintf('Iteration %g - x=%g, f(x)=%g\n', i, x_new, fx)

    if abs(fx - 2)<1e-2
        converged = true;
    end

    x = x_new;
    i = i + 1;
end
```

To see the danger of while loops, change the tolerance to 1e-3 and run the script again.

