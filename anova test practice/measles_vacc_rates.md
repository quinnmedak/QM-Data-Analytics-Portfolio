# Does School Type Significanly Impact Overall Measles Vaccination Rates?
## Skills Used
1. R programming
2. ANOVA test statistic
3. Hypothesis testing

## Summary of Data Set
This data set includes measles vaccination records, with variables including overall vaccination rate expressed as a percentage and type (public or private).

This data was completed by staff of The Wall Street Journal: Dylan Moriarty, Taylor Umlauf, & Brianna Abbot.

## Question:
Does School Type Significanly Impact Overall Measles Vaccination Rates?

# Libraries Used:
```{r}
library(tidyverse)
library(openintro)
library(knitr)
library(ggplot2)
library(statsr)
library(broom)
```

# Spread of Overall Vaccination Rates
After noticing that a large majority of overall vaccination rates were above 80 percent, I created a new variable to confirm this idea and visualized a table of counts and proportions.

```{r}
california <- california |>
  mutate(overall_group = case_when(
    overall >= 1 & overall <= 80 ~ "1-85",  # Group for 1 to 85
    overall >= 81 & overall <= 100 ~ "86-100",  # Group for 86 to 100
    TRUE ~ "Other"  # Optionally handle values outside this range (if any)
  ))
california |>
  filter(overall_group != "Other") |>
  count(overall_group) |>
  mutate (prop = n/sum(n))
```
<img width="475" alt="image" src="https://github.com/user-attachments/assets/d7bf7b94-5038-4890-8b07-dcdc789f216f" />

## Observing Association
Next, informed that over 95% of overall vaccination rates were above 80 percent, I visualized the overall rates between the two categories of type variable, excluding all rates under 80 for better visualization.

```{r}
california_clean <- california |>
  mutate(overall_limited = pmax(80, overall))

ggplot(california_clean, aes(x=type, y=overall_limited)) + 
  geom_boxplot()
```
<img width="792" alt="image" src="https://github.com/user-attachments/assets/a414e97d-6de2-4e70-b1e7-bdd8b71c25c2" />

This image shows little overlap between the two categories of school type, indicating that there is an association between school type and overall vaccination rate.

## Hypothesis Test and ANOVA  
To confirm this idea, I performed an ANOVA test.

H0: (null hypothesis) - Average overall vaccination rate is uniform among public and private schools

```{r}
anova_one_way<-aov(overall~type, data = california)
summary(anova_one_way)
```
<img width="569" alt="image" src="https://github.com/user-attachments/assets/cd35daad-e0fb-4fd1-919f-e46835ca7b1d" />

### Conclusion:
The p-value is extremely small, indicating that there is an association between the two variables, meaning the null hypothesis may be rejected. 
