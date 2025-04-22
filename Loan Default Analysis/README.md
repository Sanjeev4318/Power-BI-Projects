# Loan Default Analysis - Power BI 📊
In this project I have used data flow as the data source and i have used the loan default dataset. 
It is a three page report and here you can see that I have used line charts, ribbon chart, decomposition tree chart and donut charts.

### First Page: Loan Default Overview

![FirstPage_SC](https://github.com/user-attachments/assets/c609e2a1-8df2-4637-a198-a7f4dd6fd3f0)

### Second Page: Applicant Demographics & Financial Profile
![SecondPage_SC](https://github.com/user-attachments/assets/9cb923ba-ed0f-49ef-8f1f-1ed81fb36ab3)

### Third Page: Financial Risk Metrics
![ThirdPage_SC](https://github.com/user-attachments/assets/bb4c731d-6ee8-4828-88d7-345cb3c0f7ae)


## Data Source : Dataflows (Setting Up Dataflows)

To use dataflows we need gateway as well. To set up dataflows I followed below steps:
### Steps:
- Login to the power bi account.
- Create a new workspace, creared the workspace named Loan Default Analysis.
- Click on download and then click on Data Gateway to download the gateway. I have downloaded the standard mode gateway.
- I have named the gateway as DF1 representing the dataflows.
- I have imported the data to Microsoft SQL server and we will use SQL to create dataflows.
- The dataset table name is Loan_default
- Click on workspaces and then click on Loan Default Analysis, Now click on New Item and search Dataflows and then we have two options Gen one and Gen two.
- For this project i have used Gen one
- Then click on Add New Tables and select SQL server and provide the details to connect then click on next and select the loan_default table.
- I have named it as "DataflowsSQL_loan"

## Connecting to dataflow and getting data in power bi desktop:

### Steps:
- Login to the power bi desktop
- Click on get data
- Select dataflows and click on connect
- Click on signin and click on connect
- Now click on load 

## Loan Default dataset description:
The Loan Default Dataset contains information about borrowers who have applied for loans, along with details about their financial status, loan characteristics, and repayment behavior.

| Column Name  | Defination |
| ------- | ------- |
| <b>LoanID</b> | A unique identifier for each loan in the dataset. |
| <b>Age</b> | The borrower's age at the time the loan was issued. |
| <b>Income</b> | The borrower's annual income |
| <b>LoanAmount</b> | The total amount of the loan that the borrower is requesting or has been approved for. |
| <b>CreditScore </b> | A numerical representation of the borrower's creditworthiness, typically ranging from 300 to 850. A higher credit score indicates the borrower is more likely to repay the debt. |
| <b> MonthsEmployed</b> | The number of months the borrower has been employed at their current job or with their current employer. |
| <b>NumCreditLines </b> | The total number of active credit lines (e.g., credit cards, loans) the borrower has at the time of applying for the loan. |
| <b>InterestRate </b> | The annual percentage rate (APR) charged for borrowing the loan amount, usually expressed as a percentage. |
| <b> LoanTerm</b> | The length of time (in months) over which the loan is to be repaid. |
| <b>DTIRatio </b> | The Debt-to-Income ratio, which measures the borrower’debt payments relative to their income. A higher ratio can indicate greater financial stress. |
| <b> Education</b> | The highest level of education the borrower has completed (e.g., High School, Bachelor’s, Master’s, etc.). |
| <b>EmploymentType </b> | The type of employment the borrower is engaged in (e.g., Full-Time, Part-Time, Self-Employed, etc.). |
| <b> MaritalStatus</b> | The marital status of the borrower (e.g., Single, Married, Divorced, etc.). |
| <b>HasMortgage </b> | An  indicator (e.g., Yes/No) that shows whether the borrower has an existing mortgage on a property. |
| <b>HasDependents </b> | An  indicator (e.g., Yes/No) that shows whether the borrower has dependents (children, other family members) to support. |
| <b> LoanPurpose</b> | The primary reason for taking out the loan (e.g., Home Purchase, Debt Consolidation, Education, etc.). |
| <b>HasCoSigner </b> | An  indicator (e.g., Yes/No) that shows whether the borrower has a co-signer for the loan (someone who agrees to take responsibility if the borrower defaults). |
| <b> Default</b> | An  indicator (e.g., Yes/No) that shows whether the borrower defaulted on the loan or failed to make timely payments. |
| <b>Loan Date (DD/MM/YYYY) </b> | The date the loan was issued or originated. |


## Transform Data
Added three calculated columns <b>AgeGroup</b>,<b>CreditScoreBins</b> and <b>IncomeBracket</b>  
### AgeGroup
Added AgeGroup column using below dax:

      AgeGroup = 
         SWITCH(TRUE(),
         Loan_default[Age]<=19,"Teens",
         Loan_default[Age]<=39,"Adults",
         Loan_default[Age]<=59,"Middle Age Adults",
         "Senior Citizens"
      )

### CreditScoreBins
Added CreditScoreBins using below dax:

     CreditScoreBins = 
          SWITCH(TRUE(),
          Loan_default[CreditScore]<=400,"Poor",
          Loan_default[CreditScore]<=550,"Fair",
          Loan_default[CreditScore]<=650,"Good",
          "Excellent"
      )
### IncomeBracket
Added IncomeBracket using below dax:

         Income Bracket = 
              SWITCH(TRUE(),
              Loan_default[Income]<30000, "Low Income",
              Loan_default[Income]>=30000 && Loan_default[Income]<60000, "Middle Income",
              Loan_default[Income]>=60000, "High Income"
         )  


## Create a DateMaster table:
Created the datemaster table using below dax:

               DateMaster = ADDCOLUMNS(
                  CALENDAR(FIRSTDATE(Loan_default[Loan_Date_DD_MM_YYYY]),LASTDATE(Loan_default[Loan_Date_DD_MM_YYYY])),
                  "Year", YEAR([Date]),
                  "MonthNo",MONTH([Date]),
                  "Month",FORMAT([Date],"mmm")
               )

## Data Modeling
Connect Loan_default table to the DateMaster table 
![DataModeling_SC](https://github.com/user-attachments/assets/b0cc0073-ea0d-40ee-ad2a-234ac255db9e)

### Dashboard 📊





![Snap 2]

