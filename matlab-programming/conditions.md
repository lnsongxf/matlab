---
description: >-
  In this section we will cover cover conditions which allow to execute a code
  block only when certain conditions are met.
---

# Conditions

Conditions in MATLAB generally take one of the following forms:

* if-conditions
* if-else conditions
* if-elseif-else conditions
* switch-case conditions

### **if-condition**

```text
if condition
   <Code block>
end
```

The code block is only executed when the condition returns true, otherwise the code block is skipped.

### **if-else condition**

```text
if condition
   <Code block A>
else
   <Code block B>
end
```

In an if-else condition, if the condition returns true, code block A is executed and the rest is skipped. Otherwise, if the condition returns false, code block B is executed.

### **if-elseif-else**

```text
if condition A
   <Code block A>
elseif condition B
   <Code block B>
elseif condition C
   <Code block C>
...
else
   <Alternative code block>
end
```

If the condition is met, code block A is executed and the rest is skipped. Otherwise, if condition B is true, code block B is executed and the rest is skipped. Otherwise, condition C is check etc... If none of the conditions returns true, the alternative code block in the else part is executed.

Note that it is also possible to nest several conditions to create more complex programs.

To familiarise yourself with if-conditions, consider the following examples. Try changing the value of x and see which statements are executed.

```text
x = 3;      % change this value and re-run cell
y = 6;      % chante this value and re-run cell

if (x<7)
    if (y<=3)
        sprintf('x is smaller than 7')
        sprintf('y is smaller than or equal to 3.')
    else
        sprintf('x is smaller than 7.')
        sprintf('y is larger than 3.')
    end
elseif x==7
    sprintf('x is equal to 7.')
else
    sprintf('x is larger than 7.')
end
```

### Switch-case conditions

Sometimes we would like to be able to check for many different conditions without writing a lot of if-elseif-else conditions. MATLAB provides the switch-case-otherwise conditions which are particularly usefule to check whether a variable takes on a specific value.

```text
switch variable
    case value1
        block A
    case {value2, value3}
        block B
    case value4
        block C
    ...
    otherwise
        alternative block
end
```

Note that the cases can easily contain several valid values as in the case of block B without having to write OR conditions.

Consider the following example.

```text
x = 7;      % change this value and re-run cell

switch x
    case 3
        sprintf('x is equal to 3.')
    case 7
        sprintf('x equal to 7.')
    otherwise
        sprintf('x is not 3 and not 7.')
end
```

Note that if we want to check for inequalities, we need to create boolean variables prior to the switch-case-otherwise statement that tell us whether the condition is met. Therefore, in the case of inequalities it is recommended to use `if-elseif-else` clauses.

