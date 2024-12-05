setwd("H:/sta215")

library(readr)
library(haven)
library(ggplot2)

raw_data <- read_delim("raw_data.csv")
data <- na.omit(raw_data)

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
boxplot(data$cry, data$date)

plot(data$cry)
plot(data$gory)
plot(data$date)
plot(data$`recurring `)

resid(data$date)


##################################################################################
#################### Figure 1: boxplot             ####################   
##################################################################################
# BOX PLOT
ggplot(data, aes(x = as.factor(cry), y = `recurring `)) +
  geom_boxplot() +
  labs(title = "Box Plot of Cry and Recurring",
       x = "cry",
       y = "recurring") +
  theme_minimal()

anova <- aov(data$`recurring ` ~ as.factor(data$cry))
summary(anova)
##################################################################################
####################   Figure 2: scatter plot             ####################   
##################################################################################
linear_plot <- plot(data$date, data$`recurring `)
print(linear_plot)

# add x line and y line for means
meanx <- mean(data$date)
meany <- mean(data$`recurring `)

abline(v = meanx, col = "black")
abline(h = meany, col = "black")

linear_relationship <- lm(data$`recurring ` ~ data$date)
summary(linear_relationship)


# Add the linear regression line to the scatter plot
# NOTE: double check the scatter plot is currently in your utilities window!
abline(linear_relationship, col = "red")
##################################################################################
####################  Figure 3: residual plot                ####################   
##################################################################################
# Plot the residuals
plot(data$date, residuals(linear_relationship))

# Add a horizontal line at zero to indicate the baseline
abline(h = 0, col = "red")

##################################################################################
####################  Table 2: contingency table                ####################   
##################################################################################
table(data$gory, data$cry)
chisq.test(data$gory, data$cry)
##################################################################################
#################### Table 1: description #########################################
##################################################################################
table(data$cry)
table(data$gory)
mean(data$date)
mean(data$`recurring `)
min(data$date)

min(data$`recurring `)
max(data$`recurring `)
sd(data$date)
sd(data$`recurring `)
