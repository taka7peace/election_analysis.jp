# election_analysis.jp

## Introduction

"In districts with a higher proportion of males, there is a higher rate of approval. Similarly, in districts where there is a higher proportion of individuals in their 30s to 50s, the approval rate is higher.

Objective Clarification (Setting the dependent variable)

Objective: To extract potential factor candidates with solid evidence for the highs and lows of the approval rate

Dependent variable: Approval rate

Independent variables: Features that can be potential factor candidates
With this in mind, I plan to proceed with the analysis.since I want to extract the factors of the district where the approval rate has changed significantly compared to the last time, I will group the outliers with the dependent variable as this time's approval rate and the independent variable as the previous approval rate.

##Feature Selection
(Selection of independent variables)

This time, it was a bit peculiar that only people in their 20s are reversing the trend, so considering the presence or absence of this effect,

Feature 1 'Proportion over 60' (not considering the reversal phenomenon of people in their 20s)

Feature 2 'Proportion of 30-50s' (considering the reversal phenomenon of people in their 20s)

Feature 3 'Male Ratio'

Feature 4 'Time required from the station where the main government building is located to the old district center station' I live in a district different from where the main government building is located, but I felt a little sense of insecurity that 'my living area may be left out from the development' (domain knowledge).

Feature 5 'Average Household Size'

Feature 6 'Average Annual Income per Person'

##Data Collection and Cleansing
'1. Proportion over 60' 

'2. Proportion of 30-50s'
'3. Male Ratio'

Data acquisition method: Download the 2020 age and gender-specific estimated population from the Osaka City HP
Cleansing Method: Calculate the proportion of the target age group and the male ratio for the entire population and create a field for each district.

'4. Time to the main government building'

Data acquisition and cleansing method: Calculate the average required time from the old district center station to the nearest station of the new ward office at 8, 12, 15, and 18 on Saturday.

'5. Average Household Size'

Data acquisition method: Download the number of people per household in 2020 from the Osaka City HP
Cleansing Method: Create a field for each district

'6. Average income per person'

Data acquisition method: Download income class data by household from the Osaka City HP
Analysis and visualization of results
Cleansing Method: Calculate the average annual household income by multiplying the average annual income and proportion for each class, and divide by the average household size obtained in 5.

![Screenshot 2023-04-28 153839](https://github.com/taka7peace/election_analysis.jp/assets/114953599/17b3027e-b31b-4622-b58a-d33c9a77b1ad)


![Screenshot 2023-04-28 154244](https://github.com/taka7peace/election_analysis.jp/assets/114953599/44ff17ce-2731-40e7-a1b5-f35a6ad00425)


![Screenshot 2023-05-19 153813](https://github.com/taka7peace/election_analysis.jp/assets/114953599/3576989a-71b4-412c-9cf8-74f21f435f1a)



![Screenshot 2023-05-19 153640](https://github.com/taka7peace/election_analysis.jp/assets/114953599/043cb235-6199-4bbd-b048-95b01dc800ac)



![Screenshot 2023-05-19 153802](https://github.com/taka7peace/election_analysis.jp/assets/114953599/a3a8712f-7697-4c6a-a56e-2ee88b6c8af7)

## Result 

Before tuning, the predictions were constant and did not regress well,

After tuning, the higher the male ratio (3_male_ratio),

the more 30-60s (2_between_30to60), and the further north (latitude),

the higher the approval rate (approval_rate) = darker color,

indicating that the trend is captured.

Tuning Success

Parameter tuning of LightGBM was performed by selecting 7 parameters.

Optuna was the best algorithm among the four algorithms in terms of both speed and evaluation metrics.

Some of the parameters affect the learning time, so a wide range of parameters can slow down the speed of grid search.
