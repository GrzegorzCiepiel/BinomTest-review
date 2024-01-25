# Binom Test - simple review #

## Introduction ##
Probability of heads while tossing fair coin is 50% - ***null hypotesis***
We try 10 times but there are only two heads.
So what if probability of getting heads is different than 50% ? - ***alternative hypotesis***

## Analyse ##
flips = np.random.choice(["h", "t"], size=10, p=[0.5, 0.5])
WHERE
+ h - heads
+ t - tails
+  size - example size
+  p stands for probabilty
+  
print(sum(flips == "h"))

If we run this code a few times, we’ll likely see different results each time. Event with only two heads also occures :

['t' 'h' 'h' 't' 't' 't' 't' 't' 't' 't']

null_outcomes = []

for i in range(10000):

    flips = np.random.choice(["h", "t"], size=10, p=[0.5, 0.5])

    result = sum(flips == "h")
    
    null_outcomes.append(result)
    

null_min = np.min(null_outcomes) = ***0***

null_max = np.max(null_outcomes) = ***10***

null_mean = np.mean(null_outcomes) = ***0.498***

As we can see in 10 flips we can get from 0 to 10 heads. The distribution of heads shows plot below ( red line shows null_mean and yellow line shows us 2 )

![heads plot](https://github.com/GrzegorzCiepiel/BinomTest-review/assets/135313652/b4153501-f9ac-4abc-b6a5-5f5e4c989b29)

We can count what spread od heads we would have in 95% of outcomes:

outcomes_95 = np.percentile(null_outcomes, [2.5,97.5])

print(np.min(null_outcomes)) = ***0***

print(np.max(null_outcomes)) = ***10***

If our observed statistic falls outside this interval, then we can conclude it is unlikely that the null hypothesis
is true. In this example, because 2 falls within the 95% interval (0 - 10), it is still reasonably likely that we
observed a lower heads  rate by random chance, even though the null hypothesis was true.

null_outcomes = np.array( null_outcomes)

one_side_p_value = np.sum(null_outcomes <=2)/len(null_outcomes)

print(one_side_p_value)

We estimated that the probability of observing 2 or fewer heads is about 0.0542 (5.42%).
This probability (0.0542) is referred to as a one-sided p-value.

two_side_p_value = np.sum((null_outcomes <=2) | (null_outcomes >=8))/len(null_outcomes)

print(two_side_p_value)

two_s_p_value = binomtest(2, 10, 0.5)  = ***0.109375***

one_s_p_value = binomtest(2, 10, 0.5, alternative='less') = ***0.0546875***


### P-value counted "by hand" and p-value counted by function from scipy.stats is almost the same
### 0.0566 vs 0.0547. P-value is close to significance treshold but still completely sufficient to
### confirm the null hypothesis. 

