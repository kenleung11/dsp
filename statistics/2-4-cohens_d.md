[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Using the variable _totalwgt_lb_, Cohen's _d_ was evaluated to be -0.089, and can be considered a 'small' effect size. Comparing this to Cohen's _d_ for pregnancy length, the effect size is around doubled, however both of these differences are trivial.  

Code below:  
```python
import nsfg
import thinkstats2
import numpy as np  
import pandas as pd  
import thinkplot  
import math  

df = nsfg.ReadFemPreg()  

def CleanFemPreg(df):  
    df.agepreg /= 100.0  
    
    na_vals = [97,98,99]  
    df.birthwgt_lb.replace(na_vals, np.nan, inplace=True)  
    df.birthwgt_oz.replace(na_vals, np.nan, inplace=True)  
     
    df['totalwgt_lb'] = df.birthwgt_lb + df.birthwgt.oz / 16.0  
    
CleanFemPreg(df)  

preg = nsfg.ReadFemPreg()  
live = preg[preg.outcome == 1]  

firsts = live[live.birthord == 1]  
others = live[live.birthord != 1]  

def CohenEffectSize(group1, group2):  
    diff = group1.mean() - group2.mean()  
    
    var1 = group1.var()  
    var2 = group2.var()  
    n1, n2 = len(group1), len(group2)  
    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)  
    d = diff / math.sqrt(pooled_var)  
    return d  

first_weight_hist = thinkstats2.Hist(firsts.totalwgt_lb)  
other_weight_hist = thinkstats2.Hist(others.totalwgt_lb)  

width = 0.20  
thinkplot.PrePlot(2)  
thinkplot.Hist(first_weight_hist, align='right', width=width)  
thinkplot.Hist(other_weight_hist, align='left', width=width)  
thinkplot.Show(xlabel='weight', ylabel='frequency')  

print('Mean weight of first babies: ', firsts.totalwgt_lb.mean())  
print('Mean weight of all other babies: ', others.totalwgt_lb.mean())  
print('Variance of weight of first babies: ', firsts.totalwgt_lb.var())  
print('Variance of weight of all other babies: ', others.totalwgt_lb.var())  
print('Standard Deviation of the weight of first babies: ', firsts.totalwgt_lb.std())  
print('Standard Deviation of the weight of all other babies: ', others.totalwgt_lb.std())  
print("Cohen's d: ", CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb))  
```
