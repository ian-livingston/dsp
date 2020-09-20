[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

First, I looked at a side-by-side histogram of both groups. The initial result was a mess so I went back and used np.floor to round the weights to the nearest whole numbers, which allowed the use of fewer bins in the resulting histogram. The histogram showed both groups of baby weights exhibited normal distributions around the same center. Code (with **thinkstats2** and **thinkplot** imported and a few variables already defined):

>> `first_weights = np.floor(firsts["totalwgt_lb"])`
>> `first_weight_hist = thinkstats2.Hist(first_weights, label='first')`
>> `other_weights = np.floor(others["totalwgt_lb"])`
>> `other_weight_hist = thinkstats2.Hist(other_weights, label='other')`
>>
>> `width = .45`
>> `thinkplot.Hist(first_weight_hist, align="left", width = width)`
>> `thinkplot.Hist(other_weight_hist, align="right", width = width)`
>> `thinkplot.Config(xlim=(0, 14))`

Then, I compared the means, variances and standard deviations of each group. I didn't use the np.floor method in the interest of greater accuracy. This yielded for the first babies group:

- Mean: 7.201094430437772
- Variance: 2.0180273009157768
- Standard deviation: 1.4205728777207374

And for the other babies group:

- Mean: 7.325855614973262
- Variance: 1.9437810258964572
- Standard deviation: 1.3941954762143138

Code:

>> `summary_stat_comparison = {"first": (firsts["totalwgt_lb"].mean(), firsts["totalwgt_lb"].var(), firsts["totalwgt_lb"].std()), "other": (others["totalwgt_lb"].mean(), others["totalwgt_lb"].var(), others["totalwgt_lb"].std())}`

I then compared the means to find the difference, which was -0.12476118453549034, aka the mean weight of the other baby group was ~.125lb higher. Code:

>> `summary_stat_comparison["first"][0] - summary_stat_comparison["other"][0]`

Finally, I plugged the two groups into the CohenEffectSize function (copied and pasted below) and got as a result -0.10678966649967156, aka the weight of the other baby group was ~.11 standard deviations higher. This is nearly 4x larger than the difference in length between the first and other baby groups and so presumably more significant. Code:

>> `def CohenEffectSize(group1, group2):`
>>     `"""Computes Cohen's effect size for two groups.`
>>     `group1: Series or DataFrame`
>>     `group2: Series or DataFrame`
>>
>> ​    `returns: float if the arguments are Series;`
>> ​         `Series if the arguments are DataFrames`
>> ​    `"""`
>> ​    `diff = group1.mean() - group2.mean()`
>>
>> ​    `var1 = group1.var()`
>> ​    `var2 = group2.var()`
>> ​    `n1, n2 = len(group1), len(group2)`
>>
>> ​    `pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)`
>> ​    `d = diff / np.sqrt(pooled_var)`
>> ​    `return d`
>>
>> `CohenEffectSize(first_weights, other_weights)`

