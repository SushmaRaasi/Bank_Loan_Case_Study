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
<p>This case study aims to give you an idea of applying EDA in a real business scenario. In this case study, apart from applying the techniques that I have learnt in the EDA module, I would like to develop a basic understanding of risk analytics in banking and financial services and understand how data is used to minimize the risk of losing money while lending to customers.</p>

### Business Understanding
<p>The loan providing companies find it hard to give loans to the people due to their
insufficient or non-existent credit history. Because of that, some consumers use it as their advantage by becoming a defaulter. Suppose you work for a consumer finance company which specialises in lending various types of loans to urban customers. You have to use EDA to analyse the patterns present in the data. This will ensure that the applicants capable of repaying the loan are not rejected.
</p>

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

### DataSet
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

1 

```
plt.figure(figsize=(10,60))
missing_count.sort_values(ascending=True).plot(kind='barh', color = 'skyblue')
plt.show()
```

2

<br>
Rounding the Missing Values to 2 decimals and converting the count to Percentages for our convinience 

```
missing_count_per = round(((app_data.isna().sum()/len(app_data))*100).sort_values(ascending=False),2)
print(missing_count_per)
```
3

```
plt.figure(figsize=(10,60))
ax = missing_count_per.plot(kind='barh', color = 'blue')

ax.invert_yaxis()
for i,v in enumerate(missing_count_per):
    ax.text(v,i,str(v),ha='right',va='center',fontsize=10,color='white',fontweight='bold')
plt.show()
```
4

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
5
<br>
Checking the columns where the Missing count is lessthan threshold and not equall to 0
```
columns_lt_threshold = missing_count[(missing_count<threshold) & (missing_count != 0)].index.tolist()
print(columns_lt_threshold)

app_data[columns_lt_threshold].isna().sum()
```
6

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
7
For *NAME_TYPE_SUITE* column replacing null values with Unaccompanied
```
app_data['NAME_TYPE_SUITE'].value_counts()
```
8
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
9

```
Social_circle_columns = ['DEF_30_CNT_SOCIAL_CIRCLE','OBS_60_CNT_SOCIAL_CIRCLE','DEF_60_CNT_SOCIAL_CIRCLE','OBS_30_CNT_SOCIAL_CIRCLE']

for column in Social_circle_columns:
    app_data[column].fillna(0,inplace=True)

app_data[Social_circle_columns].isna().sum()
```
10

```
rem_columns = ['EXT_SOURCE_2', 'AMT_GOODS_PRICE', 'AMT_ANNUITY', 'CNT_FAM_MEMBERS', 'DAYS_LAST_PHONE_CHANGE']

for column in rem_columns:
    med=round(app_data[column].median(),2)
    app_data[column].fillna(med,inplace=True)
    
app_data[rem_columns].isna().sum()
```
11

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
def ploting(column_name):
    plt.figure(figsize=(12,6))
    sns.boxplot(data=app_data[column_name],orient='h')
    return plt.show()

ploting('CNT_CHILDREN')

```
12

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
13

Here i am grouping CNT_CHILDREN Column to represent the values in better way for further investigation.
```
bins = [-1,2,5,float('inf')]
bin_labels = ['0-2 Child','3-5 Child','6+ child']
app_data['CHILDREN CATEGORY'] = pd.cut(app_data['CNT_CHILDREN'],bins = bins, labels =bin_labels)
print(app_data['CHILDREN CATEGORY'].value_counts())
```
14

```
ploting('AMT_INCOME_TOTAL')
```
15

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
16

```
app_data['AMT_CREDIT_Lakhs'] = round(app_data['AMT_CREDIT']/100000,2)
# print(app_data[['AMT_CREDIT_Lakhs','AMT_CREDIT']])

ploting('AMT_CREDIT_Lakhs')
outliers('AMT_CREDIT_Lakhs')
```
17

Here i am grouping the AMT_CREDIT_Lakhs to represent the values in better way for further investigation
```
bins = [-1,5,10,15,20,25,30,35,40,float('inf')]
bins_labels = ['0-5L','6-10L','11-15L','16-20L','21-25L','26-30L','31-35L','36-40L','40L+']
app_data['AMT_CREDIT_RANGE']=pd.cut(app_data['AMT_CREDIT_Lakhs'],bins=bins, labels = bins_labels)
print(app_data['AMT_CREDIT_RANGE'].value_counts().sort_values(ascending=True))
```
18

```
app_data['AMT_GOODS_PRICE_Lakhs']=round(app_data['AMT_GOODS_PRICE']/100000,2)
ploting('AMT_GOODS_PRICE_Lakhs')
```
19

```
outliers('AMT_GOODS_PRICE_Lakhs')
bins = [-1,5,10,15,20,25,30,35,40,float('inf')]
bins_labels = ['0-5L','6-10L','11-15L','16-20L','21-25L','26-30L','31-35L','36-40L','40L+']
app_data['AMT_GOODS_PRICE_RANGE']=pd.cut(app_data['AMT_GOODS_PRICE_Lakhs'],bins=bins, labels = bins_labels)
print(app_data['AMT_GOODS_PRICE_RANGE'].value_counts().sort_values(ascending=True))
```
20

```
ploting('DAYS_BIRTH_Years')
```
21

Based on the above box plot i could see there is no outliers but the age values can t be in decimal format hence changing to ranges bybdividede them in to categories

```
bins = [-1,10,20,30,40,50,60,70,float('inf')]
bin_labels = ['0-10','11-20','21-30','31-40','41-50','51-60','61-70','70+']
app_data['DAYS_BIRTH_Age_Range']=pd.cut(app_data['DAYS_BIRTH_Years'],bins=bins,labels=bin_labels)
app_data['DAYS_BIRTH_Age_Range'].value_counts()
```
22

```
ploting('DAYS_EMPLOYED_Years')
```
23

```
outliers('DAYS_EMPLOYED_Years')
bins = [-1,10,20,30,40,50,60,70,80,90,100,500,1000,float('inf')]
bin_labels = ['0-10Y','11-20Y','21-30Y','31-40Y','41-50Y','51-60Y','61-70Y','71-80Y','81-90Y','91-100Y','101-500Y','501-1000','1000+']
app_data['DAYS_EMPLOYED_RANGE']= pd.cut(app_data['DAYS_EMPLOYED_Years'],bins=bins,labels=bin_labels)
app_data['DAYS_EMPLOYED_RANGE'].value_counts()
```
24

Here i am grouping the DAYS_EMPLOYED_Years to represent the values in better way for further investigation

#### Analyzing Data Imbalance

```
plt.figure(figsize=(6,6))
sns.countplot(data=app_data,x='TARGET')
plt.show()
```
25

```
class_counts=app_data['TARGET'].value_counts()
print(class_counts)
```
26

```
Ratio_Imbalance = round(class_counts[1]/class_counts[0],2)
print(Ratio_Imbalance)
```
***0.09***

**Conclusion**

*A ratio of 0.09 means that for every 100 loan applications:*

About 91 of them belong to Category 0 (people with no difficulties).
Only 9 of them belong to Category 1 (people with repayment difficulties).

#### Uni Variant Analysis

```
Numerical_columns = ['AMT_INCOME_TOTAL_Lakhs','AMT_ANNUITY','CNT_FAM_MEMBERS','AMT_CREDIT_Lakhs','AMT_GOODS_PRICE_Lakhs','DAYS_BIRTH_Years','DAYS_EMPLOYED_Years','DAYS_REGISTRATION_Years','DAYS_ID_PUBLISH_Years','credit_ratio']
```
```
Categorical_columns = ['TARGET','NAME_CONTRACT_TYPE','CODE_GENDER','FLAG_OWN_CAR','FLAG_OWN_REALTY','CNT_CHILDREN','NAME_TYPE_SUITE','NAME_INCOME_TYPE','NAME_EDUCATION_TYPE','NAME_FAMILY_STATUS','NAME_HOUSING_TYPE','FLAG_MOBIL','FLAG_EMP_PHONE','FLAG_WORK_PHONE','FLAG_CONT_MOBILE','FLAG_PHONE','FLAG_EMAIL','OCCUPATION_TYPE','REGION_RATING_CLIENT','REGION_RATING_CLIENT_W_CITY','WEEKDAY_APPR_PROCESS_START','ORGANIZATION_TYPE','CHILDREN CATEGORY','AMT_INCOME_TOTAL_RANGE','AMT_CREDIT_RANGE','AMT_GOODS_PRICE_RANGE','DAYS_BIRTH_Age_Range','DAYS_EMPLOYED_RANGE']
```
Summary Statistics for Numerical Columns

```
for col in Numerical_columns:
    print(col)
    Summary = app_data[col].describe()
    print(round(Summary,2))
```
27
28
29

```
def Uni_Analysis_Numerical(dataframe,column):
    sns.set(style='darkgrid')
    plt.figure(figsize=(25,7))
    
    plt.subplot(1,2,1)
    sns.boxplot(data=dataframe,x=column).set(title='Box Plot')
    
    plt.subplot(1,2,2)
    sns.histplot(data=dataframe[column]).set(title='Histogram')
    
    return plt.show()
                
for i in Numerical_columns:
           Uni_Analysis_Numerical(app_data,i) 
```
30
32
32
33
34
35
36

```
def Uni_Analysis_Categorical(dataframe,column):
    
    sns.set(style='darkgrid')
    plt.rcParams['figure.max_open_warning'] = 50
    plt.figure(figsize=(8,5))
    dataframe[column].value_counts().plot(kind='barh',width=0.2).set(title=column)
    plt.show

for i in Categorical_columns:
    Uni_Analysis_Categorical(app_data,i)
```
37
38
39
40
41
42
43
44

```
sns.set(style='darkgrid')
plt.figure(figsize=(15,20))
app_data['ORGANIZATION_TYPE'].value_counts().plot(kind='barh',width=1).set(title='ORGANIZATION_TYPE')
plt.show
```
45

#### Segmented Analysis
<ul>
  <li>CODE_GENDER - AMT_INCOME_TOTAL_Lakhs</li>
  ```
  app_data['CODE_GENDER'].value_counts()
```
  46
  Stratify the Data
  
  ```
  gender_groups = app_data.groupby(by='CODE_GENDER')
male_segment = gender_groups.get_group('M')
female_segment = gender_groups.get_group('F')
```
  Analyze Each Segment Separately

```
plt.figure(figsize=(20,6))

plt.subplot(1,3,1)
sns.histplot(male_segment['AMT_INCOME_TOTAL_Lakhs'],bins = 60)
plt.title('Male')


plt.subplot(1,3,2)
sns.histplot(female_segment['AMT_INCOME_TOTAL_Lakhs'],bins = 60)
plt.title('Female')

plt.show()
```
47
Calculating Descriptive Statistics

```
male_income_stats = male_segment['AMT_INCOME_TOTAL_Lakhs'].describe()
female_income_stats = female_segment['AMT_INCOME_TOTAL_Lakhs'].describe()
print('Descriptive Statistics of Male')
print(round(male_income_stats,2))
print('Descriptive Statistics of Female')
print(round(female_income_stats,2))
```
48
<ul>
  <li>Count: There are more female applicants (32,823) compared to male applicants (17,174).
</li>
  <li>Mean: On average, male applicants have a slightly higher income (1.94 Lakhs) compared to female applicants (1.59 Lakhs).</li>
  <li>Standard Deviation: The income distribution among females is more spread out (higher standard deviation of 6.51 Lakhs) compared to males (lower standard deviation of 1.12 Lakhs), indicating greater variability among female incomes.</li>
  <li>Minimum Income: The minimum reported income is similar for both genders.</li>
  <li>25th Percentile (Q1): The 25th percentile income for males is higher (1.35 Lakhs) compared to females (0.99 Lakhs), indicating that a larger proportion of female applicants have lower incomes.
</li>
  <li>Median: The median income (50th percentile) for males is higher (1.80 Lakhs) compared to females (1.35 Lakhs), suggesting that the income distribution for males is skewed slightly towards higher incomes.
</li>
  <li>75th Percentile (Q3): The 75th percentile income for males is also higher (2.25 Lakhs) compared to females (1.80 Lakhs), indicating that a larger proportion of male applicants have higher incomes.
</li>
  <li>Maximum Income: There is a significant difference in the maximum reported incomes, with females having a much higher maximum income than males.</li>
</ul>

<li>NAME_CONTRACT_TYPE - AMT_CREDIT</li>

```
app_data['NAME_CONTRACT_TYPE'].value_counts()
```
49
Stratify the Data

```
contract_groups = app_data.groupby(by='NAME_CONTRACT_TYPE')
CL_grp= contract_groups.get_group("Cash loans")
RL_grp= contract_groups.get_group("Revolving loans")
```
Analyze Each Segment Separately

```
plt.figure(figsize=(20,6))

plt.subplot(1,3,1)
sns.histplot(CL_grp['AMT_CREDIT_Lakhs'],bins = 60)
plt.title('Cash loans')


plt.subplot(1,3,2)
sns.histplot(RL_grp['AMT_CREDIT_Lakhs'],bins = 60)
plt.title('Revolving loans')

plt.show()
```
50
Calculating Descriptive Statistics

```
CL_stats = CL_grp['AMT_CREDIT_Lakhs'].describe()
RL_stats = RL_grp['AMT_CREDIT_Lakhs'].describe()
print('Descriptive Statistics of Cash loans')
print(round(CL_stats,2))
print('Descriptive Statistics of Revolving loans')
print(round(RL_stats,2))
```
51
<ul>
  <li>Count: There are more observations for "Cash loans" (45,276) compared to "Revolving loans" (4,723), indicating that "Cash loans" are more common in the dataset.
</li>
  <li>Mean: "Cash loans" have a higher mean loan amount (approximately 6.29 lakhs) compared to "Revolving loans" (approximately 3.19 lakhs), suggesting that, on average, "Cash loans" have higher loan amounts.
</li>
  <li>Standard Deviation: "Cash loans" also have a higher standard deviation (4.05 lakhs) compared to "Revolving loans" (2.32 lakhs), indicating greater variability in loan amounts for "Cash loans."
</li>
  <li>Minimum: The minimum loan amount for "Cash loans" is 0.45 lakhs, while for "Revolving loans," it's 1.35 lakhs. "Cash loans" have a wider range of minimum loan amounts.</li>
  <li>Quartiles (25th, 50th, 75th Percentiles): "Cash loans" generally have higher values at each quartile compared to "Revolving loans." This indicates that the loan amount distribution for "Cash loans" is shifted towards higher values.</li>
  <li>Maximum: "Cash loans" have a higher maximum loan amount of 40.50 lakhs compared to "Revolving loans," which have a maximum of 22.50 lakhs.
</li>
  <p>In summary, "Cash loans" tend to have higher average loan amounts and greater variability in loan amounts compared to "Revolving loans." The quartiles also show that "Cash loans" have a distribution shifted towards higher values.</p>
</ul>
</ul>

#### Bi Variant Analysis
<ol>
  <li>NAME_EDUCATION_TYPE  and  NAME_FAMILY_STATUS</li>
  Categorical vs. Categorical Variables
This could involve creating contingency tables and performing chi-square tests to determine if there is a significant association between these categorical variables.
<br>
  Creating a Contingency Table
  
  ```
contigency_table = pd.crosstab(app_data['NAME_EDUCATION_TYPE'],app_data['NAME_FAMILY_STATUS'])
contigency_table
```
52

```
chi2,p,_,_=chi2(contigency_table)
print("chi2 is ",chi2)
print("p is",p)
```
Interpreting the Results
<ul>
  <li>here p value is very less than significance level (e.g., 0.05) hence i can conclude that there is a significant association between 'NAME_EDUCATION_TYPE' and 'NAME_FAMILY_STATUS.'</li>
  <li>The Chi-Square statistic is approximately 663.12. This statistic measures the strength of the association between the two categorical variables in your contingency table. Larger values indicate a stronger association.</li>
</ul>
54

<li>NAME_EDUCATION_TYPE and AMT_INCOME_TOTAL_RANGE</li>

```
categorical_variable = 'NAME_EDUCATION_TYPE'
numerical_variable = 'AMT_INCOME_TOTAL_Lakhs'
education_types = app_data['NAME_EDUCATION_TYPE'].unique()
education_types
```
55

```
grouped_data=app_data.groupby(by=categorical_variable).agg({numerical_variable:['mean', 'median', 'std']}).reset_index()

plt.figure(figsize=(15, 6))

plt.subplot(1,2,1)
sns.barplot(data=grouped_data, x=categorical_variable, y=(numerical_variable,'mean'), palette=['red','blue','green'])  # You can choose 'mean', 'median', or other statistics
plt.xticks(rotation=45)  # Rotate x-axis labels for better readability
plt.xlabel(categorical_variable)
plt.ylabel(f'Mean {numerical_variable}')
plt.title(f'Mean {numerical_variable} by {categorical_variable}')
```
```
plt.subplot(1,2,2)
sns.barplot(data=grouped_data, x=categorical_variable, y=(numerical_variable,'median'), palette=['red','blue','green'])  # You can choose 'mean', 'median', or other statistics
plt.xticks(rotation=45)  # Rotate x-axis labels for better readability
plt.xlabel(categorical_variable)
plt.ylabel(f'Median {numerical_variable}')
plt.title(f'Median {numerical_variable} by {categorical_variable}')

plt.show()
```
56

```
plt.figure(figsize=(6,3))
sns.barplot(data=grouped_data, x=categorical_variable, y=(numerical_variable,'std'), palette=['red','blue','green'])  # You can choose 'mean', 'median', or other statistics
plt.xticks(rotation=45)  # Rotate x-axis labels for better readability
plt.xlabel(categorical_variable)
plt.ylabel(f'std {numerical_variable}')
plt.title(f'std {numerical_variable} by {categorical_variable}')
plt.show()
```
57

<li>AMT_CREDIT and AMT_ANNUITY</li>
Numerical Vs Numerical

```
correlation_coefficient = app_data['AMT_CREDIT'].corr(app_data['AMT_ANNUITY'])
round(correlation_coefficient,2)
```
`0.77`

```
plt.figure(figsize=(8,8))
plt.scatter(app_data['AMT_CREDIT_Lakhs'],app_data['AMT_ANNUITY'],alpha=0.5)
plt.xlabel('AMT_CREDIT_Lakhs')
plt.ylabel('AMT_ANNUITY')
plt.title('AMT_CREDIT Vs AMT_ANNUITY')
plt.grid(True)
plt.show()
```
58
<ul>
  <li>Positive Correlation: The positive sign of the correlation coefficient (0.77) indicates that as one variable, 'AMT_CREDIT,' increases, the other variable, 'AMT_ANNUITY,' tends to increase as well. In other words, there is a tendency for borrowers who take larger loans ('AMT_CREDIT') to have higher annuities ('AMT_ANNUITY').
</li>
  <li>Strength of Correlation: A correlation coefficient of 0.77 is relatively high, indicating a strong linear relationship between the two variables. This suggests that changes in 'AMT_CREDIT' are closely associated with corresponding changes in 'AMT_ANNUITY.'</li>
  <li>Scatter Plot: When you created the scatter plot, you likely observed a diagonal pattern where data points tend to cluster along a line that slopes upward. This pattern visually confirms the positive correlation.</li>
  <li>Practical Implications: In practical terms, this correlation suggests that financial institutions or lenders may use 'AMT_CREDIT' to estimate or determine 'AMT_ANNUITY' when issuing loans. Borrowers who request larger loan amounts can expect to have higher monthly annuity payments.
</li>
</ul>

```
app_data.reset_index(drop=True,inplace=True)
app_data.index = app_data.index+1
app_data.head()
```
59
<li>DAYS_BIRTH and DAYS_EMPLOYED</li>

```
plt.figure(figsize=(12,6))
plt.plot(app_data.index,app_data['DAYS_BIRTH_Age_Range'])
plt.show()
```
60

```
# DAYS_EMPLOYED_Years
plt.figure(figsize=(12,6))
plt.plot(app_data.index,app_data['DAYS_EMPLOYED_RANGE'])
plt.show()
```
61

```
plt.figure(figsize=(8, 6))
plt.scatter(app_data['DAYS_BIRTH_Age_Range'], app_data['DAYS_EMPLOYED_RANGE'], alpha=0.5)
plt.xlabel('DAYS_BIRTH_Age_Range')
plt.ylabel('DAYS_EMPLOYED_RANGE')
plt.title('Scatter Plot: DAYS_BIRTH vs. DAYS_EMPLOYED')
plt.show()
```
62

```
correlation_coefficient = app_data['DAYS_BIRTH_Years'].corr(app_data['DAYS_EMPLOYED_Years'])
round(correlation_coefficient,2)
```
0.62
<ul>
  <li>A positive correlation means that as one variable (in this case, 'DAYS_BIRTH_Years') increases, the other variable ('DAYS_EMPLOYED_Years') tends to increase as well.
</li>
  <li>The correlation coefficient value of 0.62 suggests that there is a moderate level of correlation between these two variables. It's not a perfect correlation, but there is a noticeable tendency for individuals who are older ('DAYS_BIRTH_Years' is higher) to have longer employment durations ('DAYS_EMPLOYED_Years' is higher) and vice versa.</li>
</ul>
</ol>

### Identify Top Correlations for Different Scenarios
<ul>
  <li>1 - client with payment difficulties
</li>
  <li>0 - all other cases</li>
</ul>

```
Numerical_columns = 'CNT_CHILDREN','AMT_INCOME_TOTAL','AMT_CREDIT','AMT_ANNUITY','AMT_GOODS_PRICE'
```
```
app_data_Numerical['TARGET'] == 1
val=list(app_data_Numerical['TARGET'] == 1)
payment_difficulties_data = app_data_Numerical[val]
payment_difficulties_data
```
63

```
mask = app_data_Numerical['TARGET'] == 0
other_cases = app_data_Numerical[mask]
other_cases
```
64
<ol>
  <li></li>
  
  ```
t_stast,p_value = stats.ttest_ind(payment_difficulties_data['CNT_CHILDREN'],other_cases['CNT_CHILDREN'],equal_var=False)
print(f't_stast is: ',t_stast)
print(f'p_value is: ',p_value)
```
65
<p>The small p-value (much less than the common significance level of 0.05) indicates that there is a statistically significant difference in the means of 'CNT_CHILDREN' between the group with payment difficulties (TARGET = 1) and the group without payment difficulties (TARGET = 0).

</p>
<li></li>

```
t_stast,p_value = stats.ttest_ind(payment_difficulties_data['AMT_INCOME_TOTAL'],other_cases['AMT_INCOME_TOTAL'],equal_var=False)
print(f't_stast is: ',t_stast)
print(f'p_value is: ',p_value)
```
66
<p>With a p-value of 0.464, it means that there is not enough statistical evidence to conclude that the difference in 'AMT_INCOME_TOTAL' between the payment difficulties group and the other cases group is statistically significant. In other words, the income levels of these two groups are not significantly different based on this test.</p>
<li></li>

```
t_stast,p_value = stats.ttest_ind(payment_difficulties_data['AMT_CREDIT'],other_cases['AMT_CREDIT'],equal_var=False)
print(f't_stast is: ',t_stast)
print(f'p_value is: ',p_value)
```
67
<p>With a p-value that is extremely close to zero (4.586e-17), it indicates a very high level of statistical significance. Therefore, you can conclude that there is a significant difference in 'AMT_CREDIT' between the payment difficulties group and the other cases group. In practical terms, it means that the credit amounts between these two groups are significantly different based on this test.</p>
<li></li>

```
t_stast,p_value = stats.ttest_ind(payment_difficulties_data['AMT_ANNUITY'],other_cases['AMT_ANNUITY'],equal_var=False)
print(f't_stast is: ',t_stast)
print(f'p_value is: ',p_value)
```
68
<p>The small p-value of 0.0012 indicates a statistically significant difference in 'AMT_ANNUITY' between the payment difficulties group and the other cases group. Therefore, you can conclude that 'AMT_ANNUITY' is likely to be a significant variable for distinguishing between cases with payment difficulties and other cases.</p>
<li></li>

```
t_stast,p_value = stats.ttest_ind(payment_difficulties_data['AMT_GOODS_PRICE'],other_cases['AMT_GOODS_PRICE'],equal_var=False)
print(f't_stast is: ',t_stast)
print(f'p_value is: ',p_value)
```
69
</ol>

### Hypothetical Testing
<ol>
  <li>Gender & Payment Difficulty:</li>
  <p>Male clients might exhibit different payment behaviors than female clients.</p>
  <p>Null Hypothesis (H0): gender does not influence payment behavior.
Alternate Hypothesis (H1): Gender does influence payment behavior.
</p>

  ```
contigency_table = pd.crosstab(app_data['CODE_GENDER'],app_data['TARGET'])
contigency_table
```
70

```
chi2_stat,p_value,dof,expected = stats.chi2_contingency(contigency_table)
print(f'Chi-Squared Statistic: {round(chi2_stat,3)}')
print(f'P Value: {p_value}')
print(f'Degrees of Freedom: {dof}')
```
71
<ul>
  <li>Chi-Squared Statistic: 172.311 (rounded to three decimal places): This is the calculated chi-squared statistic. It measures the strength of the association between the variables in your contingency table.</li>
  <li>P Value: 3.8296283676391616e-38: This is the p-value obtained from the chi-squared test. It is an extremely small value, indicating that the association between the variables is highly statistically significant.</li>
  <li>Degrees of Freedom: 2: This is the degrees of freedom for the chi-squared test, indicating the constraints on the chi-squared statistic.</li>
  <li>Conclusion:Gender does influence payment behavior.</li>
</ul>

<li>Income & Payment Difficulty:</li>
<p>Clients with lower total incomes might face more challenges in making timely payments.
</p>
<p>Null Hypothesis (H0): 
There is no significant association between income and payment difficulty.
Income does not influence payment behavior.</p>

<p>Alternative Hypothesis (H1): There is a significant association between income   and payment difficulty. Lower income is associated with a higher likelihood of payment difficulty.
</p>

```
income_ranges = [-1,400000,800000,float('inf')]
income_labels=['Low Income','Moderate Income','High Income']
app_data['Income_Category'] = pd.cut(app_data['AMT_INCOME_TOTAL'], bins=income_ranges, labels=income_labels)
app_data['Income_Category'].value_counts()
```
72

```
plt.figure(figsize=(12,6))
sns.countplot(data = app_data,x='Income_Category',hue = 'TARGET')
plt.show()
```
73

```
contingency_table = pd.crosstab(app_data['Income_Category'],app_data['TARGET'])
chi2_stats,p_value,dof,expected = stats.chi2_contingency(contingency_table)
print(chi2_stats)
p_value
```
74
<ul>
  <li>The chi-squared statistic (0.523) is relatively small, indicating a weak association between income categories and the target variable (which may represent payment difficulty). 
</li>
  <li>The p-value (0.770) is greater than the typical significance level of 0.05. This suggests that there isn't strong evidence to conclude that income category and the target variable are significantly associated.</li>
</ul>
<p>Conclusion:
</p>
<p>The p-value being greater than 0.05 suggests that any observed differences between income categories and payment difficulty could be due to chance rather than a real effect.</p>

<li>Age & Payment Difficulty:</li>
<p>Younger clients might face more payment difficulties than older clients.
</p>
<p>Null Hypothesis (H0): There is no significant association between age and payment difficulty. Age does not influence payment behavior.</p>
<p>Alternative Hypothesis (H1): There is a significant association between age and payment difficulty. Younger clients are more likely to face payment difficulties than older clients.</p>

```
app_data['DAYS_BIRTH_Age_Range'].unique()
```
75

```
bins = [20,30,40,60,float('inf')]
labels = ['Young','Moderate','old','Old+']
app_data['Age_Category'] = pd.cut(app_data['DAYS_BIRTH_Years'],bins = bins, labels = labels)
app_data['Age_Category'].value_counts()
```
76

```
plt.figure(figsize=(12,4))
sns.countplot(data=app_data,hue='TARGET',x='Age_Category')
plt.show()
```
77

```
young = list(range(20,30))
moderate=list(range(31,40))
old=list(range(41,60))
older= list(range(61,69))
f_statistic, p_value = stats.f_oneway(young,moderate,old,older)
print(f_statistic)
print(p_value)
```
78
Based on the results:
<ul>
  <li>The F-statistic of 159.16 indicates that there are significant differences in the numerical data (possibly related to payment difficulty) among the age groups.
</li>
  <li>The very small p-value (5.82e-23) indicates that these differences are highly statistically significant. In other words, it is highly unlikely to observe such extreme differences in group means by chance alone.</li>
</ul>
<p>Therefore, I can conclude that there are statistically significant differences in the data analyzed among the age groups. This suggests that age may play a significant role in determining the observed numerical differences (possibly related to payment difficulty) among the groups.
</p>

<li>Loan Amount & Payment Difficulty:</li>
<p>Higher loan amounts might be associated with increased payment difficulties.</p>
<p>Null Hypothesis (H0): There is no significant association between loan amount and payment difficulty. Loan amount does not influence payment behavior.
</p>
<p>Alternative Hypothesis (H1): There is a significant association between loan amount and payment difficulty. Higher loan amounts are associated with increased payment difficulties.</p>

```
app_data['AMT_CREDIT_RANGE'].unique()
```
79

```
bins=[0,10,30,40,float('inf')]
labels = ['Low','Moderate','High','Extreme']
app_data['Amt_Credit_Category'] = pd.cut(app_data['AMT_CREDIT_Lakhs'],bins = bins,labels=labels)
app_data['Amt_Credit_Category'].value_counts()
```
80

```
plt.figure(figsize=(12,6))
sns.countplot(data=app_data,x='Amt_Credit_Category',hue='TARGET')
plt.show()
```
81

```
contingency_table = pd.crosstab(app_data['Amt_Credit_Category'],app_data['TARGET'])
contingency_table
```
82

```
chi2_stat,p_value,dof,expected=stats.chi2_contingency(contingency_table)
print(chi2_stat)
print(p_value)
```
83
<p>Based on the results of the chi-squared test, I can conclude that there is a highly statistically significant association between "Loan Amount" and "Payment Difficulty." The small p-value indicates that it is extremely unlikely to observe the observed distribution of payment difficulties across different loan amount categories (or more extreme distributions) if "Loan Amount" and "Payment Difficulty" were independent.</p>

<li>Loan Type & Payment Difficulty:</li>
<p>Certain types of loans, like cash loans, might be associated with more payment difficulties than revolving loans.</p>
<p>Null Hypothesis (H0): There is no significant association between loan type and payment difficulty. Loan type does not influence payment behavior.</p>
<p>Alternative Hypothesis (H1): There is a significant association between loan type and payment difficulty. Certain loan types are associated with more payment difficulties than others.</p>

```
plt.figure(figsize=(12,6))
sns.countplot(data=app_data,x='NAME_CONTRACT_TYPE',hue='TARGET')
plt.show()
```
84

```
contingency_table = pd.crosstab(app_data['NAME_CONTRACT_TYPE'],app_data['TARGET'])
contingency_table
```
85

```
chi2_stat,p_value,dof,expected=stats.chi2_contingency(contingency_table)
print(chi2_stat)
print(p_value)
```
86
<p>Based on the results of the chi-squared test, I can conclude that there is a highly statistically significant association between "Loan Type" and "Payment Difficulty."
The small p-value suggests that it is extremely unlikely to observe the observed distribution of payment difficulties across different loan types (or more extreme distributions) if "Loan Type" and "Payment Difficulty" were independent.
</p>
</ol>

### Conclusion
<ul>
  <li>"This case study has been an invaluable learning experience, providing me with a deeper understanding of real-world problems and the intricacies of the exploratory data analysis (EDA) process. I have gained proficiency in various statistical tests, including the chi-square test, t-test, and F-test, which are essential tools for extracting meaningful insights from data.
</li>
  <li>The use of web-based applications like Jupyter Notebook has significantly facilitated the analysis process, allowing for seamless exploration and visualization of data. Leveraging the Pandas library has not only made data manipulation more convenient but has also boosted my confidence in handling complex datasets.
</li>
  <li>Beyond the technical aspects, I have delved into documentation and research to enhance my knowledge further. This case study has not only equipped me with valuable skills but has also inspired me to apply these insights to practical, real-world scenarios. The ability to inform business decisions, improve lending practices, and enhance risk assessment strategies with data-driven approaches is a powerful skillset I have developed.</li>
  <li>I am committed to continuous learning and plan to expand my knowledge in data analysis and related fields. In conclusion, this case study has been a pivotal step in my data analysis journey, equipping me with the tools and knowledge needed to tackle complex problems and contribute meaningfully to data-driven decision-making."
</li>
</ul>

### Limitations
<ul>
  <li>Causality vs. Correlation:While statistical associations and correlations have been identified between certain variables and payment difficulties, it's essential to remember that correlation does not imply causation. Factors influencing loan repayment can be complex and multifaceted, and establishing causality would require more extensive research and data.</li>
  <li>Socioeconomic Factors: The analysis seems to focus primarily on the internal factors related to loan applications. External socioeconomic factors, such as economic conditions, employment rates, and legislative changes, can also significantly impact loan repayment but may not be considered in this analysis.
</li>
  <li>Modeling: This analysis primarily focuses on exploratory data analysis (EDA) and statistical tests. Developing predictive models or risk assessment models would require a separate and more comprehensive analysis, including feature engineering and machine learning techniques.</li>
</ul>







