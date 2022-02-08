# Power-Bi-Sales-insight-Analysis
The dataset used for this analysis is Atliq sales Dataset. Atliq Hardware is a company which provide computer hardware and peripheral to their clients such as excel stores, electronic stores and surge stores.

## Problem Statement

Sales analysis is mining your data to evaluate the performance of your sales against its goals. It provides insights about the top performing and underperforming products/services, the problems in selling and market opportunities, sales forecasting, and sales activities that generate revenue.

In today world, the market is growing dynamically and companies such as ATLIQ, faces issues regarding tracking the sales in dynamically growing market and gaining information or insight about the company sales. ATLIQ have three regional offices in India, and stakeholders or CEO requires update of their company sales regularly in order to make data driven decisions and to get update about company growth. Thus requires sales analysis of their regional offices on daily basis in order to focus on weakness of regional offices where the sales numbers are declining. the sales analysis helps to make decision to promote services or give promotions in order to catch up the loss in sales. Sales analysis provides simple, understandable and digestable insight to stakeholders or CEOs.

## AIMS GRID

### Purpose
To unlock sales insight that are not visible before for sales team for decision support & automate them to reduced manual time spent in data gathering.
### Stakeholders
-Sales Director
-Marketing Team
-Data & Analytics Team
-Customer Service Team
### End Result
An Automated Dashboard providing quick & latest sale insights in order to support data driven decision making.
### Success Criteria
-Dashboard(s) uncovering sales order insights with latest data available
-Sales team able to take better decisions & prove 10% cost savings of total spend
-Sales analysts stop data gethering manually in order to save 20% of their business time and reinvest it value added activity.


## Setup

Data Analysis Using SQL ==>  DATA Cleaning & ETL ==> Build Dashboard

## Data Analysis using mySQL
Show all customer records

SELECT * FROM customers;

Show total number of customers

SELECT count(*) FROM customers;

Show transactions for Chennai market (market code for chennai is Mark001

SELECT * FROM transactions where market_code='Mark001';

Show distrinct product codes that were sold in chennai

SELECT distinct product_code FROM transactions where market_code='Mark001';

Show transactions where currency is US dollars

SELECT * from transactions where currency="USD"

Show transactions in 2020 join by date table

SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;

Show total revenue in year 2020,

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";

Show total revenue in year 2020, January Month,

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");

Show total revenue in year 2020 in Chennai

SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";

## DATA Cleaning and ETL with Power BI and Power query
Connect the Power BI with mySQL database to perform data cleaning and ETL. Power query is used to transform the data.

- Load the data into POWER BI via mySQL.
- Define the new relationships between tables and/or correct pre-defined relationships between tables. [STAR SCHEMA: Data modelling]
- Transform data using powerquery
  - Filtered the rows to select the observations which is linked to India regional offices.
  - Filter Sales Amount values which is less or equal to 0.
  - convert some of the sales amount which is given in USD currency to Indian Rupee(INR) by creating new column normalize        currency. Formula to create norm_amount column:=
  = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
  - correcting duplicates: in mysql we see that currency column is showing twice INR when trying to see distinct(transaction.currency), the problem lies in format where one is 'INR' simple and other is 'INR\r'.

## Build Dashboard
 
