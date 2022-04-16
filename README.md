# SC1015 Project - Income Determinants #
![Screenshot](incomepic.png)

Welcome to our repository! Our team comprises of Ryan, Teg and Augustine. This is our project from SC1015: Introduction to Data Science and Artificial Intelligence.

## Contributors ##
- Ryan Ng (@iamschlomo)
- Teg Tiwana (@tej172)
- Augustine Lee (@auglxw)

## Repository Directory ##
- Data folder: Contains the raw dataset, reduced dataset and train and test datasets. It also contains the data dictionary file obtained from the US Census Department.
- Data Cleaning.ipynb: Notebook for data cleaning and preprocessing
- EDA.ipynb: Notebook for Exploratory Data Analysis
- ML_Decision Tree Classifier.ipynb: Notebook for Decision Tree Classifier model
- ML_Gradient Boosting Classier.ipynb: Notebook for Gradient Boosting Classifier model

## Problem Formulation ##  
In this project, we are interested in finding out how different factors affect one's income. We felt that this will serve useful for people who wish to enter a new industry and would like to know, with their characteristics, what is the rough income they can expect to receive. We aim to create a classification model that will take in the features of an individual and predict an income class. Hence, the questions we aim to answer through our project are:
- What are the most important factors in determining one's income?
- Can we create a ML model to classify one's potential income to an income range based on his/her information?
#### Metrics for success: ####
F1 (Macro-averaging) score. F1 score takes into account both precision and recall, and macro averaging treats each income class as equal.

## Data Source ##  
To address our problem, we have used the the Annual Social and Economic Supplements from the United States' Census Bureau Current Population Survey 2021. This dataset provides us with data of American and a wide range of their information, from innate characteristics (race, gender etc) to education attaintment to familial information, as well as their corresponding income.

## Data Cleaning and Preprocessing ##
Our raw dataset has 830 columns and 163543 rows. Through the data dictionary, we found that the columns were classified into 10 broad areas:
1. Record Identifiers
2. Weights
3. Demographics
4. Basic CPS Items
5. Work Experience
6. Income
7. Poverty
8. Health Insurance
9. Supplemental Poverty Measure
10. Migration

From there, we conducted the following steps to preprocess our data:
- Preliminary selecting relevant columns
- Check for missing and invalid entries
- Dropping columns with high percentage of invalid entries
- After dropping those columns, we have about 7.49% of rows with invalid entries. We compared the distribution of our reponse variable before and after dropping and found that the distribution remains about the same. Hence, we dropped those rows.
- Exploring the number of levels for categorical variables. We dropped 1 column (Occupation) as it has 526 levels and we do not have enough support for it.
- As our problem is a classification problem, we encode our response variable (Salary) into 4 classes.
- Splitting into train and test data (80:20)

In our preprocessing, we made the following assumptions (justifications of assumptions found in notebook):
- Only features in the areas of Demographics, Basic CPS Items and Income are relevant to our problem.
- Incomes above top 10% of USA's earners are not relevant to us.

#
## Exploratory Data Analysis ##
For Exploratory Data Analysis, we did the following steps:
1. Exploration of response variable and predictor variables
2. Single-Variate Analysis of each predictor variable against the response variable
3. Multi-Variate Analysis to identify any trends
For each step, we also conducted data visualisation.

These are the insights from our EDA:

### Exploration of Variables ###
1. Salary: Cat 1 has the lowest count. The income classes have about the same count.
2. Education: The qualifications with the highest count are High School Diploma and Bachelor's Degree.
3. Marital Status: Most people are married with a civilian spouse.
4. Sex: There are about equal number of males and females in the dataset.
5. Race: The race most represented is "White Only", which is about 7 times more represented than the next most represented race - "Black Only". Many races are not given significant representation.
6. Veteran: There are many more veterans than non-veterans (43082 vs 2245).
7. Professional Certificates: The number of people without professional certificates is about three times that of those with.
8. Disabilities: There are very few people with the various disabilities (1%).
9. Citizenship: The most represented citizenship status is "Native, born in US", about 10 times of the second most represented citizenship - "Foregin born, US citizen by naturalization".
10. Working Hours: The median and most common working hours in 40 hours.
11. Industry: The most represented industry is "Educational and health services", about twice of the second most represented industry - "Wholesale and retail trade".
12. Work Class: The most represented workclass is "Private, for profit", about 10 times that of the second most represented work class - "Government Local".

### Single-Variate Analysis ###
1. Education: Generally, the more education one receives, the higher the salary received.
2. Marital Status: Married respondents earn the most on average but it could be due to other factors like them being older. This is supported by how married and divorced respondents earn more on average. It may not be meaningful to attribute the difference in salary to solely their marital status.
3. Sex: On average, males earn more than females.
4. Age: People aged between 40-55 are earning the most on average.
5. Race: Due to a lack of representation in many races, the mean salary class may not be meaningful. We also see that generally, there is an increasing number of people from income class 4 to 1.
6. Veteran: Veterans appear to earn more than non-veterans. Perhaps this is due to veterans being respected for their contributions to the country or it may be due to them being older. However the difference is not a lot.
7. Professional Certificates: Respondents with professional certificates appears to earn more on average but not much more.
8. Disabilities: Respondents without grooming, errand and climbing disability appear to earn more. Respondents with visual disability earn slightly less on average. Regardless of hearing disability, it appears that respondents earn the same on average. This suggests that hearing disability may not be an important feature in predicting salary.
9. Citizenship: It appears that there is no clear distinction between native and foreign-born. However, it seems that non-citizens have a lower salary.
10. Working Hours: It appears that people will lower salary work less hours per week on average.
11. Industry: The mining industry is the most well-compensated industry.
12. Work Class: We see that generally, the government sector pays better than the private sector and within the government sector, federal pays better than local which in turn pays better than state. For the private sector, nonprofit appears to pay better than profit in general and self-employed people with incorporated companies tend to earn more than self-employed people without incorporated companies who tends to earn in the lowest income band.

### Multi-Variate Analysis ###
1. It appears that regardless of marital status, having a higher education level helps to boost one's income.
2. It appears that on average, with the same level of education, females tend to earn less than males.
3. It appears that on average, with the same education level, people aged 40-65 are earning more. This could be due to their wealth of experience.
4. It seems like there isn't much linear correlation between Education and Race. Regardless of Race, Education does help to get a higher income.
5. With the same level of education, veterans tend to fetch a higher salary.
6. With the same formal education level, having an extra professional certificate do help to compensate a lower education level and fetch a higher salary.
7. It appears that having grooming or errands disability will result in one having a lower pay, in general.
8. With the same level of education, having hearing or visual disability will still fetch about the same income range.
9. For those without a degree, having concentration disability will result in one having a lower pay, in general.
10. Across the various citizenship, with the same education level, they seem to fetch about the same income range. However non-citizens tend to fetch a lower income range among the various citizenship status.
11. Across the various industry, higher education will generally result in higher pay. However, in the Transportation and Utilities Industry (6), having higher education beyond a degree does not bring about an increasing trend in salary.
12. Regardless of private, public or self-employed, having a higher education does increase one's salary in general.
13. Regardless of education level, the work hours needed to achieve the same income range is about the same.
14. It appears that the across various marital status, the number of hours worked for the same income class is about the same except people who are married to an armed forces spouse who work 3 hours less weekly on average.
15. Within the same income range, males work longer hours than females.
16. People aged 25 to 59 years old work the longest for the same income range.
17. For races with significant representation (white only and black only) in the survey, it seems like the hours worked is largely consistent across the various races.
18. Regardless of veteran status, the hours worked for the same income range are about the same.
19. Regardless of whether one has a professional certificate, the hours worked for the same income range are about the same.
20. Reople with grooming, errands and concentration disabilities work less on average for the same income range.
21. For higher paying jobs (cat 4 - 3), the hours worked for those with hearing disability are about the same as those without hearing disability. However, for lower-paying jobs (cat 1 and 2), the hours worked by those with hearing disability are less. This could be due to lower-paying job being more physically-demanding.
22. Regardless of visual disability, the hours worked are about the same for each income range.
23. For salary cat 3 and 4, regardless of climbing disability, the hours worked are about the same. However, for cat 1 - 2, the hours worked are less for those with climbing disability. This could be due to lower-paying jobs being more physically-demanding. 24. The hours worked for each income range, across the various citizenship status, are largely consistent.
25. The agriculture, foresty, fishing and hunting as well as mining industries have the longest working hours. The other industries tend to be about the same.
26. The hours worked across various workclass are quite consistent except those who are self-employed and without an incorporated company. This could be due to the fact that they may be freelance workers with lower working hours. Those who are self-employed with an incorporated company and in salary cat 3 also has a higher working hours than the rest. This could be because their companies are in the start-up phase and require more hours to grow the company.

#
## Machine Learning (Decision Tree Classifier) ##
In this notebook, we explored the use of a Decision Tree Classifier.
- Our base model of max depth 3 yielded a f1 score of 0.44240.
- Through hyperparameter (max depth) tuning, we found the optimal max depth is about 7-13.
- We conducted cross-validation using GridSearchCV and found the optimal max depth is 8 and this model yielded a f1 score of 0.49456.
- We found that the Race, Marital, Vis_Dis, Citizenship and WorkClass are not very useful for our model.

#
## Machine Learning (Gradient Boosting Classifier) ##
In this notebook, we explored the use of a Gradient Boosting Classifier.
- Our base model of max depth 3, n_estimators 300 and subsample 0.7 yield a f1 score of 0.52610.
- Through hyperparameters (max depth, n_estimators and subsample) tuning, we estimated the optimal max depth to be 2-5.
- After cross-validation, we found the optimal hyperparameters to be max depth=3, n_estimators=150 and subsample=0.8. This model yield a f1 score of 0.52658.

#
## New tools we have learnt ##
- Data Visualisation: GraphViz
- Cross-Validation: GridSearchCV
- ML models: Gradient Boosting Classifier, Multi-Layer Perceptron, Support Vector Machines
