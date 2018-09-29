---
title: Lending Club Data Analysis
tags: Data Science
---
## Backgound Knowledge
### FICO
The FICO score was first introduced in 1989 by FICO, then called Fair, Isaac, and Company.[3] The FICO model is used by the vast majority of banks and credit grantors, and is based on consumer credit files of the three national credit bureaus: Experian, Equifax, and TransUnion. Because a consumer's credit file may contain different information at each of the bureaus, FICO scores can vary depending on which bureau provides the information to FICO to generate the score.
FICO信用分计算的基本思想上把借款人过去的信用历史资料与数据库中的全体借款人的信用习惯相比较，检查借款人的发展趋势跟经常违约、随意透支、甚至申请破产等各种陷入财务困境的借款人的发展趋势是否相似。美国各种信用分的计算方法中，FICO信用分的正确性最高。据一项统计显示，信用分低于600分，借款人违约的比例是1/8，信用分介于700～800分，违约率为1/123，信用分高于800分，违约率为1/1292。因此美国商务部要求在半官方的抵押住房业务审查中使用FICO信用分。

### Business Model
Lending Club的利润主要来自对贷款人收取的手续费和对投资者的管理费，前者会因为贷款者个人条件的不同而有所起伏，一般为贷款总额的1.1-5%；后者则是统一对投资者收取一样的1%的管理费

借款人年利率：5.59起
年回报率：6.03%-27.49%

## Concepts and Definitions
### Extracted Features
- loan_amnt: The listed amount of the loan applied for by the borrower. If at some point in time, the credit department reduces the loan amount, then it will be reflected in this value.
- term: The number of payments on the loan. Values are in months and can be either 36 or 60.
- int_rate: Interest Rate on the loan.
- grade: LC(Lending Club) assigned loan grade.
- issue_d: The date which the borrower's application was issued on the platform.
- addr_state: The state provided by the borrower in the loan application.
- loan_status: The status of the loan. See [*The 10 loan status variants explained*](https://help.bitbond.com/article/20-the-10-loan-status-variants-explained) for more information.
- purpose: A category provided by the borrower for the loan request.
- annual_inc: The self-reported annual income provided by the borrower during registration.
- emp_length: Employment length in years. Possible values are between 0 and 10 where 0 means less than one year and 10 means ten or more years.

### Other terms
- Debt consolidation: a form of debt refinancing that entails taking out one loan to pay off many others.

## Target


## Data Cleaning
### Quality Issues
- 'int_rate' and 'emp_length': datatype should be float instead of object ->astype("float")
- 'int_rate': unwanted '%' sign
- 'issue_d' datatype should be datetime instead of ?. -> pd.to_datetime()
- most values in some columns are void. -> delete those columns
- 'loan_status' has a few error value 'n'.  -> drop() those rows

### Tidiness Issues
- 'loan_status' has too many categories. -> only classify a case into normal(1)/ abnormal(0)
- 'loan_status'  has unbalanced 1/0 ratio ->???


## Data Analysis
### Single Variable
### Multiple Variable

## Feature Engineering
### Feature Derivative
### Feature Abstraction

## Reference
https://www.huxiu.com/article/41472/1.html
