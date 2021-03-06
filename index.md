---
title       : Central Limit Theorem
subtitle    : With proper simulatons, many random variables are Gaussian.
author      : Luis Capelo
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Summary

In this report we present the essential differences between the theoretical mean and the empirical mean (or sample  mean). It addresses that by demonstrating how the [Central Limit Theorem](http://en.wikipedia.org/wiki/Central_limit_theorem) defends that, with the proper amount of simulations, many distributions are Gaussian.


--- 

## Variances and Distributions

If we generating a number random, non-Gaussian samples, and take plot their observations, we'll notice that those are naturally skewed to the left. Their theoretical variance (and mean) will demonstrate that skewness. 


```r
library(ggplot2)
# Function to make simulations.
calculateVariance <- function(simulations) {
  for (i in 1:simulations) {
    it <- data.frame(
      title = paste("Simulation", i),
      observations = rexp(40, 0.2)
      )
    if (i == 1) out <- it
    else out <- rbind(out, it)
  }
  return(out)
}
```

---

## Variance from Random Samples

```r
# Running simulations
ggplot(calculateVariance(6)) + theme_bw() + 
  geom_histogram(aes(observations),) + 
  facet_wrap(~ title, ncol = 6)
```

<img src="assets/fig/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" width="1000in" height="300in" />

---

## Empirical (Sample) Mean

The Central Limit Theorem demonstrates that, if given a certain number of observations and observing the characteristics of those groups, the Empirical Mean of those samples will beform a Gaussian distribution. That's what makes the CLT wonderful for statistical inference.


```r
# Function to make simulations.
calculateSimulations <- function(simulations) {
  for (i in 1:simulations) {
    results <- rexp(40, 0.2)
    it <- data.frame(id = i, 
                     mean = mean(results), 
                     variance = var(results),
                     sd = sd(results))
    if (i == 1) out <- it
    else out <- rbind(out, it)
  }
  return(out)
}
```

---

## Plot of Gaussian Curve with 1000 Simulation


```r
# Running the simulations.
results <- calculateSimulations(1000)
qplot(results$mean)
```

<img src="assets/fig/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" height="300in" />









