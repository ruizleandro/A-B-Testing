# A/B Testing

## What is A/B Testing?

It is a controlled experiment where a change (usually on a website) is faced to its original form. For example, changing the color of a buy button from blue to orange.

In this case, an A / B test will be carried out to know which button works best.

This type of test can also be used in other situations, such as:

* Design changes.
* Changes in the user interface.
* Changes in an algorithm.
* Price changes (although not highly recommended).

## How is measured?

First of all, the first step to perform this experiment is to define which metric you want to optimize. It can be revenue, earnings, clicks, or ad views. You can choose one or more of these metrics depending on the case. When many of these improve, it means that you are on the right track.

> It is very important to know who to attribute a conversion to. For example, if we make a change to page A, and a user goes from page A to page B, and then to page C, is it thanks to the change made?

Also keep in mind that when performing an A / B test, variance is our enemy. So try to choose a metric that has little variance so as not to affect the conclusions of the experiment.

### T-statistic and p-value

These are two tools of statistics to know if a result is real.

#### T-statistic
T-statistic or T-test, is a measurement of the difference in behavior between the two groups, expressed in units of standard error.

The result is interpreted as follows: a high T-value means that there is a probability of a real difference. A low one indicates that the change made little difference.

In addition, there are alternatives to this test according to the metric observed: Fisher's exact test (clicks through rates), E-test (transactions per user), Chi-squared test (number of orders).

#### p-value

The p-value is the probability that the experiment satisfies the null hypothesis, that is, the probability that there is no real difference between the two groups.

A low p-value indicates that there is a high probability that the change will have a real impact on the analyzed metrics.

So what we are looking for is a high T-statistic and a low p-value. But before starting the experiment, we must decide the initial limit of success that we are looking for. It can be a p-value of 1 or 5 (more risk), but it is always possible that the result is random.

> When the result of the experiment is negative, you will not want to run it for a long time or you expose yourself to lose money. That is why it is a good idea to monitor the results on a daily basis.

### Measuring T-statistic and p-value in Python

Thanks to the scipy library it is quite simple to measure these values.

We are going to use synthetic data as an illustration:

```python
In[1]:
    import numpy as np
    from scipy import stats

    A = np.random.normal(26.0, 5.0, 10000)
    B = np.random.normal(25.0, 5.0, 10000)

    stats.ttest_ind(A, B)

Out[1]: 
    Ttest_indResult(statistic=-14.702166911741832, pvalue=1.1209149921150975e-48)
```

The negative T-test value tells us that we made a bad change, and the very low p-value confirms that it is very unlikely that the result is this by chance.

In summary, what we are looking for is a high T-test with a low p-value, to be sure that our changes are positive and a consequence of experiment and not chance.

## When to end the experiment?
It depends on the objectives set before the experiment, if you reached the p-value of 1 or 5, this is a good time.

If many days go by where the p-value does not drop, it means that it will not happen, and there you must decide what is the maximum time that you are willing to wait (it may be three or four more weeks), understanding that you can use that time for another experiment.

## A / B test gotchas
Correlation does not imply causality. There is always the possibility that there is no real effect.

* Novelty Effects: Your change works only because it's new. The only way to be sure of the results is to do the experiment again, and replicate the results.

* Temporal effects: if you carry out the experiment at Christmas (where people spend more) or in summer (where people spend more time on vacation). For this reason, you have to be aware of the time of year where the test is performed. In case of doing it in a "special" season, you should compare the results with the same period of the previous year.

* Partial selection: you have to be careful with the way in which you choose in which group each user will go (for example, putting new users in one group and old users in another), because the way in which a group reacts to the change can be conditioned. You must also make sure that during a session the user remains in the assigned group.

> Perform an A / A test (that is, use two equal groups) to check for bias or other problems.

## Data Noises

It is very important to clean the data before doing A / B testing. It is necessary to observe what type of outliers there are, since there may be many strange behaviors that need to be filtered.

## Errors in attribution

You should think about how you are going to count conversions as a function of distance from the change you made, and agree on how you are going to measure those effects. Also, if you are conducting several experiments at the same time, will they create problems for the other? That is very very important.

Again, you always have to take your results with a grain of salt. There are many things that can alter the results. Also, if you don't have much time, you have to take the results carefully and ideally try them again at another time.

## Conclusion

These are the basics of A / B testing, I didn't know anything about this either but thanks to the research I did for this article I have a good base of concepts.
