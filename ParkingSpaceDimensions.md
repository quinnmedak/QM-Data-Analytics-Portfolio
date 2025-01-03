# Advising Parking Space Dimension Planning 

## Data Set Summary
Data Set (cars04) made available by Loyola Marymoung University (MATH 205 Dr. Bargagliotti)
This data set contains 429 vehicles, theoretically depicting all cars used by residents of a city. It includes boolean variables reflecting the model/type of car, weight, length, width and wheel_base. The goal of my individual piece of this project was to propose dimensions of the city's public parking spaces in order to maximize space and cater to the city's population. To accomplish this goal, the width and length of the vehicles drove my analysis. 

## Outlier Threshold: Determining Common Length and Width
```{r}
library(tidyverse)
library(openintro)
library(knitr)
library(ggplot2)
library(statsr)
library(broom)
cars <- as.data.frame(read.csv('cars04.csv'))
```
```{r}
glimpse(cars04)
```
cars |> summarise(
q1 = quantile(width, 0.25, na.rm = TRUE), q3 = quantile(width, 0.75, na.rm = TRUE), iqr = q3 - q1
)
width = (iqr*1.5 + Q3)
```markdown
