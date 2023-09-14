# Bank_Loan_Case_Study

- [Project Description](#project-Description)
- [Business Understanding](#business-understanding)
- [Data Understanding](#data-understanding)
- [Business Objectives](#business-objectives)
- [Approach and Tech Stack Used](#approach-and-tech-stack-used)
- [Analytics and Insights](#analytics-and-insights)
  - [1) Handling Missing Data](#handling-missing-data)

### Project Description
This case study aims to give you an idea of applying EDA in a real business scenario. In
this case study, apart from applying the techniques that I have learnt in the EDA
module, I would like to develop a basic understanding of risk analytics in banking and
financial services and understand how data is used to minimize the risk of losing money
while lending to customers.

### Business Understanding
The loan providing companies find it hard to give loans to the people due to their
insufficient or non-existent credit history. Because of that, some consumers use it as their
advantage by becoming a defaulter. Suppose you work for a consumer finance company
which specialises in lending various types of loans to urban customers. You have to use
EDA to analyse the patterns present in the data. This will ensure that the applicants
capable of repaying the loan are not rejected.

When the company receives a loan application, the company has to decide for loan
approval based on the applicant’s profile. 
Two types of risks are associated with the bank’s
decision:
- If the applicant is likely to repay the loan, then not approving the loan results in a loss
of business to the company.
- If the applicant is not likely to repay the loan, i.e. he/she is likely to default, then
approving the loan may lead to a financial loss for the company.

The data given below contains the information about the loan application at the time
of applying for the loan. 
It contains two types of `scenarios`:
- The client with payment difficulties: he/she had late payment more than X days on at
least one of the first Y instalments of the loan in our sample
- All other cases: All other cases when the payment is paid on time.

When a client applies for a loan, there are four types of decisions that could be taken by
the client/company:
- Approved: The company has approved loan application
- Cancelled: The client cancelled the application sometime during approval. Either the
client changed her/his mind about the loan or in some cases due to a higher risk of
the client he received worse pricing which he did not want.
- Refused: The company had rejected the loan (because the client does not meet their
requirements etc.).
- Unused Offer: Loan has been cancelled by the client but on different stages of the
process.
### Business Objectives
It aims to identify patterns which indicate if a client has difficulty paying their
installments which may be used for taking actions such as denying the loan, reducing the
amount of loan, lending (to risky applicants) at a higher interest rate, etc. This will ensure
that the consumers capable of repaying the loan are not rejected. Identification of such
applicants using EDA is the aim of this case study.

In other words, the company wants to understand the driving factors (or driver
variables) behind loan default, i.e. the variables which are strong indicators of default.
The company can utilize this knowledge for its portfolio and risk assessment.

To develop your understanding of the domain, you are advised to independently research
a little about risk analytics – understanding the types of variables and their significance
should be enough).

### Data Understanding 
1. application_data.csv: contains all the information of the client at the time of
application.The data is about whether a client has payment difficulties.

- [Download Here](https://docs.google.com/spreadsheets/d/1G4cweFtW4fMXPFLhrwvRZRPwhe-rhbfoufN9Zm15cKE/edit#gid=848798451)

2. columns_descrption.csv: is data dictionary which describes the meaning of the
variables.

- [Download Here](https://docs.google.com/spreadsheets/d/1W3AMPHCq5J2bEeWu-m7LYwrW4WPtj6QVfyXbG2ge_ZI/edit#gid=939882734)

### Approach and Tech Stack Used
- For this project I used Jupyter Notebook (Anaconda) to run my queries
and charts.
- The notebook extends the console-based approach to interactive
computing in a qualitatively new direction, providing a web-based
application suitable for capturing the whole computation process:
  - developing,
  - documenting and
  - executing code,
  - as well as communicating the results.
- The Jupyter notebook combines two
components:
  - ***A web application:*** a browser-based tool for interactive authoring of
documents which combine explanatory text, mathematics,
computations and their rich media output.
  - ***Notebook documents:*** a representation of all content visible in the
web application, including inputs and outputs of the computations,
explanatory text, mathematics, images, and rich media representations
of objects.
- This project helped me in understanding the tables at a much-detailed
manner and helped to improve my strength in extracting data from
tables in a more efficient manner.

### Analytics and Insights

#### Handling Missing Data
It is essential to handle missing data effectively to ensure the accuracy of the analysis.
Importing the necessary libraries for doing analysis.

- ***pandas** is a fast, powerful, flexible and easy to use open source data analysis and manipulation tool,
built on top of the Python programming language.*
- ***Matplotlib** is a comprehensive library for creating static, animated, and interactive visualizations in Python.*
- ***Seaborn** is a Python data visualization library based on matplotlib. It provides a high-level interface for drawing attractive and informative statistical graphics.*
    
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```
Loading the dataset
```
application_data = pd.read_csv('application_data.csv')
```
keeping the original dataset safe and doing all the analysis in **app_data**
```
app_data = pd.read_csv('application_data.csv')
```
setting the display option to display all rows and columns for our convinience
```
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)
```
Finding the count of Missing number of rows from every Column and sorting the result in ascending order based on the MissingCount
```
missing_count = app_data.isna().sum().sort_values(ascending = False)
print(missing_count)
```

![4](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/90aa6173-fcb0-4a65-b43d-5ba3171de441)

```
plt.figure(figsize=(10,60))
missing_count.sort_values(ascending=True).plot(kind='barh', color = 'skyblue')
plt.show()
```

![5](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/eba5b383-b3b4-44f6-8327-b2b1ecbbd366)

```
Rounding the Missing Values to 2 decimals and converting the count to Percentages for our convinience 
missing_count_per = round(((app_data.isna().sum()/len(app_data))*100).sort_values(ascending=False),2)
print(missing_count_per)
```
![6](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/1ee33a81-3d70-4042-b1f9-08bb55a367aa)
```
plt.figure(figsize=(10,60))
ax = missing_count_per.plot(kind='barh', color = 'blue')

ax.invert_yaxis()
for i,v in enumerate(missing_count_per):
    ax.text(v,i,str(v),ha='right',va='center',fontsize=10,color='white',fontweight='bold')
plt.show()
```
![7](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/c1836346-60c4-45a3-b2b8-5a42b63b326b)

Calculating the Threshold
```
threshold = (50/100) * len(app_data)
print(round(threshold))
```
If the column Missing Count is greater than the Threshold Imputing those with ***Missing*** Value 
And finally checking is the missing count is 0 or not 
```
columns_grt_threshold = missing_count[missing_count>threshold].index.tolist()
print(columns_grt_threshold)

for column in columns_grt_threshold:
    app_data[column].fillna("Missing",inplace=True)

app_data[columns_grt_threshold].isna().sum()
```
![8](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/5f2cc801-6e66-4b38-879b-119a9854febf)

Checking the columns where the Missing count is lessthan threshold and not equall to 0
```
columns_lt_threshold = missing_count[(missing_count<threshold) & (missing_count != 0)].index.tolist()
print(columns_lt_threshold)

app_data[columns_lt_threshold].isna().sum()
```
![9](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/2e8629c1-67f9-4b46-a8e8-0da14996d9a9)
Among those columns which i mentioned aboove making few columns Missing values to ***MIssing*** as they are required for analysis and not droping those may be they required for analysis further.
```
columns_lt_threshold_1 = ['FLOORSMAX_MODE', 'FLOORSMAX_MEDI', 'FLOORSMAX_AVG', 'YEARS_BEGINEXPLUATATION_MODE', 'YEARS_BEGINEXPLUATATION_MEDI', 'YEARS_BEGINEXPLUATATION_AVG', 'TOTALAREA_MODE', 'EMERGENCYSTATE_MODE', 'OCCUPATION_TYPE', 'EXT_SOURCE_3', 'AMT_REQ_CREDIT_BUREAU_HOUR', 'AMT_REQ_CREDIT_BUREAU_DAY', 'AMT_REQ_CREDIT_BUREAU_WEEK', 'AMT_REQ_CREDIT_BUREAU_MON', 'AMT_REQ_CREDIT_BUREAU_QRT', 'AMT_REQ_CREDIT_BUREAU_YEAR']

for column in columns_lt_threshold_1:
    app_data[column].fillna("Missing",inplace = True)

app_data[columns_lt_threshold_1].isna().sum()
```
Rest of the columns
```
columns_lt_threshold_2 = ['NAME_TYPE_SUITE', 'OBS_30_CNT_SOCIAL_CIRCLE', 'DEF_30_CNT_SOCIAL_CIRCLE', 'OBS_60_CNT_SOCIAL_CIRCLE', 'DEF_60_CNT_SOCIAL_CIRCLE', 'EXT_SOURCE_2', 'AMT_GOODS_PRICE', 'AMT_ANNUITY', 'CNT_FAM_MEMBERS', 'DAYS_LAST_PHONE_CHANGE']

app_data[columns_lt_threshold_2].isna().sum()
```
![10](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/9db6ded3-5e3b-4ab7-90d5-4e28eff33e3d)


