# Bank_Loan_Case_Study

- [Project Description](#header-name)
- [Business Understanding](#business-understanding)
- [Data Understanding](#data-understanding)

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
### Business Objectives:
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

### Approach & Tech-Stack Used:
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
