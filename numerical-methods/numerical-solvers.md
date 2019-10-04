---
description: This section reviews numerical solvers in MATLAB.
---

# Numerical Solvers

A very useful feature of Matlab is its ability to find solutions to nonlinear equations and, more generally, systems of nonlinear equations.

## Finding the root of a nonlinear function

The function `fzero` searches for a point $$x$$ where target\_function$$(x)=0$$. It stops searching once it finds a point where the function changes sign. This can be highly useful for example to find solutions to first order conditions.

The syntax for using `fzero` is

```text
[x,fval,exitflag] = fzero(@function,x0,options)
```

where $$x$$ is the solution, `fval` the value of the function at the solution, `exitflag` gives the exit condition, `function` is our function of interest, $$x0$$ is the starting value \(can be a single point or an interval\), and options specifies the options of `fzero` to be used.

Say, for example, if we want to find the root of the sine function close to 3 we write

```text
options = optimset('fzero');
options = optimset(options,'Display','iter');
[x,fval,exitflag] = fzero(@sin,3,options)
```

Likewise, instead of looking close to 3 we can specify a range by writing

```text
[x,fval,exitflag] = fzero(@sin,[2.5,3.5],options)
```

However, if the function of interest has hyperparameters we need to make an extra step. Take our univariate function from the previous section, $$f(x) = a + bx+cx^2$$. The first order conditions are then $$b+2cx = 0$$ which we can solve with `fzero` but we need to specify the values of $$b$$ and $$c$$. We can write

```text
options = optimset('fzero');
options = optimset(options,'Display','iter');
myfun = @(x,b,c) b+2*c*x;
b = 2;
c = 1.5;
fun = @(x) myfun(x,b,c)
[x,fval,exitval] = fzero(fun,-1,options)
```

A short cut could be to write

```text
options = optimset('fzero');
options = optimset(options,'Display','iter');
b = 2;
c = 1.5;
[x,fval,exitval] = fzero(@(x) b+2*c*x,-1,options)
```

## Solving systems of nonlinear equations

Often the problems we face are not simply a function of a single variable but are rather systems of nonlinear equations. To solve these problems we can use the `fsolve` function which solves $$F(x)=0$$ for $$x$$ \(which is a vector or matrix\), where $$F(x)$$ is a function returning a vector value. The syntax is comparable to that of `fzero`, that is

```text
[x,fval,exitflag] = fsolve(@function,x0,options)
```

where $$x$$ is the solution, `fval` the value of the function at the solution, `exitflag` gives the exit condition, `function` is our function of interest, `x0` is the starting value, and options specifies the options of `fsolve` to be used.

Say that we have a system of two equations in two variables:

$$exp(-x) = y^2$$

$$y cos(x) = 1$$

To solve this system we first need to convert the system to the form $$F(X)=0$$ and write a function that calculates the left-hand side of the the equation:

```text
function F = d2roots(z)
F(1) = exp(-z(1)) - z(2)^2;
F(2) = z(2)*cos(z(1)) - 1;
end
```

Then we can pass the function to `fsolve` to obtain the solution:

```text
options = optimset('fsolve');
options = optimset(options,'Display','iter');
z0 = [0,0];
[z,fval,exitval] = fsolve(@d2roots,z0,options)
```

### Solving a New Keynesian model using `fsolve`

The basic New Keynesian model consists of three core equations:

$$ \pi_t = \beta E_t \pi_{t+1}+\kappa y_t$$ \(The NK Phillips curve\)

$$ y_t = E_t y_{t+1} - \sigma^{-1}(i_t - E_t \pi_{t+1}-\rho+z_t)$$ \(The Dynamic IS equation\)

$$ i_t = \rho + \phi_{\pi}\pi_t + \phi_y y_t$$ \(Monetary policy\)

where $$\pi_t$$ _denotes the inflation rate,_ $$y_t$$ _the output gap,_ $$i_t$$ _the nominal interest rate and_ $$z_t$$ _is a "financial shock" which evolves according to the process_ $$z_t = \rho_z z_{t-1} + \epsilon_t$$ _where_ $$\epsilon_t$$ _is an iid random variable with zero mean and standard deviation_ $$\sigma_{\epsilon}$$.

We consider a finite horizon version of the model and use `fsolve` to solve the system and give us the impulse response of a one standard deviation decrease in $$\epsilon_t$$ _\(i.e.,_ $$\epsilon_0 = -\sigma_{\epsilon}$$, $$\epsilon_t = 0  \ \  \forall t>0$$\) for the parameter values

| $$\beta$$ | $$\kappa$$ | $$\sigma$$ | $$\phi_{\pi}$$ | $$\phi_y$$ | $$\rho_z$$ | $$\sigma_{\epsilon}$$ | $$\rho$$ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0.99 | 0.17 | 1 | 1.5 | 1/8 | 0.8 | 0.02 | $$-log(\beta)$$ |

We begin by setting up our target function \(recall that our target function needs to have all the choice parameters as the first input\):

```text
function out = BNK_mdl(x,T,nvar,zshock)
        % Parameters
        betta = 0.99;        % discount factor
        rho = -log(betta);   % steady state interest rate
        kappa = 0.17;       % slope of the NK Phillips curve
        sigma = 1;          % CRRA coefficient
        phipi = 1.5;        % CB weight on inflation
        phiy = 1/8;         % CB weight on output

        % Define variables
        x = reshape(x,T,nvar);
        pi = x(:,1);
        y = x(:,2);
        int = x(:,3);

        % Create the forward terms
        pi_next = [pi(2:end);0];    % The steady state pi=0 is the terminal condition
        y_next = [y(2:end);0];      % The steady state y=0 is the terminal condition

        % Equations being solved
        z(:,1) = -pi + betta*pi_next + kappa*y;                          % NK Phillips curve
        z(:,2) = -y + y_next - 1/sigma.*(int - pi_next - rho + zshock); % DIS equation
        z(:,3) = -int + rho + phipi*pi + phiy*y;                        % Monetary Policy Rule

        out=z(:); % stack the columns to output a column vector
end
```

And now, to solve the model and to plot the impulse responses we run the following:

```text
%% Solve the model
% Set the options for the root finding algorithms
options = optimset('fsolve');
option=optimset(options,'MaxFunEvals',200000,'MaxIter',10000,'TolFun',1e-8,'TolX',1e-8, 'Display','iter');

% Specify some variables
T = 30; % Number of periods
nvar = 3; % Number of variables
varnames = char('Inflation','Output Gap','Int.rate');

% Create the path of the financial shock
rhoz = 0.8;         % persistence of financial shock
sige = 0.02;        % s.d. of innovation of financial shock
zshock = NaN(T,1);
zshock(1,1) = -sige;
for i = 2:T
    zshock(i,1) = rhoz*zshock(i-1,1);
end

%% Solve model using
xstart = zeros(nvar*T,1);                   % initial guess
solpath = fsolve(@(x) BNK_mdl(x,T,nvar,zshock),xstart(:),option); % find solution

%% Plot solutions
solpath = reshape(solpath,T,nvar);
% Plot solutions using fsolve
figure('Name','Using fsolve')
for i=1:nvar
    subplot(2,2,i)
    plot([0:T-1], solpath(:,i),'.-');
    title(varnames(i,:));
    xlabel('Period');
    ylabel('Impact');
end
subplot(2,2,4)
plot([0:T-1], zshock,'.-');
title('Financial shock');
xlabel('Period');
ylabel('Impact');
```

