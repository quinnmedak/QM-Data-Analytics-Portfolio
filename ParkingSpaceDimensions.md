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
### Width

Firstly, I use a dot plot and a box plot to visualize the data and pinpoint any outliers. 
```{r}
ggplot(data = cars, aes(x = width)) + geom_dotplot(dotsize = 0.4)
```
#### Figure 1
<img width="789" alt="image" src="https://github.com/user-attachments/assets/7a0ee258-5a1b-4bf6-9cda-ca59c4238045" />

```{r}
ggplot(data = cars, aes(x = width)) + geom_boxplot()
```
#### Figure 2
<img width="804" alt="image" src="https://github.com/user-attachments/assets/82f2da19-05fa-4917-a3c7-5793a05eff8e" />

These visualizations raise concern of a few outlying vehicles whose widths' skew the data. Therefore, I use the following computations to find the quartiles for this variable and an IQR value which discounts outliers. 

```{r}
cars |> summarise(
q1 = quantile(width, 0.25, na.rm = TRUE), q3 = quantile(width, 0.75, na.rm = TRUE), iqr = q3 - q1
)
width = (iqr*1.5 + Q3)
```
Using the outlier threshold formula (IQR * 1.5 + Q3) to clean this data due to data points observed beyond the outlier threshold, I conclude that **over 99% of cars in the data set had a width of 79 inches or less**, providing a maximum width for parking space dimension planning. 

### Length
Again, I use a dot plot and a box plot to visualize the data and pinpoint any outliers. 
```{r}
ggplot(data = cars, aes(x = length)) + geom_dotplot(dotsize = 0.4)
```
#### Figure 3
<img width="891" alt="image" src="https://github.com/user-attachments/assets/114af267-e352-4ade-a7e7-cad55559c5de" />

```{r}
ggplot(data = cars, aes(x = width)) + geom_boxplot()
```
#### Figure 4
<img width="901" alt="image" src="https://github.com/user-attachments/assets/95a6af54-b97c-48fa-8995-77185e487407" />

The same concerns with the width variable arose for the length variable, so I calculated descriptive statistics in a similar fashion. 
```{r}
cars |> summarise(
q1 = quantile(length, 0.25, na.rm = TRUE), q3 = quantile(length, 0.75, na.rm = TRUE), iqr = q3 - q1
)
length = (iqr*1.5 + Q3)
```
Using the outlier threshold formula (IQR * 1.5 + Q3) to clean this data due to data points observed beyond the outlier threshold, I conclude that **over 99% of cars in the data set had a length of 209 inches or less**, providing a maximum length for parking space dimension planning. 

### Summary of Descriptive Statistics Calculated for Length and Width:
Width: Mean: 71.3, Median: 71,  Q1: 69, Q3: 73, SD: 3.4, IQR: 4 
Length: Mean: 185 inches, Median: 186, Q1: 177, Q3: 193, SD: 13, IQR: 16

## Recommendations
I propose that 75% of parking spaces be made this length plus 18 additional inches of room for the front and back of the vehicle, and this width plus 24 additional inches of room for each side of the vehicle, making 75% of spaces 103 inches wide and 227 inches long. 

Additionally, using the median statistic, 50% of the observed cars have a width of 71 inches or less and a length of 186 inches or less, so I propose that 25% of the spaces be made compact spaces. These should be this width plus 18 inches of additional room for each side of the vehicle, and this length plus 12 additional inches of room for the front and back of the vehicle, making 25% percent of spaces 89 inches wide and 198 inches long. 

The few observed cars whose widths and lengths were outliers of the data set would still be able to fit into the standard parking spaces, even if more tightly, due to provided wiggle-room for the front, back, and sides of the vehicles, as the maximum width is only 81 inches and the maximum length is only 227 inches.
