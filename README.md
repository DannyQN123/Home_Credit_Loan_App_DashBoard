# Home_Credit_Loan_Applicant_DashBoard  
- ***The purpose of the project is:*** to create Dashboards to gain some insights on Home Credit's loan applicants. Because the datasets is plenty, we will only focus on the ***application_train.csv***.   
- Basically we will conduct Exploratory Data Analysis to analyze the loan applicants' background.
- Original datasets: https://www.kaggle.com/c/home-credit-default-risk.

## The conclusions (still updating):
- The largest customer segment by Occupation Type are laborers (26.14%). 
- This segment of applicants also have the top 5 highest default rate (about 10.58%).

## Tools used:
- ***Python:*** used for checking for missing values (Number of missing values for each column). 
- ***SQLite:*** particularly DB Browser for SQLite. As our Dataset is in CSV format, create a database from these .CSV files is simple with SQLite.
- ***PowerBI:*** for Dashboard Visualization.
  
## Python script for checking missing values:
```Python
import pandas as pd
application_train = pd.read_csv('./datasets/application_train.csv')

# Function to calculate missing values by column 
def missing_values_table(df): 
    # Total missing values 
    mis_val = df.isnull().sum() 
    # Percentage of missing values 
    mis_val_percent = 100 * df.isnull().sum() / len(df) 
    # Make a table with the results 
    mis_val_table = pd.concat([mis_val, mis_val_percent], axis=1) 
    # Rename the columns 
    mis_val_table_ren_columns = mis_val_table.rename( columns = {0 : 'Missing Values', 1 : '% of Total Values'}) 
    # Sort the table by percentage of missing descending 
    mis_val_table_ren_columns = mis_val_table_ren_columns[ mis_val_table_ren_columns.iloc[:,1] != 0].sort_values( '% of Total Values', ascending=False).round(1) 
    # Print some summary information 
    print ("Your selected dataframe has " + str(df.shape[1]) + " columns.\n" "There are " + str(mis_val_table_ren_columns.shape[0]) + " columns that have missing values.") 
    # Return the dataframe with missing information 
    return mis_val_table_ren_columns

missing_values = missing_values_table(application_train)
missing_values
```
***Output:***  
![Check Missing Values (1a)](https://github.com/DannyQN123/Home_Credit_Loan_App_DashBoard/assets/107457149/26cf2ba5-2b3b-4e3c-9940-c0f322cf13ea)  

![Check Missing Values (1)](https://github.com/DannyQN123/Home_Credit_Loan_App_DashBoard/assets/107457149/9d116d16-3033-405d-b986-1991836e2326)


## SQL Queries:  

- Number of Applicants (Thounsands) by ***Family Status***:  
```SQL
SELECT NAME_FAMILY_STATUS, COUNT(NAME_FAMILY_STATUS) AS Number_of_Applications
FROM application_train
GROUP BY NAME_FAMILY_STATUS
ORDER BY Number_of_Applications DESC`
```

- Number of Applicants (Thounsands) by ***Occupation Type***:  
```SQL
SELECT OCCUPATION_TYPE, COUNT(OCCUPATION_TYPE) AS Number_of_Applications
FROM application_train  
GROUP BY OCCUPATION_TYPE  
HAVING OCCUPATION_TYPE NOT NULL  
ORDER BY Number_of_Applications ASC`
```

- Number of Applicants (Thounsands) by ***Income Type***:  
```SQL
SELECT NAME_INCOME_TYPE, COUNT(NAME_INCOME_TYPE) AS Number_of_Applications
FROM application_train
GROUP BY NAME_INCOME_TYPE
ORDER BY Number_of_Applications ASC
```

- Default Rate (%) by ***Family Status***:  
```SQL
SELECT
    NAME_FAMILY_STATUS,
    ROUND((SUM(CASE WHEN TARGET = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(NAME_FAMILY_STATUS)), 2) AS Default_Rate
FROM
    application_train
GROUP BY
    NAME_FAMILY_STATUS
HAVING NAME_FAMILY_STATUS NOT LIKE "%Unknown%"
ORDER BY 
	Default_Rate ASC
```

- Default Rate (%) by ***Occupation Type***:  
```SQL
SELECT
    OCCUPATION_TYPE,
    ROUND((SUM(CASE WHEN TARGET = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(OCCUPATION_TYPE)), 2) AS Default_Rate
FROM
    application_train
GROUP BY
    OCCUPATION_TYPE
HAVING OCCUPATION_TYPE NOT NULL
ORDER BY 
	Default_Rate ASC
```

- Default Rate (%) by ***Income Type***:  
```SQL
SELECT
    NAME_INCOME_TYPE,
    ROUND((SUM(CASE WHEN TARGET = 1 THEN 1 ELSE 0 END) * 100.0 / COUNT(NAME_INCOME_TYPE)), 2) AS Default_Rate
FROM
    application_train
GROUP BY
    NAME_INCOME_TYPE
HAVING NAME_INCOME_TYPE NOT NULL
ORDER BY 
	Default_Rate ASC
```

## Dashboards:  
***DashBoard - Applications & Default Rate by Income Type and Family Status***  

![DashBoard - Applications   Default Rate by Income Type and Family Status](https://github.com/DannyQN123/Home_Credit_Loan_App_DashBoard/assets/107457149/7e17c709-6d69-4cde-9af1-00592f41111e)

***DashBoard - Applications & Default Rate by Occupation***  

![DashBoard - Applications   Default Rate by Occupation](https://github.com/DannyQN123/Home_Credit_Loan_App_DashBoard/assets/107457149/9344daa0-bb58-470c-a9a1-9081b6a2987d)
