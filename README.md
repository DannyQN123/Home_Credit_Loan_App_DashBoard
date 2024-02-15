# Home_Credit_Loan_Applicant_DashBoard  
- ***The purpose of the project is:*** to create Dashboards to gain some insights on Home Credit's loan applicants. Because the datasets is plenty, we will only focus on the ***application_train.csv***.   
- Basically we will conduct Exploratory Data Analysis to analyze the loan applicants' background.  
## The conclusion:
- A large percentage of the applicants of Home Credit's Loan are laborer, and they are married.
-  
Original datasets: https://www.kaggle.com/c/home-credit-default-risk
## SQL Queries:  

- Number of Applicants by ***Family Status***:  
`SELECT NAME_FAMILY_STATUS, COUNT(NAME_FAMILY_STATUS) AS Number_of_Applications
FROM application_train
GROUP BY NAME_FAMILY_STATUS
ORDER BY Number_of_Applications DESC`  

- Number of Applicants by ***Occupation Type***:  
`SELECT OCCUPATION_TYPE, COUNT(OCCUPATION_TYPE) AS Number_of_Applications
FROM application_train  
GROUP BY OCCUPATION_TYPE  
HAVING OCCUPATION_TYPE NOT NULL  
ORDER BY Number_of_Applications ASC`  

## Dashboards:  
***DashBoard - Applications & Default Rate by Income Type and Family Status***  

![DashBoard - Applications   Default Rate by Income Type and Family Status](https://github.com/DannyQN123/Home_Credit_Loan_App_DashBoard/assets/107457149/7e17c709-6d69-4cde-9af1-00592f41111e)

***DashBoard - Applications & Default Rate by Occupation***  

![DashBoard - Applications   Default Rate by Occupation](https://github.com/DannyQN123/Home_Credit_Loan_App_DashBoard/assets/107457149/9344daa0-bb58-470c-a9a1-9081b6a2987d)
