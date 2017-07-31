[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

From the PMF, you can see that all random variates are represented with equal probability, and the CDF is approximately a straight line, which means that the distribution is uniform.

Code below:

```python
import numpy as np
import thinkstats2
import thinkplot
import random
%matplotlib inline 

sample = np.random.random(1000)

pmf = thinkstats2.Pmf(sample)
thinkplot.Pmf(pmf, linewidth=0.05)
thinkplot.Config(xlabel='Random variate', ylabel='PMF')

cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Random variate', ylabel='CDF')
```
