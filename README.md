## The Lending Club Loan Dataset

Lending Club is the world's largest peer-to-peer lending platform. They make money by charging borrowers an origination fee(1.1-5%) and investors a service fee(1%). The standard loan period is three years. 

### Code Book 

#### Predictors 

**loan_amnt**: The listed amount of the loan applied for by the borrower. If at some point in time, the credit department reduces the loan amount, then it will be reflected in this value.

**term**: The number of payments on the loan. Values are in months and can be either 36 or 60.

**int_rate**: Interest rate on the loan.

**grade**: LC(Lending Club) assigned loan grade.

**issue_d**: The date which the borrower's application was issued on the platform.

**addr_state**: The state provided by the borrower in the loan application.

**purpose**: A category provided by the borrower for the loan request.

**annual_inc**: The self-reported annual income provided by the borrower during registration.

**emp_length**: Employment length in years. Possible values are between 0 and 10 where 0 means less than one year and 10 means ten or more years.

**delinq_2yrs**: The number of 30+ days past-due incidences of delinquency in the borrower's credit file for the past 2 years.

#### Outcome

**loan_status**: The status of the loan. See [The 10 loan status variants explained](https://help.bitbond.com/article/20-the-10-loan-status-variants-explained) for more information.



## The Task

Given a quarter's records of all the loans approved, we want to predict if a new given loan will go default or not.

For a given observation:

- **Predictors**:  information about the borrower & the loan

- **Outcome**: current status of the loan (default / non-default)

As analyized above, this can be viewed as a **Binary Classification** task.



## The Model

We apply a Logistic Regression to solve the binary classification problem.

### Logistic regression

1. Score function.

   First we need to have a **Score Function**: 

$$
t_i = f(x_i)
$$
​	this is the most important part of our work. f(x) is the model/algorithm we will use. It could be as simple as a linear model ($f(x_i) = \beta_0 + \sum_{j=1}^n \beta_jx_{ij}$), or a deep learning model such as a Neuron Network.

​	Note: $x_i$ is a vector,  $x_i \in R^n$ where $n$ is the number of features. $t_i$ is a real scalar. 

2 . Calculate probability. 

​	No matter what algorithm we use to calculate the score, we will use the **Logistic Function** to scale it in the range of (0, 1) :
$$
\pi_i = Pr(Y=1|x_i)=  \frac{e^{t_i}}{1 + e^{t_i}} = \frac{1}{1 + e^{-t_i}}
$$
​	The plot of the logistic function is as follow:

![](image/logfunc.png) 

3. Classification.

   We set the threshold for classification to 0.5. That is to say, given an observation $x_i$: 

- if the probability $\pi_i >= 0.5$, we classify it as label 1
- if the probability $\pi_i < 0.5$, we classify it as label 0



## Data Cleaning

### Dropping variables

- Delete columns with more than 40% of missing values, as well as with same values for all observations. 

- Delete irrelevant features(eg. Zip code) 
- Delete information-leaking features 

### Type Conversions

- Convert *int_rate, revol_util* from obj to float

### Dealing with Missing Values

- Categorical: fill NaN with 'Unknown'
- Numerical: using **Mean Interpolation**  `Imputer` in sklearn



## Feature Engineering

### Add / Drop variables

- Manually Drop redundent, irrelevant & info-leaking features:  -18
- derive new variable:
  - Installment_feat = installment / annual_inc

### Encode Categorical Features

- loan_status: collapse to only 2 categories: 1: default, 0: non-default

- Ordinal: assign integer values from 0, len(feature)-1
- Nominal: One-hot Encoding (dummy variables)

### Scaling

- Standardization: $x_{s}=(x-μ)/σ$

### Feature Selection

using **Recursive Feature Elemination** 





