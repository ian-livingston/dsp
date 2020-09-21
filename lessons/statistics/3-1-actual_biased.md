[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

First, I found the actual distribution of the number of kids (aged under 18) in the households of respondents. Code (with **thinkstats2** and **thinkplot** imported and a few variables already defined):

>> `how_many_kids = resp["numkdhh"]`
>> `kids_pmf_actual = thinkstats2.Pmf(how_many_kids, label="# of kids (actual)")`

The actual probability distribution is:

- 0: 0.466178202276593
- 1: 0.21405207379301322
- 2: 0.19625801386889966
- 3: 0.08713855815779145
- 4: 0.025644380478869556
- 5: 0.01072877142483318

Coded for plotting in a Pmf:

>> `thinkplot.Pmf(kids_pmf_actual, label="# of kids (actual)")`

Then I plugged the Pmf into the BiasPmf function (copied and pasted below) to find the biased distribution. Code: 

>> `def BiasPmf(pmf, label):`
>>     `new_pmf = pmf.Copy(label=label)`
>>
>> ​	`for x, p in pmf.Items():`
>> ​    	`new_pmf.Mult(x, x)`
>> ​    `new_pmf.Normalize()`
>> ​	`return new_pmf`
>>
>> `kids_pmf_biased = BiasPmf(kids_pmf_actual, label="# of kids (biased)")`

The biased probability distribution is as follows:

- 0: 0.0
- 1: 0.20899335717935616
- 2: 0.38323965252938175
- 3: 0.25523760858456823
- 4: 0.10015329586101177
- 5: 0.052376085845682166

Coded for plotting in a Pmf:

>> `thinkplot.Pmf(kids_pmf_biased, label="# of kids (biased)")`

Next, I plotted the two PMFs on the same plot:

>> `thinkplot.PrePlot(2)`
>> `thinkplot.Pmfs([kids_pmf_actual, kids_pmf_biased])`
>> `thinkplot.Config(xlabel="# of kids", ylabel="PMF")`

And finally I compared the means of the two versions of the data:

>> `print("Actual mean: {}".format(kids_pmf_actual.Mean()))`
>> `print("Biased mean: {}".format(kids_pmf_biased.Mean()))`

The two means:

- Actual mean: 1.024205155043831
- Biased mean: 2.403679100664282