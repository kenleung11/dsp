[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

The mean and median household income is calculated to be $74,278 and $51,226 respectively. The sample skewness is calculated to be 4.95, which suggests that the distribution is skewed to the right. Pearson's skewness is calculated to be 0.74, which also indicates a skewness to the right, but the strength is less apparent than the sample skewness. Approximately 66% of households fall below the mean. 

All of these values greatly depend on the assumed upper bound. If the upper bound was increased by a multiple of 10 (to $10 million), the fraction of households that fall below the mean increases to 86%.

```python
import hinc
import hinc2
import thinkstats2
import thinkplot
import numpy as np

%matplotlib inline

def RawMoment(xs, k):
    return sum(x**k for x in xs) / len(xs)

def Mean(xs):
    return RawMoment(xs, 1)

def CentralMoment(xs, k):
    mean = RawMoment(xs, 1)
    return sum((x - mean)**k for x in xs) / len(xs)

def Var(xs):
    return CentralMoment(xs, 2)

def StandardizedMoment(xs, k):
    var = CentralMoment(xs, 2)
    std = np.sqrt(var)
    return CentralMoment(xs, k) / std**k

def Skewness(xs):
    return StandardizedMoment(xs, 3)

def Median(xs):
    cdf = thinkstats2.Cdf(xs)
    return cdf.Value(0.5)

def PearsonMedianSkewness(xs):
    median = Median(xs)
    mean = RawMoment(xs, 1)
    var = CentralMoment(xs, 2)
    std = np.sqrt(var)
    gp = 3 * (mean - median) / std
    return gp

df = hinc.ReadData()
log_sample = hinc2.InterpolateSample(df, log_upper=6.0)

log_cdf = thinkstats2.Cdf(log_sample)
thinkplot.Cdf(log_cdf)
thinkplot.Config(xlabel='Household income (log $)',
                 ylabel='Log CDF',
                 title = 'Household income')
                 
sample = np.power(10, log_sample)

cdf = thinkstats2.Cdf(sample)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='Household income ($)',
                 ylabel='CDF',
                 title = 'Household income')

print('Mean: ', Mean(sample))
print('Median: ', Median(sample))
print('Sample skewness: ', Skewness(sample))
print('Pearsons skewness: ', PearsonMedianSkewness(sample))

print('Fraction of households below mean: ', cdf.Prob(Mean(sample)))
```
