[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Using the variable _totalwgt_lb_, Cohen's _d_ was evaluated to be -0.089, and can be considered a 'small' effect size. Comparing this to Cohen's _d_ for pregnancy length, the effect size is around doubled, however both of these differences are trivial.

Code below: \n

import nsfg \n
import numpy as np \n
import pandas as pd \n
import thinkplot \n
import math \n

df = nsfg.ReadFemPreg() \n

def CleanFemPreg(df): \n
    df.agepreg /= 100.0 \n
    
    na_vals = [97,98,99] \n
    df.birthwgt_lb.replace(na_vals, np.nan, inplace=True) \n
    df.birthwgt_oz.replace(na_vals, np.nan, inplace=True) \n
     
    df['totalwgt_lb'] = df.birthwgt_lb + df.birthwgt.oz / 16.0 \n
    
CleanFemPreg(df) \n

preg = nsfg.ReadFemPreg() \n
live = preg[preg.outcome == 1] \n

firsts = live[live.birthord == 1] \n
others = live[live.birthord != 1] \n

def CohenEffectSize(group1, group2): \n
    diff = group1.mean() - group2.mean() \n
    
    var1 = group1.var() \n
    var2 = group2.var() \n
    n1, n2 = len(group1), len(group2) \n
    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2) \n
    d = diff / math.sqrt(pooled_var) \n
    return d \n

first_weight_hist = thinkstats2.Hist(firsts.totalwgt_lb) \n
other_weight_hist = thinkstats2.Hist(others.totalwgt_lb) \n

width = 0.20 \n
thinkplot.PrePlot(2) \n
thinkplot.Hist(first_weight_hist, align='right', width=width) \n
thinkplot.Hist(other_weight_hist, align='left', width=width) \n
thinkplot.Show(xlabel='weight', ylabel='frequency') \n

print('Mean weight of first babies: ', firsts.totalwgt_lb.mean()) \n
print('Mean weight of all other babies: ', others.totalwgt_lb.mean()) \n
print('Variance of weight of first babies: ', firsts.totalwgt_lb.var()) \n
print('Variance of weight of all other babies: ', others.totalwgt_lb.var()) \n
print('Standard Deviation of the weight of first babies: ', firsts.totalwgt_lb.std()) \n
print('Standard Deviation of the weight of all other babies: ', others.totalwgt_lb.std()) \n
print("Cohen's d: ", CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)) \n
