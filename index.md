---
title       : Height Prediction
subtitle    : Predict the height of your offspring
author      : ManfredoS
job         : Scientifier
logo        : Sizes.png
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # {tomorrow, zenburn}
widgets     : [mathjax, quiz, bootstrap, shiny, interactive]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- .class #id

## Overview

The app "Height prediction" will allow you to predict the height of your yet unborn daughter or son at adult age. This is phantastic, because you can now plan ahead on real estate, clothes and all matters related to your offsprings future height.

The upcoming slides will guide you through the app with the follwing topics: 

1. Data set

2. Prediction model 

3. Interpretation and use of the shiny app


--- .class #id 

## Data set

The app is based on the following package:

```r
require(HistData)
```

The "PearsonLee" data set includes the heights of parents and their children, classified by gender:

```
##   child parent frequency gp    par chl
## 1  59.5   62.5       0.5 fs Father Son
## 2  59.5   63.5       0.5 fs Father Son
```

In the following plot (and regression) the dependency of the offsprings height on his (her) gender and the gender of the parents becomes visible. 
![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


--- .class #id 

## Prediction model

The height of the parants (parent) in inches as a numeric, and the expected combination of the gender of parent and offspring (gp) as a factor variable are the the two regressors on the height of the offspring (Child).    

```r
summary(lm.fit <- lm(child ~ parent + gp - 1, weight = frequency, data = PearsonLee))$coefficients
```

```
##        Estimate Std. Error t value  Pr(>|t|)
## parent   0.5206    0.03274   15.90 3.304e-49
## gpfd    28.6031    2.22215   12.87 2.311e-34
## gpfs    33.1799    2.20720   15.03 8.939e-45
## gpmd    31.3209    2.05219   15.26 6.210e-46
## gpms    36.1417    2.05203   17.61 2.902e-58
```


The prediction is performed as follows, using the above obtained linear regression coefficients:    

```r
Height <- function(height, select) predict(lm.fit, data.frame(parent = height, 
    gp = as.factor(select)), type = "response")
```



--- .class #id 

## Interpretation and use of the app

Interpreting the regression results, we observe gpms (female with male offspring) has the highest impact on height (+36.14 inches).

# Use of the app:
* Within the left panel of the "Height" app you can specify your own height in inches

* In the following you need to specify your gender and the expected gender of your offspring

* Finally press the submit button to obtain the height prediction. You´ll find your height (inches and centimeters) and gender specifications on the main panel.
You can find the prediction ouputs following your specifications.

# Now happy prediction ...

