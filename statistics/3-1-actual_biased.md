[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

The unbiased mean number of children per household is 1.02 while the biased mean number of children per household is 2.4. The code is shown below:

```python

import nsfg
import thinkstats2
import thinkplot
%matplotlib inline 

def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    
    new_pmf.Normalize()
    return new_pmf

sample = nsfg.ReadFemResp()

pmf = thinkstats2.Pmf(sample.numkdhh, label='numkdhh')

thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

biased = BiasPmf(pmf, label='biased')

thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

print('Unbiased mean: ',pmf.Mean())
print('Biased mean: ', biased.Mean())

```
