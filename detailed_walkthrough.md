## Lending Club Loan Dataset

Lending Club is the world's largest peer-to-peer lending platform. They make money by charging borrowers an origination fee(1.1-5%) and investors a service fee(1%). 

The dataset can be downloaded [here](https://www.lendingclub.com/info/download-data.action).

## Task

Given a quarter's records of all the loans approved, we want to predict if a new given loan will go default or not.

For a given observation:

- **Predictors**:  information about the borrower & the loan
- **Outcome**: current status of the loan (default / non-default)

As analyized above, this can be viewed as a **Binary Classification** task.



## Model

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

![](/Users/jacqueline/My/Duke-MIDS/Projects/LendingClub-RiskModeling/image/logfunc.png) 

1. Classification.

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

- Manually Drop redundent, irrelevant & info-leaking features: -18
- derive new variable:
  - Installment_feat = installment / annual_inc

### Encode Categorical Features

- loan_status: collapse to only 2 categories: 1: default, 0: non-default
- Ordinal: assign integer values from 0, len(feature)-1
- Nominal: One-hot Encoding (dummy variables)

### Scaling

- Standardization: $x_{s}=(x-μ)/σ$

### Feature Selection

using **Recursive Feature Elemination**, we decrease the features we use down to 30.



## Unbalanced Data

The data we have is quite unbalance. We deal this issue by using **SMOTE** :

|        | Non-default    | Default        | Total  |
| ------ | -------------- | -------------- | ------ |
| Before | 99198 (94.07%) | 6253 (5.93%)   | 105451 |
| After  | 99198 (50.00%) | 99198 (50.00%) | 198396 |



## Results

Results are of trainned model with L2 regularization & strength of C=1000. (selected using grid search).

### Confusion Matrix

|             | Ture 0 | True 1 |
| ----------- | ------ | ------ |
| Predicted 0 | 22916  | 6731   |
| Predicted 1 | 12184  | 17688  |

In risk modelling, we want the occurance of FN to be as low as possible. We have 6731 as our result, which isn't so bad.



### ROC Curve

![roc](/Users/jacqueline/My/Duke-MIDS/Projects/LendingClub-RiskModeling/image/roc.png)

Area under ROC curve: 0.68