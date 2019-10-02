# Monte-Carlo Simulations

If we know how to generate random numbers we can perform Monte Carlo simulations. The main idea behind the method is to generate results based on repeated random sampling and statistical analysis.

In general, Monte Carlo methods follow the following pattern 

1. The domain of possible inputs is defined
2. These inputs are generated randomly from a probability distribution defined over the domain
3. Some deterministic computation is performed on the inputs
4. Results are aggregated

Sawilowsky \(2003\) distinguishes between a simulation, a Monte Carlo method, and a Monte Carlo simulation. While a simulation is a fictitious representation of a real world phenomena, the Monte Carlo method is simply a technique to solve mathematical or statistical problems. Thus a Monte Carlo simulation is the use of repeated sampling to obtain the statistical properties of some real world phenomenon. Examples:

* **Simulation**: Drawing one pseudo-random uniform integer variable from the interval \[1,6\] can be used to simulate the tossing of a die. This is a simulation but not a Monte Carlo simulation
* **Monte Carlo method**: Pouring out a box of dice on a table, then computing the ratio of each number that comes up is a Monte Carlo method of determining the behaviour of repeated die tosses but is not a simulation.
* **Monte Carlo simulation**: Drawing a large number of pseudo random uniform integer variables from the interval \[1,6\] at one time, is a Monte Carlo simulation of the behaviour of repeatedly tossing a die.

Lets perform this Monte Carlo simulation just described. The following \(inefficient\) code can answer the question of how a die would behave if repeatedly tossed

```text
n_sim = 100;
nmbr = NaN(n_sim,1);
for i = 1:n_sim
  nmbr(i) = randi(6);
end
histogram(nmbr)
```

We can also use Monte Carlo simulation to approximate $$\pi$$. Recall that the area of a circle with radius $$r$$, is $$A_c = \pi r^2$$. We can put this circle inside of a square whos sides have length $$2r$$ and thus an area of $$A_s = 4r^2$$. Now imagine that we draw a random point inside this square. The probability of this point being within the circle is $$Pr($$Point inside circle$$) = \pi r^2 / 4 r^2$$ and thus we can express $$\pi$$ as $$\pi = 4 Pr($$Point inside circle$$)$$. We can use Monte Carlo simulation to approximate the probability and thus to get an approximation of $$\pi$$. We proceed as follows:

{% code-tabs %}
{% code-tabs-item title="sim\_approx\_pi.m" %}
```text
n_sim = 100; % number of monte-carlo replications

x = 2*rand(n_sim,1); % draw random x
y = 2*rand(n_sim,1); % draw random y

r = (x-1).^2 + (y-1).^2; % subtract 1 to centre on (1,1)

figure('color','white');
hold all
axis square;
box on;

ii = (r<=1);
m = sum(ii);
plot(x(ii),y(ii),'.b');
plot(x(~ii),y(~ii),'.r');
rectangle('Position',[0 0 2 2],'Curvature',[1,1]);
piapprox = 4*(m/n_sim);
titlelstr = sprintf('Pi is approx. %g', piapprox);
title(titlestr)

fprintf('Pi is approx. %g based on %g draws.\n', piapprox, n_sim)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## "Test" of the Central Limit Theorem

Recall that the central limit theorem states that the sample mean \(scaled by sqrt\(n\)\) of iid random variables with zero mean and unit variance converges in distribution to the standard normal distribution.

Lets test this numerically using Monte Carlo Simulation. We begin by generating a large number of samples, calculate the mean within each sample and then compare the CDF of the means to that of the standard normal.

```text
n = 50 % size of each sample
R = 1000 % the number of samples to generate

x = randn(n,R); % generate data using a standard normal distribution
m = mean(x); % calculate the mean within each sample

s = sqrt(n)*sort(m); % sort the means by size in order to plot properly
cdfplot(s); % CDF plot of the means
hold all;
plot(s,cdf('Normal',s,0,1)); % cdf plot of N(0,1)
legend('cdf of means','cdf of N(0,1)','Location','SouthEast');
```

As we can see from running the code, the cdfs are very close and become closer as we increase the sample size.

## Uses in econometrics

The same idea can be used to simulate the distributions of parameter estimates, test statistics, and other statistics, as discussed in the exercises.

