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
## How do online vs. offline market segments impact booking cancelation?
The hotel business is hypothetically experiencing a large number of booking cancelations and wonders how their online vs. offline market segments impact this high number. They want to readjust their marketing efforts depending on which segments cancel bookings significantly more.

To determine this, I transformed the market segment binary values, 0 and 1, assigned oppositely to offline vs. online bookers, into categorical values, allowing me to visualize them in a bar graph positioned for market segments and represented proportionately.
```{r}
hotel$categorical_canceled <- factor(hotel$is_canceled, 
                                     levels = c(0, 1), 
                                     labels = c("not canceled", "canceled"))
hotel$categorical_online <- factor(hotel$market_segment_Online_TA, 
                                     levels = c(0, 1), 
                                     labels = c("offline", "online"))
ggplot(hotel, aes(x = categorical_canceled, fill = categorical_online)) + geom_bar(position = "fill")
```
<img width="881" alt="image" src="https://github.com/user-attachments/assets/b8ffb684-ccc6-4807-918b-d687505e13b4" />
Firstly, a summary of the data reveals that the market segments are nearly evenly split, with 52 percent of bookers being a part of the online market segment and 48 percent being part of the offline market segment, making this visual relevant.
This visual informs me that over 50 percent of bookings which were followed through were booked by the offline market segment, meaning that these bookers are more reliable and less likely to cancel even though they make up a slightly smaller portion of the total market compared to online bookers. In addition, almost 75% of those who cancel their bookings are from the online market segment, meaning this segment has the greatest impact on the business' booking cancelation issue. 

### Recommendation
Due to these results, and the severity and urgency of the booking cancelation issue, I would recommend that this business limit the refund amount available to online bookers. However, there is essential information that could impact the effectiveness of this decision. 

### Further Data Necessary to Determine Refund Policy
While these statistics give insight on the issue of booking cancelations, the business cannot know how online bookers will react to a limited refund for online booking, especially if competing hotels offer a full refund garuntee. This information is necessary to obtain. Therefore, the hotel business should compare their policies to those of their competitors.

Additionally, none of the bookers in the sample are repeat bookers. If a portion of outlying bookers, those who book with this business frequently, are missing from the data set, the business's cancelation rates are likely much different that what's shown by the sample, and repeat bookers who may bring in a large proportion of revenue for the business might feel detered by a change in refund policy.

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

## Is there an association between nights stayed and cancelation?
The business may look to nights booked to find a reason for their high cancelation rate. To visualize this, I summed two variables to find total nights booked per booker and then plotted side-by-side box plots,
```{r}
hotel$total_nights <- hotel$stays_in_week_nights + hotel$stays_in_weekend_nights
ggplot(data = hotel, aes(x = total_nights, y = categorical_canceled)) + 
  geom_boxplot()
```
<img width="926" alt="image" src="https://github.com/user-attachments/assets/387d88a3-6d78-4f29-ab30-c75a1e2e01c5" />

This visualization demonstrated that the variables are not associated, so the company should avoid making any marketing changes related to length of stay.
