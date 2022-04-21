# SC1015 Project - Income Determinants #
![Screenshot](incomepic.png)

Welcome to our project's repository for SC1015: Introduction to Data Science and Artificial Intelligence !

## Contributors ##
- Ryan Ng (@iamschlomo) : Support Vector Machine, K-Nearest-Neighbours
- Teg Tiwana (@tej172) : Multilayer Perceptron
- Augustine Lee (@auglxw) : Data Cleaning, Exploratory Data Analysis, Feature Engineering, Decision Tree Classifier, XGBoost Classifier

## Repository Directory ##
- Data folder: Contains the raw dataset, reduced dataset and train and test datasets. It also contains the data dictionary file obtained from the US Census Department.
- Data Cleaning.ipynb: Notebook for Data Cleaning and Preprocessing
- Feature Engineering.ipynb: Notebook for Feature Transformation and Dimension Reduction
- EDA.ipynb: Notebook for Exploratory Data Analysis
- ML_Decision Tree Classifier.ipynb: Notebook for Decision Tree Classifier model
- ML_Gradient Boosting Classier.ipynb: Notebook for Gradient Boosting Classifier model

## Problem Formulation ##  
In this project, we are interested in finding out how different factors affect one's income. We felt that this will serve useful for people who wish to enter a new job and would like to know, with their characteristics, what is the rough income they can expect to receive. We aim to create a classification model that will take in the features of an individual and predict an income class. Hence, the questions we aim to answer through our project are:
- What are the most important factors in determining one's income?
- Can we create a ML model to classify one's potential income to an income range based on his/her information?
#### Metrics for success: ####
F1 (Macro-averaging) score. F1 score takes into account both precision and recall, and macro averaging treats each income class as equal.

## Data Source ##  
To address our problem, we have used the the Annual Social and Economic Supplements from the United States' Census Bureau Current Population Survey 2021. This dataset provides us with data of American and a wide range of their information, from innate characteristics (race, gender etc) to education attaintment to familial information, as well as their corresponding income.
- Source: https://www.census.gov/data/datasets/time-series/demo/cps/cps-asec.html

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
- As our problem is a classification problem, we encode our response variable (Salary) into 4 classes.
- Splitting into train and test data (80:20)

In our preprocessing, we made the following assumption (justification found in notebook):
- Only features in the areas of Demographics, Basic CPS Items, Work Experience and Income are relevant to our problem.

#
## Exploratory Data Analysis ##
For Exploratory Data Analysis, we did the following steps:
1. Understand dataset dimension
2. Exploration of features through Single-Variate Analysis
3. Understanding relationship of each feature with Salary through Bi-Variate Analysis
4. Exploring possible trends through Multi-Variate Analysis

These are the insights from our EDA:

### Single-Variate Analysis ###
1. Salary: Cat 1 has the lowest count. The income classes have about the same count.
2. Education: The qualifications with the highest count are High School Diploma and Bachelor's Degree.
3. Marital Status: Most people are married with a civilian spouse.
4. Sex: There are about equal number of males and females in the dataset.
5. Age: We see that majority of the respondents are aged 20 to 64 years old. There are 4612 respondents who are outliers (younger than 20 or older than 64).
5. Race: The race most represented is "White Only", which is about 7 times more represented than the next most represented race - "Black Only". Many races are not given significant representation.
6. Veteran: There are many more non-veterans than veterans.
7. Professional Certificates: The number of people without professional certificates is about three times that of those with. Among those who possess professional certificates, most are issued by government bodies. However, for most, they do not require such certificates in their jobs.
8. Disabilities: There are very few people with disabilities (1702 vs 49493).
9. Citizenship: The most represented citizenship status is "Native, born in US", about 10 times of the second most represented citizenship - "Foregin born, US citizen by naturalization".
10. Working hours: Most work between 34 -42 hours. For those who work less than 35 hrs, it is a common occurence for many. However, for those who are working full-time, most work longer than 35 hours usually; most work 40 hours weekly.
11. Industry: The most represented industry is "Educational and health services", about twice of the second most represented industry - "Wholesale and retail trade".
12. Occupation Group: Professionals is the most common occupation group, followed by management and financial occupations then service occupations. Occupations that are more traditional like farming, fishing and forestry are less popular.
13. Occupations: Most common occupations include managers, teachers, registered nurses, ship captains, retail supervisors and customer service representatives.
14. Work Class: The most represented workclass is "Private", about 15 times that of the second most represented work class - Government, Local.
15. Longest Industry: Many respondents have industrial experience in healthcare and social assistance, retail trade and educational services.
16. Longest Job Class: TMost respondents have most experience working in private and government companies.

### Bi-Variate Analysis ###
1. Education: Generally, the more education one receives, the higher the salary received.
2. Marital Status: Married respondents earn the most on average but it could be due to other factors like them being older. This is supported by how married and divorced respondents earn more on average. It may not be meaningful to attribute the difference in salary to solely their marital status.
3. Sex: On average, males earn more than females.
4. Age: On average, those who are older earn more.
5. Race: Due to a lack of representation in many races, the mean salary class may not be meaningful. We also see that generally, there is an increasing number of people from income class 4 to 1.
6. Veteran: Veterans appear to earn more than non-veterans. Perhaps this is due to veterans being respected for their contributions to the country or it may be due to them being older. However the difference is not a lot.
7. Professional Certificates: Respondents with professional certificates appears to earn more on average but not much more. Whether one's professional certificate is issued by the government does not seem to have much impact on one's salary. For those with professional certificates, if their job requires them to have the certificate, they are generally better paid.
8. Disabilities: Respondents with disability earn less on average and they tend to work at jobs in the lower income classes.
9. Citizenship: It appears that there is no clear distinction between native and foreign-born. However, it seems that non-citizens have a lower salary.
10. Working Hours: It appears that people with lower salary work less hours per week on average. Working longer hours tend to be associated with a higher pay; 5hose who work less than 35 hours for more than 1 week earn less on average.
12. Household Information: It does not seem to have a trend except that children of householders tend to earn less, possibly due to their younger age.
13. Industry: The mining industry is the most well-compensated industry.
14. Occupations: Occupations related to management and finance are the most well-paid while service occupations are paid the lowest.
15. Work Class: We see that generally, the government sector pays better than the private sector and within the government sector, federal pays better than local which in turn pays better than state. Self-employed people with incorporated companies tend to earn more than self-employed people without incorporated companies who tends to earn in the lowest income band.
16. Experience: We see that generally, those with mining, utilities, professional and technical industrial experience are the most well-paid. Generally, those have been working for the government earn the most.

### Multi-Variate Analysis ###
1. It appears that regardless of marital status, having a higher education level helps to boost one's income.
2. It appears that on average, with the same level of education, females tend to earn less than males.
3. It appears that on average, with the same education level, people aged 40-60 are earning more. This could be due to their wealth of experience.
4. It seems like there isn't much linear correlation between Education and Race. Regardless of Race, Education does help to get a higher income.
5. With the same level of education, veterans tend to fetch a higher salary.
6. With the same formal education level, having an extra professional certificate do help to compensate a lower education level and fetch a higher salary.
7. It appears that, for the same education level, having disability will result in one having a lower pay, in general.
8. With the same level of education, having hearing or visual disability will still fetch about the same income range.
9. For those without a degree, having concentration disability will result in one having a lower pay, in general.
10. Across the various citizenship, with the same education level, they seem to fetch about the same income range. However non-citizens tend to fetch a lower income range among the various citizenship status.
11. It appears that across the various industry, higher education will generally result in higher pay. However, in the Transportation and Utilities Industry (6), having higher education beyond a degree does not bring about an increasing trend in salary. Generally, the Public Administration (13) pays more than other industries for the same education level.
12. It appears that Education does not help much in occupations relating to Farming, Fishing and Foresty as well as Transport and material moving occupations.
12.It appears that regardless of private, public or self-employed, having a higher education does increase one's salary in general. However, education is less likely to one's pay as much if one is self-employed (5&6).
14. Regardless of education level, the work hours needed to achieve the same income range is about the same.
15. Within the same income range, males work longer hours than females.
16. For races with significant representation (white only and black only) in the survey, it seems like the hours worked is largely consistent across the various races.
17. It appears that veterans work longer for the same income class.
18. Regardless of whether one has a professional certificate, the hours worked for the same income range are about the same.
19. Reople with grooming, errands and concentration disabilities work less on average for the same income range.
20. Regardless of disability, for the same income class, the hours worked tend to be about the same except for the lowest income class (1) where people with disability work less hours.
21. The hours worked for each income range, across the various citizenship status, are largely consistent.
22. The agriculture, foresty, fishing and hunting as well as mining industries have the longest working hours. The other industries tend to be about the same.
23. Similarly, we see jobs relating to farming, fishing and foresty (6) have the longest working hours.
24. The hours worked across various workclass are quite consistent except those who are self-employed and without an incorporated company. This could be due to the fact that they may be freelance workers with lower working hours. Those who are self-employed with an incorporated company tend to work longer than the rest. This could be because they have generally greater responsibility within the company.

#
## Machine Learning (Decision Tree Classifier) ##
In this notebook, we explored the use of a Decision Tree Classifier.
- Our base model of max depth 3 yielded a f1 score of 0.47628.
- Through hyperparameter (max depth) tuning, we found the optimal max depth is about 7-13.
- We conducted cross-validation using GridSearchCV and found the optimal max depth is 11 and this model yielded a f1 score of 0.53561.
- Industry, Disability, Age and Occupation Group are the top factors considered by our decision tree classifier.

#
## Feature Engineering ##
In this notebook, we did feature scaling (numerical) using MinMax Scaler and dimension reduction through feature selection (categorical) using Mutual Information and Chi-Squared Test. The categorical features with the significant dependence with Salary are: Occupation, Education, Less than 35hrs for at least 1 week, Occupation Group, Longest Industry, More than 35hrs weekly, Industry, Detailed Household Status, Marital.

#
## Machine Learning (Support Vector Machine) ##

#
## Machine Learning (K-Nearest-Neighbours) ##

#
## Machine Learning (Multilayer Perceptron) ##

#
## Machine Learning (XGBoost Classifier) ##
In this notebook, we explored the use of a Gradient Boosting Classifier.
- Our base model of max depth 3, n_estimators 300 and subsample 0.7 yield a f1 score of 0.57372.
- Through hyperparameters (max depth, n_estimators and subsample) tuning, we estimated the optimal max depth to be 7-12.
- After cross-validation, we found the optimal hyperparameters to be max depth=3, n_estimators=150 and subsample=0.8. This model yield a f1 score of 0.52658.

#
## Conclusions and Recommendations ##

#
## New tools we have learnt ##
- Data Visualisation: GraphViz
- Feature Engineering: MinMax Scaler, Mutual Information, Chi-Squared Test
- Cross-Validation: GridSearchCV
- ML models: XGBoost Classifier, Multilayer Perceptron, Support Vector Machine, K-Nearest-Neighbours
