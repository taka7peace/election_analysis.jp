# Election Analysis JP
## Introduction
This project undertakes an analysis of voting results concerning the Osaka metropolitan plan.


## Objective Clarification and Variable Definition
### Objective: 
The main goal of this analysis is to identify potential influential factors, bolstered by robust evidence, that significantly sway the approval rates.

### Dependent Variable: 
The dependent variable under study is the 'Approval Rate' for concerning the Osaka metropolitan plan.

### Independent Variables: 
The independent variables encompass a set of features, each of which could potentially be a candidate influencing the approval rate.

Moving forward with the analysis, the focus will be on extracting the factors that have contributed to significant changes in the approval rate compared to previous periods. Therefore, I will create a grouping of outliers based on the current approval rate (serving as the dependent variable) and the approval rate from the previous period (serving as the independent variable).

## Target Parameters
![Screenshot 2023-04-28 154244](https://github.com/taka7peace/election_analysis.jp/assets/114953599/44ff17ce-2731-40e7-a1b5-f35a6ad00425)

## Feature Selection
The following features have been chosen as potential factors:

'Proportion over 60' (excluding the reversal trend of people in their 20s)
'Proportion of 30-50s' (including the reversal trend of people in their 20s)
'Male Ratio'
'Time required from the station where the main government building is located to the old district center station'
'Average Household Size'
'Average Annual Income per Person'
The fourth feature reflects a domain-specific understanding that those living away from the main government building might feel their region would be left out of development.

## Data Collection and Cleansing
Data for each feature has been collected and cleaned as follows:

### 1.'Proportion over 60', 2.'Proportion of 30-50s', 3.'Male Ratio': 
Data acquired from Osaka City HP's 2020 age and gender-specific estimated population. The target age group proportion and male ratio were calculated and a field for each district was created.
(https://www.city.osaka.lg.jp/toshikeikaku/page/0000015211.html)

### 4.'Time to the main government building': 
The average required time from the old district center station to the nearest station of the new ward office was calculated at 8, 12, 15, and 18 on Saturday.
(https://ekitan.com/)

### 5.'Average Household Size': 
Data acquired from the Osaka City HP's 2020 number of people per household data. A field for each district was created.
(https://www.city.osaka.lg.jp/toshikeikaku/page/0000068035.html)


### 6.'Average income per person': 
Income class data by household was downloaded from the Osaka City HP. The average annual household income was calculated by multiplying the average annual income and proportion for each class, and then dividing by the average household size obtained in feature 5.
(https://www.city.osaka.lg.jp/toshikeikaku/page/0000233170.html)

## Feature Importance for Election
In order of importance, the top features are:

1. 'Proportion of 30-50s'
2. 'Average Household Size'
3. 'Male Ratio'

Our analysis suggests more approval in districts with a high proportion of working-age males, fewer average household sizes, and located in the north. Conversely, more opposition is noted in districts with a low proportion of working-age males, larger families, and located in the south. The influence of age composition appears to be the largest, while the influence of male ratio is the smallest.

As can be seen from correlation analysis, the substantial opposition in their 20s (the reversal phenomenon with their 30s) is also likely to impact the difference in approval rate by district.

## Model Performance

## Learning Curve

![Screenshot 2023-05-19 153640](https://github.com/taka7peace/election_analysis.jp/assets/114953599/043cb235-6199-4bbd-b048-95b01dc800ac)

・Is the target performance achieved?

→ Although the target performance is not set, it is OK because it has improved significantly from before tuning (-0.0369 → -0.0150)


・Isn't it overfitting?

→ Reversal can be seen in the part where the number of data is small, but it is OK because the verification data index and the training data index finally converge

### Before tuning: 
The model predicted the same value (color intensity) for all conditions, indicating unsuccessful regression. The model needed improvement in tuning.

![Screenshot 2023-05-19 153813](https://github.com/taka7peace/election_analysis.jp/assets/114953599/3576989a-71b4-412c-9cf8-74f21f435f1a)


### After tuning: 
The model showed significant improvement. It successfully captured trends, indicating higher approval rates (darker color) for districts with a higher male ratio, more people between the ages of 30-60, and located further north.

![Screenshot 2023-05-19 153802](https://github.com/taka7peace/election_analysis.jp/assets/114953599/a3a8712f-7697-4c6a-a56e-2ee88b6c8af7)

## Final Thoughts
Optuna emerged as the best algorithm for parameter tuning of LightGBM, both in terms of speed and evaluation metrics. Please note that certain parameters can affect the learning time, potentially slowing down the speed of grid search. Although the model did not meet a specific target performance, the tuning significantly improved its performance, which is a success in its




