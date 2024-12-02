# STA215-Bernknopf.R

setwd("H:/sta215")

library(readr)
library(haven)

data <- read_delim("raw_data.csv")

mean(data$cry)
mean(data$gory)
mean(data$date)
mean(data$`recurring `)

table(data$cry, data$gory)
table(data$date, data$`recurring `)

boxplot(data$cry)
boxplot(data$gory)
boxplot(data$date)
boxplot(data$`recurring `)

plot(data$cry)
plot(data$gory)
plot(data$date)
plot(data$`recurring `)

resid(data$date)
