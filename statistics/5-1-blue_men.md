[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

The percentage of US males that fall between 5'10" and 6'1" is approximately 34%.

Code below:

```python
import pandas
import thinkstats2
import thinkplot
import scipy
import brfss
%matplotlib inline 
    
df = brfss.ReadBrfss()
brfss.CleanBrfssFrame(df)
male = df[df.sex == 1]

male_height = male.htm3

male_mean = male.htm3.mean()
male_std = male.htm3.std()

cdf = thinkstats2.Cdf(male_height)
thinkplot.Cdf(cdf)
thinkplot.Config(xlabel='male height (cm)', 
                 ylabel='CDF', 
                 title='Male Height')

z2 = (185.42-male_mean)/male_std
z1 = (177.8-male_mean)/male_std

male_range = (scipy.stats.norm.cdf(z2) - scipy.stats.norm.cdf(z1)) * 100
print('% of US male population in range: ', male_range)
```
