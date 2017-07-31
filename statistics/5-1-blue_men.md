[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

The percentage of US males that fall between 5'10" and 6'1" is approximately 34%.

Code below:

```python
import pandas
import thinkstats2
import thinkplot
import scipy
%matplotlib inline 

def ReadBrfss(filename='CDBRFS08.ASC.gz', compression='gzip', nrows=None):
    """Reads the BRFSS data.

    filename: string
    compression: string
    nrows: int number of rows to read, or None for all

    returns: DataFrame
    """
    var_info = [
        ('age', 101, 102, int),
        ('sex', 143, 143, int),
        ('wtyrago', 127, 130, int),
        ('finalwt', 799, 808, int),
        ('wtkg2', 1254, 1258, int),
        ('htm3', 1251, 1253, int),
        ]
    columns = ['name', 'start', 'end', 'type']
    variables = pandas.DataFrame(var_info, columns=columns)
    variables.end += 1
    dct = thinkstats2.FixedWidthVariables(variables, index_base=1)

    df = dct.ReadFixedWidth(filename, compression=compression, nrows=nrows)
    CleanBrfssFrame(df)
    return df

def CleanBrfssFrame(df):
    """Recodes BRFSS variables.

    df: DataFrame
    """
    # clean age
    df.age.replace([7, 9], float('NaN'), inplace=True)

    # clean height
    df.htm3.replace([999], float('NaN'), inplace=True)

    # clean weight
    df.wtkg2.replace([99999], float('NaN'), inplace=True)
    df.wtkg2 /= 100.0

    # clean weight a year ago
    df.wtyrago.replace([7777, 9999], float('NaN'), inplace=True)
    df['wtyrago'] = df.wtyrago.apply(lambda x: x/2.2 if x < 9000 else x-9000)
    
df = ReadBrfss()
CleanBrfssFrame(df)
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
