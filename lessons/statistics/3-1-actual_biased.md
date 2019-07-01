[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Communicate the problem, how you solved it, and the solution, within each of the following markdown files. (You can include code blocks and images within markdown.)

The problem we're addressing in this section is the class size paradox, which is the bias found when surveying children to ask how many children there are in their family. The biases found are that families with more children will be more likely to be surveyed, and obviously families without children will not be surveryed at all.

The goal of this assignment is to compute the baised distribution, compare it to the actual distribution and show them visually. The method we're going to use will be presented in a probability mass function and compared visually via step function.

As for the bias calculation, ThinkStats has provided us with the function BiasPmf:

~~~
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
~~~

This function works as follows, for each actual number of children per family, we multiply the probability by the number of children able to report on that family size. You can see the result below graphed on top of the actual number:

~~~
resp = nsfg.ReadFemResp()
actual
pmf = thinkstats2.Pmf(resp.numkdhh, label='actual')
thinkplot.Pmf(pmf)
thinkplot.Config(xlabel='Number of children', ylabel='PMF')

biased = BiasPmf(pmf, label='biased')
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')
~~~
