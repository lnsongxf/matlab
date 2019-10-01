---
description: >-
  This section provides some exercises that are meant to deepen your knowledge
  in the topics covered in this section and to gain experience solving
  real-world problems.‌
---

# Applied Exercises

## 1. Getting familiar with data imports and descriptive analysis

In this exercise you will download some data of your choice from popular statistical databases and conduct descriptive analysis using MATLABs graphical engine. Try this exercise multiple times varying data source, the dataset and the data format until you get comfortable with handling and plotting data in MATLAB.

{% tabs %}
{% tab title="Exercise" %}
1\) Download a dataset of your choice in either .csv or .xls/.xlsx format from one of the following statistical databases.

* [FRED \(Federal Reserve Bak of St. Louis\)](https://fred.stlouisfed.org/)
* [BLS \(US Bureau of Labor Statistics\)](https://www.bls.gov/data/)
* [ECB Statistical Data Warehouse](https://sdw.ecb.europa.eu/)
* [EUROSTAT](https://ec.europa.eu/eurostat/data/database)
* [FRED-MD/FRED-QD](https://research.stlouisfed.org/econ/mccracken/fred-databases/)
* [World Bank Database](https://data.worldbank.org/)
* [IMF \(International Monetary Fund\)](https://www.imf.org/en/Data)

2\) Inspect the file using a text editor and decide which is the best way to import it into MATLAB?

3\) Use the commands you learned in this unit to import the data. 

4\) Use MATLABs graphical engine to generate interesting plots of varying plot type etc. Make sure your label your axis appropriately, add titles and legends etc.
{% endtab %}
{% endtabs %}

## 2. Plotting the evolution of the economy in the canonical OLG model

{% tabs %}
{% tab title="Exercise" %}
Simulate the evolution of the economy for each variable, saving it in a different vector when the initial capital stock per worker is $$k_0=0.1$$ and initial population size is $$L_1=1$$. Create a 4 by 4 plot that shows the evolution of capital per worker, output, wages and return to capital side by side. For each plot, label the variable and axis appropriately.

Use the following parameter values.

| **Parameter** | **Value** |
| :--- | :--- |
| $$A$$ | 4 |
| $$\alpha$$ | 0.4 |
| $$\beta$$ | 0.9 |
| $$n$$ | 0.02 |
| $$\delta$$ | 0.5 |

**Tip:** Use the `subplot` command to create the 4x4 plot matrix.
{% endtab %}
{% endtabs %}

### Theory

In the canonical overlapping-generations \(OLG\) model, the evolution of the capital stock per worker is described by the following law of motion.

$$k_{t+1} = \frac{1}{1+n} \frac{\beta}{1+\beta} \; (1-\alpha) \; A \; k_t^\alpha$$

where $$k$$ is the capital per worker, $$n$$ is the population growth rate, $$\beta$$ is the discount factor, $$\alpha$$ is the capital share in the production function and $$A$$ is the TFP parameter from the production function.

The population stock $$L$$ is described by the following law of motion.

$$L_{t+1} = (1+n) \; L_t$$

Output of the economy \($$Y$$\), wages of the workers \($$w$$\) and return to capital $$R$$ are described by the following equations.

$$Y = A L^{1-\alpha} K^\alpha$$ 

$$w = (1-\alpha) \frac{Y}{L}$$

 $$R = (1-\delta) + \alpha \frac{Y}{K}$$

