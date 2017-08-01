[Think Stats Chapter 7 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2008.html#toc70) (weight vs. age)

The result from Pearson's correlation (0.0688) and Spearman's correlation (0.0946) suggest a weak relationship between the variables. The result from the scatterplot also supports this conclusion. Plotting the percentiles of weights versus age shows a slight relationship between mother's age and baby's weight for ranges of age between 15 and 25, but the relationship tapers off at higher ages.

Code below:

```python
import first
import nsfg
import numpy as np
import pandas as pd
import thinkstats2
import thinkplot

%matplotlib inline

def Cov(xs, ys, meanx=None, meany=None):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    if meanx is None:
        meanx = np.mean(xs)
    if meany is None:
        meany = np.mean(ys)

    cov = np.dot(xs-meanx, ys-meany) / len(xs)
    return cov

def Corr(xs, ys):
    xs = np.asarray(xs)
    ys = np.asarray(ys)

    meanx, varx = thinkstats2.MeanVar(xs)
    meany, vary = thinkstats2.MeanVar(ys)

    corr = Cov(xs, ys, meanx, meany) / np.sqrt(varx * vary)
    return corr

def SpearmanCorr(xs, ys):
    xranks = pd.Series(xs).rank()
    yranks = pd.Series(ys).rank()
    return Corr(xranks, yranks)

live, firsts, others = first.MakeFrames()
live = live.dropna(subset=['agepreg', 'totalwgt_lb'])

ages = live.agepreg
weights = live.totalwgt_lb

print('Pearson correlation: ', Corr(ages, weights))
print('Spearman correlation: ', SpearmanCorr(ages, weights))

bins = np.arange(10, 48, 3)
indices = np.digitize(live.agepreg, bins)
groups = live.groupby(indices)

ages_group = [group.agepreg.mean() for i, group in groups][1:-1]
cdfs = [thinkstats2.Cdf(group.totalwgt_lb) for i, group in groups][1:-1]

thinkplot.PrePlot(3)
for percent in [75, 50, 25]:
    weights_group = [cdf.Percentile(percent) for cdf in cdfs]
    label = '%dth' % percent
    thinkplot.Plot(ages_group, weights_group, label=label)

thinkplot.Config(xlabel="mother's age",
                 ylabel="baby's weight (kg)",
                 xlim=[14, 45],
                 ylim=[6, 8.5], 
                 legend=True)
               
thinkplot.Scatter(ages, weights, alpha=0.05)
thinkplot.Config(xlabel="mother's age",
                 ylabel="baby's weight (kg)",
                 xlim=[10, 45],
                 ylim=[0, 15])
```
