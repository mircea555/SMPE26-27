Ex 5 My analysis
================

Let’s first look at the first shuttle csv data

``` r
data = read.csv("shuttle.csv",header=T)
data
```

    ##        Date Count Temperature Pressure Malfunction
    ## 1   4/12/81     6          66       50           0
    ## 2  11/12/81     6          70       50           1
    ## 3   3/22/82     6          69       50           0
    ## 4  11/11/82     6          68       50           0
    ## 5   4/04/83     6          67       50           0
    ## 6   6/18/82     6          72       50           0
    ## 7   8/30/83     6          73      100           0
    ## 8  11/28/83     6          70      100           0
    ## 9   2/03/84     6          57      200           1
    ## 10  4/06/84     6          63      200           1
    ## 11  8/30/84     6          70      200           1
    ## 12 10/05/84     6          78      200           0
    ## 13 11/08/84     6          67      200           0
    ## 14  1/24/85     6          53      200           2
    ## 15  4/12/85     6          67      200           0
    ## 16  4/29/85     6          75      200           0
    ## 17  6/17/85     6          70      200           0
    ## 18  7/29/85     6          81      200           0
    ## 19  8/27/85     6          76      200           0
    ## 20 10/03/85     6          79      200           0
    ## 21 10/30/85     6          75      200           2
    ## 22 11/26/85     6          76      200           0
    ## 23  1/12/86     6          58      200           1

One major mistake I think that they did in their analysis was the
filtering the data to only the flights with malfunction especially when
the sample is only 23 to begin with.In doing the filtering by flights
with malfunctions, they had too few samples to draw conclusions on that
it was safe and that the temperature doesn’t affect the mission.

``` r
data = data[data$Malfunction>0,]
data
```

    ##        Date Count Temperature Pressure Malfunction
    ## 2  11/12/81     6          70       50           1
    ## 9   2/03/84     6          57      200           1
    ## 10  4/06/84     6          63      200           1
    ## 11  8/30/84     6          70      200           1
    ## 14  1/24/85     6          53      200           2
    ## 21 10/30/85     6          75      200           2
    ## 23  1/12/86     6          58      200           1

7 samples is not enough when they had 23 to work with.This is the plots
that they should have worked with

``` r
plot(data=data, Malfunction/Count ~ Temperature, ylim=c(0,1))
```

![](ex5_mine_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
logistic_reg = glm(data=data, Malfunction/Count ~ Temperature, weights=Count, 
                   family=binomial(link='logit'))
summary(logistic_reg)
```

    ## 
    ## Call:
    ## glm(formula = Malfunction/Count ~ Temperature, family = binomial(link = "logit"), 
    ##     data = data, weights = Count)
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)
    ## (Intercept) -1.389528   3.195752  -0.435    0.664
    ## Temperature  0.001416   0.049773   0.028    0.977
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1.3347  on 6  degrees of freedom
    ## Residual deviance: 1.3339  on 5  degrees of freedom
    ## AIC: 18.894
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
# shuttle=shuttle[shuttle$r!=0,] 
tempv = seq(from=30, to=90, by = .5)
rmv <- predict(logistic_reg,list(Temperature=tempv),type="response")
plot(tempv,rmv,type="l",ylim=c(0,1))
points(data=data, Malfunction/Count ~ Temperature)
```

![](ex5_mine_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

# Others mistakes

1.  When the the temperature data is so different than the estimated
    temperature of the departure(31 F) I think is a really bad mistake
    on their part(the minimum in the dataset was 53 F which ironically
    had 2 malfunctions).
2.  Another thing I think they got wrong was misleading the decision
    makers that the low temperature had little to no effect on the
    mission instead of reconizing that they didn’t have the data at low
    temperature.
