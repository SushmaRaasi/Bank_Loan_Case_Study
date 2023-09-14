# Bank_Loan_Case_Study

- [Project Description](#project-Description)
- [Business Understanding](#business-understanding)
- [Data Understanding](#data-understanding)
- [Business Objectives](#business-objectives)
- [Approach and Tech Stack Used](#approach-and-tech-stack-used)
- [Analytics and Insights](#analytics-and-insights)
  - [1) Handling Missing Data](#handling-missing-data)
  - [2) Identify Outliers](#identify-outliers)
  - [3) Analyzing Data Imbalance](#analyzing-data-imbalance)

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
For *NAME_TYPE_SUITE* column replacing null values with Unaccompanied
```
app_data['NAME_TYPE_SUITE'].value_counts()
```
![11](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/e48364fc-bd63-4361-9d64-3884f0afef65)
```
app_data['NAME_TYPE_SUITE'].fillna("Unaccompanied",inplace=True)
app_data['NAME_TYPE_SUITE'].isna().sum()
```
0
*DEF_30_CNT_SOCIAL_CIRCLE,OBS_60_CNT_SOCIAL_CIRCLE,DEF_60_CNT_SOCIAL_CIRCLE,OBS_30_CNT_SOCIAL_CIRCLE*
```
DEF_30_median = app_data['DEF_30_CNT_SOCIAL_CIRCLE'].median()
OBS_60_median = app_data['OBS_60_CNT_SOCIAL_CIRCLE'].median()
DEF_60_median = app_data['DEF_60_CNT_SOCIAL_CIRCLE'].median()
OBS_30_median = app_data['OBS_30_CNT_SOCIAL_CIRCLE'].median()

print(f'DEF_30_CNT_SOCIAL_CIRCLE --> ',DEF_30_median)
print(f'OBS_60_CNT_SOCIAL_CIRCLE --> ',OBS_60_median)
print(f'DEF_60_CNT_SOCIAL_CIRCLE --> ',DEF_60_median)
print(f'OBS_30_CNT_SOCIAL_CIRCLE --> ',OBS_30_median)
```
![12](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/3478b44c-fab4-419c-98c5-2e73e709e405)
```
Social_circle_columns = ['DEF_30_CNT_SOCIAL_CIRCLE','OBS_60_CNT_SOCIAL_CIRCLE','DEF_60_CNT_SOCIAL_CIRCLE','OBS_30_CNT_SOCIAL_CIRCLE']

for column in Social_circle_columns:
    app_data[column].fillna(0,inplace=True)

app_data[Social_circle_columns].isna().sum()
```
![13](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/07e9072d-e6be-477d-a3eb-b2963ec39ce1)

```
rem_columns = ['EXT_SOURCE_2', 'AMT_GOODS_PRICE', 'AMT_ANNUITY', 'CNT_FAM_MEMBERS', 'DAYS_LAST_PHONE_CHANGE']

for column in rem_columns:
    med=round(app_data[column].median(),2)
    app_data[column].fillna(med,inplace=True)
    
app_data[rem_columns].isna().sum()
```
![14](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/0beaa30c-6d20-4411-8388-d0e3331432d1)

There are few columns like *DAYS_BIRTH,DAYS_EMPLOYED,DAYS_REGISTRATION,DAYS_ID_PUBLISH* are in days with -ve values.
To represent these columns in better way changing them to +ve values and to years which will very helpful in further analysis.

Created a function for those 4 columns 
```
def abs_round_days(column):
    return round(abs(app_data[column])/365,2)

app_data['DAYS_BIRTH_Years']=abs_round_days('DAYS_BIRTH')
app_data['DAYS_EMPLOYED_Years']=abs_round_days('DAYS_EMPLOYED')
app_data['DAYS_REGISTRATION_Years']=abs_round_days('DAYS_REGISTRATION')
app_data['DAYS_ID_PUBLISH_Years']=abs_round_days('DAYS_ID_PUBLISH')
```

Finding Credit Ratio Column
```
app_data['credit_ratio']= round((app_data['AMT_CREDIT']/app_data['AMT_INCOME_TOTAL']),2)
```
#### Identify Outliers

```
numerical_columns = app_data.select_dtypes(include=[np.number]).columns
print(numerical_columns)
```
![15](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/09f51fcb-2f9a-4a9d-a7b3-516019db2ea3)

```
def ploting(column_name):
    plt.figure(figsize=(12,6))
    sns.boxplot(data=app_data[column_name],orient='h')
    return plt.show()

ploting('CNT_CHILDREN')
```
![16](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/ac4137ac-3241-49f2-81cc-def4216ce3d0)

```
def outliers(column_name):
    Q1= app_data[column_name].quantile(0.25)
    Q3 = app_data[column_name].quantile(0.75)
    IQR = Q3-Q1
    UT = Q3+(1.5*IQR)
    LT=Q1-(1.5*IQR)
    Outliers = app_data[(app_data[column_name]<LT) | (app_data[column_name]>UT)]
    return (Outliers[column_name].value_counts())

outliers('CNT_CHILDREN')
```
![17](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/33a5018d-272c-4056-9d5d-6164c6fc895e)

Here i am grouping CNT_CHILDREN Column to represent the values in better way for further investigation.
```
bins = [-1,2,5,float('inf')]
bin_labels = ['0-2 Child','3-5 Child','6+ child']
app_data['CHILDREN CATEGORY'] = pd.cut(app_data['CNT_CHILDREN'],bins = bins, labels =bin_labels)
print(app_data['CHILDREN CATEGORY'].value_counts())
```
![18](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/3050da9d-06e0-4c69-a439-40587907c8a7)

```
ploting('AMT_INCOME_TOTAL')
```
![image](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/9c135b58-dd9b-4b9d-b509-48de54889034)

```
outliers('AMT_INCOME_TOTAL')
```
Here i am grouping the AMT_INCOME_TOTAL to represent the values in better way for further investigation

```
bins = [-1,100000,200000,300000,400000,500000,600000,700000,800000,900000,1000000,float('inf')]
bins_labels = ['0-1L','1-2L','2-3L','3-4L','4-5L','5-6L','6-7L','7-8L','8-9L','9-10L','10L+']
app_data['AMT_INCOME_TOTAL_RANGE']=pd.cut(app_data['AMT_INCOME_TOTAL'],bins = bins,labels =bins_labels)
print(app_data['AMT_INCOME_TOTAL_RANGE'].value_counts())
```
![20](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/0c1c5043-3f51-485e-aeb9-d3f79069eb1f)

```
app_data['AMT_CREDIT_Lakhs'] = round(app_data['AMT_CREDIT']/100000,2)
# print(app_data[['AMT_CREDIT_Lakhs','AMT_CREDIT']])

ploting('AMT_CREDIT_Lakhs')
outliers('AMT_CREDIT_Lakhs')
```
![21](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/cf048ac6-c8a3-4c07-8589-13ec6edc816e)

Here i am grouping the AMT_CREDIT_Lakhs to represent the values in better way for further investigation
```
bins = [-1,5,10,15,20,25,30,35,40,float('inf')]
bins_labels = ['0-5L','6-10L','11-15L','16-20L','21-25L','26-30L','31-35L','36-40L','40L+']
app_data['AMT_CREDIT_RANGE']=pd.cut(app_data['AMT_CREDIT_Lakhs'],bins=bins, labels = bins_labels)
print(app_data['AMT_CREDIT_RANGE'].value_counts().sort_values(ascending=True))
```
![22](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/1a5465b5-fe1c-471b-a8a3-c55b6e48b61e)

```
app_data['AMT_GOODS_PRICE_Lakhs']=round(app_data['AMT_GOODS_PRICE']/100000,2)
ploting('AMT_GOODS_PRICE_Lakhs')
```
![23](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/abcfbfc0-12d1-4d1a-b6d3-178de9d6ef3f)

```
outliers('AMT_GOODS_PRICE_Lakhs')
bins = [-1,5,10,15,20,25,30,35,40,float('inf')]
bins_labels = ['0-5L','6-10L','11-15L','16-20L','21-25L','26-30L','31-35L','36-40L','40L+']
app_data['AMT_GOODS_PRICE_RANGE']=pd.cut(app_data['AMT_GOODS_PRICE_Lakhs'],bins=bins, labels = bins_labels)
print(app_data['AMT_GOODS_PRICE_RANGE'].value_counts().sort_values(ascending=True))
```
![24](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/a16c6f6c-8619-4500-b79d-66ebc78ec0eb)

```
ploting('DAYS_BIRTH_Years')
```
![25](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/e44a25f4-498b-491b-8d15-6d871d9df95d)

Based on the above box plot i could see there is no outliers but the age values can t be in decimal format hence changing to ranges bybdividede them in to categories

```
bins = [-1,10,20,30,40,50,60,70,float('inf')]
bin_labels = ['0-10','11-20','21-30','31-40','41-50','51-60','61-70','70+']
app_data['DAYS_BIRTH_Age_Range']=pd.cut(app_data['DAYS_BIRTH_Years'],bins=bins,labels=bin_labels)
app_data['DAYS_BIRTH_Age_Range'].value_counts()
```
![26](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/1d214fd9-cd03-44ec-813e-7a1cb9e6585d)

```
ploting('DAYS_EMPLOYED_Years')
```
![27](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/c32f70f9-4a50-4ba1-8f67-ba8c1b59fe3a)

```
outliers('DAYS_EMPLOYED_Years')
bins = [-1,10,20,30,40,50,60,70,80,90,100,500,1000,float('inf')]
bin_labels = ['0-10Y','11-20Y','21-30Y','31-40Y','41-50Y','51-60Y','61-70Y','71-80Y','81-90Y','91-100Y','101-500Y','501-1000','1000+']
app_data['DAYS_EMPLOYED_RANGE']= pd.cut(app_data['DAYS_EMPLOYED_Years'],bins=bins,labels=bin_labels)
app_data['DAYS_EMPLOYED_RANGE'].value_counts()
```
![28](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/365f25e2-d9fe-4f6e-ae72-1e60027748f9)
Here i am grouping the DAYS_EMPLOYED_Years to represent the values in better way for further investigation

#### Analyzing Data Imbalance

```
plt.figure(figsize=(6,6))
sns.countplot(data=app_data,x='TARGET')
plt.show()
```
![29](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/ad60cf8f-cad8-4788-af64-e6738b12c54a)

```
class_counts=app_data['TARGET'].value_counts()
print(class_counts)
```
![30](https://github.com/SushmaRaasi/Bank_Loan_Case_Study/assets/79751402/2838df88-a6f7-4789-8ff4-a1c63757378a)

```
Ratio_Imbalance = round(class_counts[1]/class_counts[0],2)
print(Ratio_Imbalance)
```
***0.09***
**Conclusion**
*A ratio of 0.09 means that for every 100 loan applications:*

About 91 of them belong to Category 0 (people with no difficulties).
Only 9 of them belong to Category 1 (people with repayment difficulties).


































