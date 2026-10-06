---
title: "Ex3"
author: "Pieleanu Mircea-Adrian"
date: "06/10/2026"
output: github_document
---

## Some explanations
This is the dataset

```{r dataset, echo=TRUE}
dataset = c(14.0, 7.6, 11.2, 12.8, 12.5, 9.9, 14.9, 9.4, 16.9, 10.2, 14.9, 18.1, 7.3, 9.8, 10.9,12.2, 9.9, 2.9, 2.8, 15.4, 15.7, 9.7, 13.1, 13.2, 12.3, 11.7, 16.0, 12.4, 17.9, 12.2, 16.2, 18.7, 8.9, 11.9, 12.1, 14.6, 12.1, 4.7, 3.9, 16.9, 16.8, 11.3, 14.4, 15.7, 14.0, 13.6, 18.0, 13.6, 19.9, 13.7, 17.0, 20.5, 9.9, 12.5, 13.2, 16.1, 13.5, 6.3, 6.4, 17.6, 19.1, 12.8, 15.5, 16.3, 15.2, 14.6, 19.1, 14.4, 21.4, 15.1, 19.6, 21.7, 11.3, 15.0, 14.3, 16.8, 14.0, 6.8, 8.2, 19.9, 20.4, 14.6, 16.4, 18.7, 16.8, 15.8, 20.4, 15.8, 22.4, 16.2, 20.3, 23.4, 12.1, 15.5, 15.4, 18.4, 15.7, 10.2, 8.9, 21.0)

```
## Minimum and Maximum
```{r min and max, echo=FALSE}
min(dataset)
max(dataset)
```
## Average and Median
```{r avg and median, echo=FALSE}
mean(dataset)
median(dataset)
```
## Standard Deviation
```{r standard deviation, echo=FALSE}
sd(dataset)
summary(dataset)
```

# Data visualization

## Sequence plot
```{r seq plot, echo=FALSE}
plot(dataset, type = "l",col = "blue", xlab = "", ylab = "")
```
## Histogram
```{r histogram, echo=FALSE}
hist(dataset,col = "blue", xlab = "", ylab = "",xlim=c(0,25),ylim=c(0,25))
```
## I don't know what to do to make the histogram the same
