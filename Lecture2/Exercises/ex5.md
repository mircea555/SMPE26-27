---
title: "Ex 5 My analysis"
name: "Pieleanu Mircea-Adrian"
---

Let's first look at the first shuttle csv data

```{r}
data = read.csv("shuttle.csv",header=T)
data
```

One major mistake I think that they did in their analysis was the filtering the data to only the flights with malfunction especially when the sample is only 23 to begin with.In doing the filtering by flights with malfunctions, they had too few samples to draw conclusions on that it was safe and that the temperature doesn't affect the mission.
```{r}
data = data[data$Malfunction>0,]
data
```
7 samples is not enough when they had 23 to work with.This is the plots that they should have worked with

```{r}
plot(data=data, Malfunction/Count ~ Temperature, ylim=c(0,1))
```
<img width="875" height="540" alt="image" src="https://github.com/user-attachments/assets/2c148716-f43e-45e6-bc8b-3a9d2db6bced" />


```{r}
logistic_reg = glm(data=data, Malfunction/Count ~ Temperature, weights=Count, 
                   family=binomial(link='logit'))
summary(logistic_reg)
```
```
Call:
glm(formula = Malfunction/Count ~ Temperature, family = binomial(link = "logit"), 
    data = data, weights = Count)

Coefficients:
            Estimate Std. Error z value Pr(>|z|)  
(Intercept)  5.08498    3.05247   1.666   0.0957 .
Temperature -0.11560    0.04702  -2.458   0.0140 *
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 24.230  on 22  degrees of freedom
Residual deviance: 18.086  on 21  degrees of freedom
AIC: 35.647

Number of Fisher Scoring iterations: 5
```
```{r}
# shuttle=shuttle[shuttle$r!=0,] 
tempv = seq(from=30, to=90, by = .5)
rmv <- predict(logistic_reg,list(Temperature=tempv),type="response")
plot(tempv,rmv,type="l",ylim=c(0,1))
points(data=data, Malfunction/Count ~ Temperature)
```
<img width="875" height="540" alt="image" src="https://github.com/user-attachments/assets/64ef5d6d-0f24-48f8-94d7-5094e9830297" />


# Others mistakes
1. When the the temperature data is so different than the estimated temperature of the departure(31 F) I think is a really bad mistake on their part(the minimum in the dataset was 53 F which ironically had 2 malfunctions).
2. Another thing I think they got wrong was misleading the decision makers that the low temperature had little to no effect on the mission instead of reconizing that they didn't have the data at low temperature.
