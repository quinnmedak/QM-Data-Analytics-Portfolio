# Summary of Data
This dataset contains fifty variables describing the hotel bookings of 100 clients. 
It was accessed through DataCamp. 

The following are realistic, hypothetical questions this hotel business may ask to improve their business.

```{r}
library(tidyverse)
library(openintro)
library(knitr)
library(ggplot2)
library(statsr)
library(broom)
```
```{r}
glimpse(hotel)
```

## What is the relationship between cancelation and price of booking? Is there an association?
To answer this question, I used a visualization method that allows me to compare one quantitative and one categorical variable. 
To do so, I first needed to transform the is_cancelled variable to a categorical variable, where 1 values represent "Yes" (canceled) and 0 values represent "No" (not cancelled):
Next, I visualized two box plots side by side. 
```{r}
hotel$qualitative_canceled <- factor(hotel$is_canceled, 
                                     levels = c(0, 1), 
                                     labels = c("No", "Yes"))
ggplot(hotel, aes(x=avg_daily_rate, y=qualitative_canceled))+ geom_boxplot()
```
<img width="912" alt="image" src="https://github.com/user-attachments/assets/817b8cd6-bcec-4010-9608-54793d687150" />

This visualization leads me to believe from initial observation that no association exists between the two variables because so much overlap exists in daily rates. 
