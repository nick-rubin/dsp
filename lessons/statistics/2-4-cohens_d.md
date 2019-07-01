[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

The problem here is two-fold, first determining what the best analytical approach might be to find out if first babies are lighter or heavier than non-first babies, the second being to compare the difference between the two to the difference in pregnancy length. To tackle the first problem, it might be best to simply compare the mean of both categories, but the median might also prove helpful. Rather than the average, the median would provide the point in the distribution where a babies' weight is equally likely to be above and below it. Regardless of the median's importance  the tool we'll be using to compare the two will be Cohen's *d*, which uses mean in its calculations, so while I'll be presenting the median below for context, it's important to note the mean will be what we use.



These analyses are fairly simple in python (I've rounded to 4 significant figures):

**Mean difference**: (7.201, 7.326)
~~~
round(firsts.totalwgt_lb.mean(),3), round(others.totalwgt_lb.mean(),3)
~~~
**Median difference**: (7.312, 7.375)
~~~
round(firsts.totalwgt_lb.median(),3), round(others.totalwgt_lb.median(),3)
~~~
As you can see by the results of both the mean and median calculations, first babies are typically smaller than non-first babies.

As for computing Cohen's *d* for baby weight, which compares the difference between the groups to the variability between groups, we can use the function outlined in the textbook as "CohenEffectSize" to get the number of standard deviations between the two means.

~~~

def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
~~~
**Pregnancy Length difference:** 0.029
~~~
round(CohenEffectSize(firsts.prglngth, others.prglngth),3)
~~~
**Baby Weight difference:** -0.089
~~~
round(CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb),3)
~~~

These results tell us pregnancy duration for first time babies is negligably longer than for non-first babies at .029 standard deviations longer, and baby weight is roughly 3 times that amount, with first babies being 0.089 standard deviations lighter than non-first babies, but still under 1 standard deviation apart.
