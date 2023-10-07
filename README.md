# Lending-Club-Default-Neural-net


## Data Summary
This data was comprised of the following features: credit.policy: 1 if the customer meets the credit underwriting criteria of LendingClub.com, and 0 otherwise. In other words Binary classification

purpose: The purpose of the loan (takes values "credit_card", "debt_consolidation", "educational", "major_purchase", "small_business", and "all_other").

int.rate: The interest rate of the loan, as a proportion (a rate of 11% would be stored as 0.11). Borrowers judged by LendingClub.com to be more risky are assigned higher interest rates.

installment: The monthly installments owed by the borrower if the loan is funded.

log.annual.inc: The natural log of the self-reported annual income of the borrower.

dti: The debt-to-income ratio of the borrower (amount of debt divided by annual income).

fico: The FICO credit score of the borrower.

days.with.cr.line: The number of days the borrower has had a credit line.

revol.bal: The borrower's revolving balance (amount unpaid at the end of the credit card billing cycle).

revol.util: The borrower's revolving line utilization rate (the amount of the credit line used relative to total credit available).

inq.last.6mths: The borrower's number of inquiries by creditors in the last 6 months.

delinq.2yrs: The number of times the borrower had been 30+ days past due on a payment in the past 2 years.

pub.rec: The borrower's number of derogatory public records (bankruptcy filings, tax liens, or judgments).

## Problem Statement:
For companies like Lending Club correctly predicting whether or not a loan will be a default is very important. In this project, using the historical data from 2007 to 2015, you have to build a deep learning model to predict the chance of default for future loans

## TLDR:

We initialize pandas and numpy librarys for data frame reading and manipulation. We build the data frame with loan_data.csv, and perform basic manipulation. Identifying dataframe describe, row and column size, headers, and dtypes. We identify the not_fully_paid column which is what we will be comparing. The pie chart shows the count of transactions for Fully paid vs not fully paid, as our goal is to create a model to identify those who will default. we can see it's 16% not fully paid, and 84% paid their full statement on time. Now that we know 16% of transactions are not fully paid, we have to figure out the purpose. We add the purpose into a grouping, with only the not_fully_paid and plot this into a table for the purpose of viewing the data in a list. As a result, we get two columns, Purpose and the count under each purpose. Here is the fun part, we group our other features in the dataframe. I'll drop the list below.

int.rate             float64
installment          float64
log.annual.inc       float64
dti                  float64
fico                   int64
days.with.cr.line    float64
revol.bal              int64
revol.util           float64
inq.last.6mths         int64
delinq.2yrs            int64
pub.rec                int64



With these features, we create groupings 1-11, within each grouping we Create pivot tables to calculate the mean (average) values of several numerical columns using the not fully paid column. We have to split our groupings into two. Due to a real estate limit. So in the code, you'll see 1-5, and 6-11. Each of the groupings is re-labeled as a new feature. Then we use OneHotEncoder, to turn all of our 11 groupings into values to either a 0 or a 1. We re-merge the 11 groups now our features. We add the 11 features back into the original dataset. When we print the new data frame, we can see one column we must take care of. Everything is an integer, except purpose. This column is still a string, so we remove the purpose column from our data frame by dropping it. Finally, all we have is a gigantic data frame with every single cell as a number. We Initialize a heatmap for the sake of understanding the correlation between each feature. We split out the dataframe into train tests, our ratio is 75% train and 25% test. Next our Train test split, we have to use the standard scaler on our split data. We import the tensorflow library, and proceed to creating a neural net with 4 layers deep. We use sigmoid as our activatio fuction across all 4 layers. We did some experimetation with ReLu, like switching the first 3 layers, while keeping sigmoid for the final layer (after all we are doing classification) we use the ADAM optimizer. In combination with back propogation in order to train our dataset. we proceed with the initial test, at 10 epochs. After 10 epochs, we can see no overfitting, and the accuracy score increase. We re-run the neural net with 100 epochs, and plot the Accuracy and Train Loss. 


